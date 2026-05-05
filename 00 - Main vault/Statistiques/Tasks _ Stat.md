---
tags:
  - Personal/Stats
Creation date: 2025-03-04 15:44
banner: "[[DeathNoteBanner.jpg]]"
banner_x: 0
banner_y: 0.906
cssclasses:
  - daily
  - sNote
---

#### ☑️ To-Dos ❌
```dataviewjs
/***** CONFIG (unchanged) *****/
const calendarData = { year: 2026,
    intensityScaleStart: 0,
  intensityScaleEnd: 19,
  entries: [],
  separateMonths: true,
  colorScheme: {
    paletteName: "tasksV2",
    // taskV2p1: [
    //   "rgb(51, 51, 51)","rgb(77, 26, 26)","rgb(102, 26, 26)",
    //   "rgb(127, 38, 38)","rgb(153, 51, 51)","rgb(181, 61, 61)","rgb(255, 0, 0)"
    // ],
    // taskV2p2: [
    //   "rgb(51, 51, 51)","rgb(77, 77, 77)","rgb(102, 102, 102)",
    //   "rgb(150, 160, 180)","rgb(160, 160, 160)","rgb(217, 221, 222)"
    // ],
    // taskV2p3: [
    //   "rgb(50, 55, 75)","rgb(40, 45, 90)","rgb(30, 35, 100)",
    //   "rgb(15, 20, 80)","rgb(5, 15, 60)","rgb(0, 10, 51)"
    // ],
  }
};

const taskV2p1 = [
  'rgb(255, 0, 0)',
  'rgb(181, 61, 61)',
  'rgb(153, 51, 51)',
  'rgb(127, 38, 38)',
  'rgb(102, 26, 26)',
  'rgb(77, 26, 26)',
  'rgb(51, 51, 51)'
];
const taskV2p2 = [
  'rgb(217, 221, 222)',
  'rgb(160, 160, 160)',
  'rgb(150, 160, 180)',
  'rgb(102, 102, 102)',
  'rgb(77, 77, 77)',
  'rgb(51, 51, 51)'
];
const taskV2p3 = [
  'rgb(50, 55, 75)',
  'rgb(40, 45, 90)',
  'rgb(30, 35, 100)',
  'rgb(15, 20, 80)',
  'rgb(5, 15, 60)',
  'rgb(0, 10, 51)'
];

function scaleIntensity(count, isNotDone, date) {
  if (isNotDone) return (8 - count > 7) ? 1 : 8 - count;
  if (count > 0)   return (12 + count > 19) ? 19 : 12 + count;
  return (13 + count > 7) ? 13 + count : 8;
}

/***** FOLDERS (same as your script) *****/
const FOLDER_A = '00 - Main vault/Notes';
const FOLDER_B = '00 - Main vault/Meetings';

/***** 1) Indexed query over just the two folders *****/
const pages = dv.pages(`"${FOLDER_A}" or "${FOLDER_B}"`); // Dataview “source” is indexed

/***** 2) Single-pass aggregation: Map<ISODate, {done, not, cancel}> *****/
const byDate = new Map();
let C =0,Cc=0, Ccc=0;
for (const p of pages) {
	Ccc++;
  const ts = p.file?.tasks;
  if (!ts || ts.length === 0) continue;

  for (const t of ts) {
	  Cc++;
    if (!(t.scheduled || t.due)) continue;

    const dateKey = (t.scheduled ?? t.due).toISODate();
    let acc = byDate.get(dateKey);
    if (!acc) { acc = { done: 0, not: 0, cancel: 0 }; byDate.set(dateKey, acc); }

    const isCancelled = t.text.includes('❌') || (t.checked && !t.completed); // same intent
    C++;
    if (isCancelled) acc.cancel++;
    else if (t.completed) acc.done++;
    else acc.not++;
  }
}

//dv.span(C+' '+Cc+' '+Ccc);

/***** 3) Build entries (exact same semantics & content markup as yours) *****/
const dates = Array.from(byDate.keys()).sort(); // ISO sorts chronologically
for (const date of dates) {
  const { done, not, cancel } = byDate.get(date);
  const isNotDone = not > 0;

  // Restore your original adjustment:
  //   if cancel <= 7: subtract cancel
  //   else: subtract (cancel - 7)
  const subtract = (cancel - 7 > 0) ? (cancel - 7) : cancel;
  const effective = isNotDone ? not : (done - subtract);

  calendarData.entries.push({
    date,
    intensity: scaleIntensity(effective, isNotDone, date),
  });
}

/***** 4) Render heatmap *****/
const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData);

/***** 5) Legends row (avoid mutating palettes during reverse) *****/
const legendsContainer = document.createElement('div');
legendsContainer.style.display = 'flex';
legendsContainer.style.alignItems = 'center';
legendsContainer.style.justifyContent = 'center';
legendsContainer.style.width = '100%';
legendsContainer.style.marginBottom = '12px';

function makeLegend(text) {
  const legend = document.createElement('div');
  legend.innerText = text;
  legend.style.fontSize = '65%';
  legend.style.fontFamily = 'IBM plex mono, sans-serif';
  legend.style.textTransform = 'uppercase';
  legend.style.margin = '0 8px';
  return legend;
}
function makeBoxes(colors) {
  const boxContainer = document.createElement('div');
  boxContainer.style.display = 'flex';
  boxContainer.style.alignItems = 'center';
  for (let i = 0; i < colors.length; i++) {
    const box = document.createElement('div');
    box.style.width = '9px'; box.style.height = '9px';
    box.style.backgroundColor = colors[i];
    box.style.marginRight = '5px';
    boxContainer.appendChild(box);
  }
  return boxContainer;
}

legendsContainer.appendChild(makeLegend('Buzy with tasks to-do'));
legendsContainer.appendChild(makeBoxes(taskV2p1));

legendsContainer.appendChild(makeLegend('...    Canceled     ...'));
legendsContainer.appendChild(makeBoxes(taskV2p2));

legendsContainer.appendChild(makeLegend('...    Free     ...'));
legendsContainer.appendChild(makeBoxes(taskV2p3));

legendsContainer.appendChild(makeLegend('Tasks Done'));

heatmapTrackerEl.appendChild(legendsContainer);

// dv.span('Tasks tracker statistics:');
// renderHeatmapTracker(this.container, calendarData);

```