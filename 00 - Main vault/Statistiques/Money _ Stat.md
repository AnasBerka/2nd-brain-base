---
tags:
  - Personal/Stats
Creation date: 2025-03-04 15:45
banner: "[[DeathNoteBanner.jpg]]"
banner_x: 0
banner_y: 0.906
cssclasses:
  - daily
  - sNote
---

#### 💲Global wealth (Future)💲
```dataviewjs
const heatmapColors = [
  "rgb(204, 0, 0)",
  "rgb(255, 0, 0)",
  "rgb(255, 51, 51)",
  "rgb(255, 102, 102)",
  "rgb(255, 153, 153)",
  "rgb(255, 204, 204)",
  "rgb(128, 138, 166)",
  "rgb(77, 90, 128)",
  "rgb(51, 64, 114)",
  "rgb(25, 38, 99)",
  "rgb(0, 18, 77)",
  "rgb(0, 10, 51)"
];

const calendarData = { year: 2026,
    intensityScaleStart: 0,
    intensityScaleEnd: 12, // I have 12 color levels in heat
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "heat2",
//         "heat2": [
//         "rgb(204, 0, 0)",
//         "rgb(255, 0, 0)", 
//         "rgb(255, 51, 51)",
//         "rgb(255, 102, 102)",
//         "rgb(255, 153, 153)",  
//       "rgb(255, 204, 204)",    
//       "rgb(128, 138, 166)",
//       "rgb(77, 90, 128)",
//       "rgb(51, 64, 114)",
//       "rgb(25, 38, 99)",
//       "rgb(0, 18, 77)",
//       "rgb(0, 10, 51)",
//     ],
//     "heat3": [
//     "rgb(204, 0, 0)", 
//     "rgb(170, 20, 20)", 
//     "rgb(140, 35, 35)", 
//     "rgb(110, 45, 45)", 
//     "rgb(80, 50, 50)", 
//     "rgb(51, 51, 51)", 
//     "rgb(50, 55, 75)", 
//     "rgb(40, 45, 90)", 
//     "rgb(30, 35, 100)", 
//     "rgb(15, 20, 80)", 
//     "rgb(5, 15, 60)", 
//     "rgb(0, 10, 51)"
// ]   
    }
};

  function renderInlineLegend(container, colors, minLabel, maxLabel) {
    const legendsContainer = document.createElement('div');
    legendsContainer.style.display = 'flex';
    legendsContainer.style.alignItems = 'center';
    legendsContainer.style.justifyContent = 'center';
    legendsContainer.style.width = '100%';
    legendsContainer.style.marginBottom = '12px';
    legendsContainer.style.gap = '5px';

    const createLabel = (text) => {
      const label = document.createElement('div');
      label.innerText = text;
      label.style.fontSize = '65%';
      label.style.fontFamily = 'IBM plex mono, sans-serif';
      label.style.textTransform = 'uppercase';
      return label;
    };

    legendsContainer.appendChild(createLabel(minLabel));

    const colorsContainer = document.createElement('div');
    colorsContainer.style.display = 'flex';
    colorsContainer.style.alignItems = 'center';
    colorsContainer.style.gap = '5px';

    for (const color of colors) {
      const colorBox = document.createElement('div');
      colorBox.style.width = '9px';
      colorBox.style.height = '9px';
      colorBox.style.backgroundColor = color;
      colorsContainer.appendChild(colorBox);
    }

    legendsContainer.appendChild(colorsContainer);
    legendsContainer.appendChild(createLabel(maxLabel));
    container.appendChild(legendsContainer);
  }

const DAY_MS = 86_400_000;
const Cap = 16500*12*35+16500*5*3+32500;

const PS = dv.date("2014-02-07").startOf("day");
const PE = dv.date("2106-02-07").startOf("day");
const N = PE.diff(PS, "days")/DAY_MS; // total number of days

const minS = 50;       // minimum daily spend
const maxS = 1000;     // maximum daily spend

const daysPerYear = 365.25;
const Y = N/daysPerYear;

const r = Math.pow(maxS / minS, 1 / Y);   // yearly growth rate

// analytic normalization
const totalRaw =
    (daysPerYear * minS / Math.log(r)) *
    (Math.pow(r, N / daysPerYear) - 1);

const K = Cap / totalRaw;

function dailyS(date) {
    const i =
        (date.startOf("day").toMillis() - PS.toMillis()) / DAY_MS;
    if (i < 0 || i >= N) return 0;

    return K * minS * Math.pow(r, i / daysPerYear);
}


function dailySWithRemaining(date) {
    const i = Math.floor((date.startOf("day").toMillis() - PS.toMillis()) / DAY_MS)+1;
	if (i < 1) return { daily: 10, remaining: 1 };
    if (i > N) return { daily: maxS, remaining: 1 };

	const daily = dailyS(date);
	const remaining = N-i+1;
	
    return { daily, remaining };
}

let msg = ''
let moneyInDh = 0;

// Always normalize to start-of-day to avoid time-of-day drift.
const asDayStart = d => d.startOf('day');
const noteDate = (page) =>
  asDayStart(
    page.date            ? dv.date(page.date) :
    dv.date(page.file.name) ?? dv.date(page.file.cday)
  );
  
// --- state carried across iterations ---
let ctr = 0, ctr_ = 0;
let previousNote = null;     // will hold a dv link to the prior note
let previousDate = null;     // will hold the Luxon DateTime of the prior note

// Dates strictly between a and b (exclusive), 1-day steps
function daysBetweenExclusive(a, b) {
  const out = [];
  let d = a.plus({ days: 1 }).startOf('day');
  const end = b.minus({ days: 1 }).startOf('day');
  while (d <= end) { out.push(d); d = d.plus({ days: 1 }); }
  return out;
}

for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.moneyInDh || p.meTime || p.vOwnerfirstnameOwnerlastname || p.vCjBank2Bank).sort(p => p.file.name, 'asc')) {
    if (!dv.date(page.file.name)) continue;
    // current note’s normalized date
	const currentDate = noteDate(page);
	
	// compute gap in whole days between this and the previous; 0 on the first item
	let numberOfDays = previousDate
	? Math.round((currentDate.toMillis() - previousDate.toMillis()) / DAY_MS)
	: 0;
	
	// “successive” means exactly 1 day after the previous note
	const successive = previousDate ? (numberOfDays === 1) : true;
	
	// days missed are the days strictly between the two notes
	const missedDays = previousDate ? Math.max(numberOfDays - 1, 0) : 0;
	
	// I want to see if the next period using dailyS can be covered with money in dh
	const savedMoney = moneyInDh;
    if (previousNote) {
		//dv.paragraph(`${++ctr}. ${page.file.link} was logged after ${previousNote} by ${numberOfDays} day(s)` + (successive ? `.` : ` — missed ${missedDays}.`));
		if (missedDays > 0) {
		const missing = daysBetweenExclusive(previousDate, currentDate);
		missing.forEach(d => {
			const { daily: dDaily_, remaining: remDaily_} = dailySWithRemaining(dv.date(d));
			let dailyDhA = savedMoney/(dDaily_*remDaily_);
			//dv.span(d.toISODate()+"~"+savedMoney+" >"+dDaily_+"_"+remDaily_+"< "+dailyDhA+"</br>"); //check
			let scale; // Extract the date from the filename 
			if (dailyDhA >= 1) { scale = 11.5; } else if (dailyDhA*2 >= 1) { scale = 10.5; } else if (dailyDhA*4 >= 1) { scale = 9.5; } else if (dailyDhA*8 >= 1) { scale = 8.5; } else if (dailyDhA*16 >= 1) { scale = 7.5; } else if (dailyDhA*32 >= 1) { scale = 6.5; } else if (dailyDhA*64 >= 1) { scale = 5.5; } else if (dailyDhA*128 >= 1) { scale = 4.5; } else if (dailyDhA*256 >= 1) { scale = 3.5; } else if (dailyDhA*512 >= 1) { scale = 2.5; } else if (dailyDhA*1024 >= 1) { scale = 1.5; } else { scale = 0.5; }
		
		    // Push data to calendar
		    calendarData.entries.push({
		        date: d.toISODate(),
		        intensity: scale,
		        // color: "heat",
		    });
	});
		}
	}
	
	// retrieve the daily money
    moneyInDh += ((page.moneyInDh || 0) + (page.vCDBalance||0) + (page.vCjBank2Bank||0));
	
	// --- update carried state so the next iteration “knows” the previous note ---
	previousNote = page.file.link;   // this is how you “add” previousNote for the next loop
	previousDate = currentDate;      // needed to compute the next numberOfDays 

    
    // Extract the date from the filename
    const pageDate = dv.date(page.file.name).startOf("day");

	//Get averge that should be expected
    const { daily: dDaily, remaining: remDaily} = dailySWithRemaining(pageDate);
	let dailyDhA = moneyInDh/(dDaily*remDaily);
	let scale; // Extract the date from the filename 
	if (dailyDhA >= 1) { scale = 11.5; } else if (dailyDhA*2 >= 1) { scale = 10.5; } else if (dailyDhA*4 >= 1) { scale = 9.5; } else if (dailyDhA*8 >= 1) { scale = 8.5; } else if (dailyDhA*16 >= 1) { scale = 7.5; } else if (dailyDhA*32 >= 1) { scale = 6.5; } else if (dailyDhA*64 >= 1) { scale = 5.5; } else if (dailyDhA*128 >= 1) { scale = 4.5; } else if (dailyDhA*256 >= 1) { scale = 3.5; } else if (dailyDhA*512 >= 1) { scale = 2.5; } else if (dailyDhA*1024 >= 1) { scale = 1.5; } else { scale = 0.5; }

    // Push data to calendar
    calendarData.entries.push({
        date: page.file.name,
        intensity: scale,//scaledIntensity,
        // color: "heat",
        //content: await dv.span(`[](${page.file.name})`),
    });
}
//renderHeatmapTracker(this.container, calendarData)

// const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData)

// // Adding container for legends and colored boxes on the same line
// const legendsContainer = document.createElement('div');
// legendsContainer.style.display = 'flex';
// legendsContainer.style.alignItems = 'center'; // Align vertically
// legendsContainer.style.justifyContent = 'center'; // Center horizontally 
// legendsContainer.style.width = '100%'; // Ensure it takes full width for centering

// // Adding first legend with reduced size and custom font
// const firstLegend = document.createElement('div');
// firstLegend.innerText = 'Pooooor'; // Updated to "LESS" with all caps
// firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
// firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
// legendsContainer.appendChild(firstLegend);

// // Adding colored boxes with adjusted size
// const legendContainer = document.createElement('div');
// legendContainer.style.display = 'flex';
// legendContainer.style.alignItems = 'center'; // Align vertically

// for (let color of calendarData.colorScheme.heat2) {
//     const colorBox = document.createElement('div');
//     colorBox.style.width = '9px'; // Reduced box width by 50%
//     colorBox.style.height = '9px'; // Reduced box height by 50%
//     colorBox.style.backgroundColor = color;
//     colorBox.style.marginRight = '5px'; // Adjusted margin
//     legendContainer.appendChild(colorBox);
// }

// // Adding second legend after the colored boxes with reduced size and custom font
// const secondLegend = document.createElement('div');
// secondLegend.innerText = 'Riiiiich'; // Updated to "MORE" with all caps
// secondLegend.style.fontSize = '65%'; // Reduce font size by 50%
// secondLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// secondLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// legendContainer.appendChild(secondLegend);

// legendsContainer.appendChild(legendContainer);
// legendsContainer.style.marginBottom = "12px";

// heatmapTrackerEl.appendChild(legendsContainer);

// //dv.span('Money spending tracker statistics:')

const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData);
renderInlineLegend(heatmapTrackerEl, heatmapColors, 'Pooooor', 'Riiiiich');

```
#### 💸 Global wealth (Past) 💸
```dataviewjs
const heatmapColors = [
  "rgb(204, 0, 0)",
  "rgb(255, 0, 0)",
  "rgb(255, 51, 51)",
  "rgb(255, 102, 102)",
  "rgb(255, 153, 153)",
  "rgb(255, 204, 204)",
  "rgb(128, 138, 166)",
  "rgb(77, 90, 128)",
  "rgb(51, 64, 114)",
  "rgb(25, 38, 99)",
  "rgb(0, 18, 77)",
  "rgb(0, 10, 51)"
];

const calendarData = { year: 2026,
    intensityScaleStart: 0,
    intensityScaleEnd: 12, // I have 12 color levels in heat
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "heat2",
//         "heat2": [
//         "rgb(204, 0, 0)",
//         "rgb(255, 0, 0)", 
//         "rgb(255, 51, 51)",
//         "rgb(255, 102, 102)",
//         "rgb(255, 153, 153)",  
//       "rgb(255, 204, 204)",    
//       "rgb(128, 138, 166)",
//       "rgb(77, 90, 128)",
//       "rgb(51, 64, 114)",
//       "rgb(25, 38, 99)",
//       "rgb(0, 18, 77)",
//       "rgb(0, 10, 51)",
//     ],
//     "heat3": [
//     "rgb(204, 0, 0)", 
//     "rgb(170, 20, 20)", 
//     "rgb(140, 35, 35)", 
//     "rgb(110, 45, 45)", 
//     "rgb(80, 50, 50)", 
//     "rgb(51, 51, 51)", 
//     "rgb(50, 55, 75)", 
//     "rgb(40, 45, 90)", 
//     "rgb(30, 35, 100)", 
//     "rgb(15, 20, 80)", 
//     "rgb(5, 15, 60)", 
//     "rgb(0, 10, 51)"
// ]   
    }
};

  function renderInlineLegend(container, colors, minLabel, maxLabel) {
    const legendsContainer = document.createElement('div');
    legendsContainer.style.display = 'flex';
    legendsContainer.style.alignItems = 'center';
    legendsContainer.style.justifyContent = 'center';
    legendsContainer.style.width = '100%';
    legendsContainer.style.marginBottom = '12px';
    legendsContainer.style.gap = '5px';

    const createLabel = (text) => {
      const label = document.createElement('div');
      label.innerText = text;
      label.style.fontSize = '65%';
      label.style.fontFamily = 'IBM plex mono, sans-serif';
      label.style.textTransform = 'uppercase';
      return label;
    };

    legendsContainer.appendChild(createLabel(minLabel));

    const colorsContainer = document.createElement('div');
    colorsContainer.style.display = 'flex';
    colorsContainer.style.alignItems = 'center';
    colorsContainer.style.gap = '5px';

    for (const color of colors) {
      const colorBox = document.createElement('div');
      colorBox.style.width = '9px';
      colorBox.style.height = '9px';
      colorBox.style.backgroundColor = color;
      colorsContainer.appendChild(colorBox);
    }

    legendsContainer.appendChild(colorsContainer);
    legendsContainer.appendChild(createLabel(maxLabel));
    container.appendChild(legendsContainer);
  }

const DAY_MS = 86_400_000;
const Cap = 16500*12*35+16500*5*3+32500;

const PS = dv.date("2014-02-07").startOf("day");
const PE = dv.date("2106-02-07").startOf("day");
const N = PE.diff(PS, "days")/DAY_MS; // total number of days

const minS = 50;       // minimum daily spend
const maxS = 1000;     // maximum daily spend

const daysPerYear = 365.25;
const Y = N/daysPerYear;

const r = Math.pow(maxS / minS, 1 / Y);   // yearly growth rate

// analytic normalization
const totalRaw =
    (daysPerYear * minS / Math.log(r)) *
    (Math.pow(r, N / daysPerYear) - 1);

const K = Cap / totalRaw;

function dailyS(date) {
    const i =
        (date.startOf("day").toMillis() - PS.toMillis()) / DAY_MS;
    if (i < 0 || i >= N) return 0;

    return K * minS * Math.pow(r, i / daysPerYear);
}


function dailySWithOnGoing(date) {
    const i = Math.floor((date.startOf("day").toMillis() - PS.toMillis()) / DAY_MS)+1;
	if (i < 1) return { daily: 10, onGoing: 1 };
    if (i > N) return { daily: maxS, onGoing: 1 };

	const daily = dailyS(date);
	const onGoing = i-1;
	
    return { daily, onGoing };
}

let msg = ''
let moneyInDh = 0;
let dailyPastDh = 0;

// Always normalize to start-of-day to avoid time-of-day drift.
const asDayStart = d => d.startOf('day');
const noteDate = (page) =>
  asDayStart(
    page.date            ? dv.date(page.date) :
    dv.date(page.file.name) ?? dv.date(page.file.cday)
  );
  
// --- state carried across iterations ---
let ctr = 0, ctr_ = 0;
let previousNote = null;     // will hold a dv link to the prior note
let previousDate = null;     // will hold the Luxon DateTime of the prior note

// Dates strictly between a and b (exclusive), 1-day steps
function daysBetweenExclusive(a, b) {
  const out = [];
  let d = a.plus({ days: 1 }).startOf('day');
  const end = b.minus({ days: 1 }).startOf('day');
  while (d <= end) { out.push(d); d = d.plus({ days: 1 }); }
  return out;
}

for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.moneyInDh || p.meTime || p.vOwnerfirstnameOwnerlastname || p.vCjBank2Bank).sort(p => p.file.name, 'asc')) {
    if (!dv.date(page.file.name)) continue;
    // current note’s normalized date
	const currentDate = noteDate(page);
	
	// compute gap in whole days between this and the previous; 0 on the first item
	let numberOfDays = previousDate
	? Math.round((currentDate.toMillis() - previousDate.toMillis()) / DAY_MS)
	: 0;
	
	// “successive” means exactly 1 day after the previous note
	const successive = previousDate ? (numberOfDays === 1) : true;
	
	// days missed are the days strictly between the two notes
	const missedDays = previousDate ? Math.max(numberOfDays - 1, 0) : 0;
	
	// I want to see if the next period using dailyS can be covered with money in dh
	const savedMoney = moneyInDh;
    if (previousNote) {
		//dv.paragraph(`${++ctr}. ${page.file.link} was logged after ${previousNote} by ${numberOfDays} day(s)` + (successive ? `.` : ` — missed ${missedDays}.`));
		if (missedDays > 0) {
		const missing = daysBetweenExclusive(previousDate, currentDate);
		missing.forEach(d => {
			const { daily: dDaily_, onGoing: remDaily_} = dailySWithOnGoing(dv.date(d));
			dailyPastDh +=(dDaily_*missedDays);
			let dailyDhA = savedMoney/dailyPastDh;
			//dv.span(d.toISODate()+"~"+savedMoney+" >"+dDaily_+"_"+remDaily_+"< "+dailyDhA+"</br>"); //check
			let scale; // Extract the date from the filename 
			if (dailyDhA >= 1) { scale = 11.5; } else if (dailyDhA*2 >= 1) { scale = 10.5; } else if (dailyDhA*4 >= 1) { scale = 9.5; } else if (dailyDhA*8 >= 1) { scale = 8.5; } else if (dailyDhA*16 >= 1) { scale = 7.5; } else if (dailyDhA*32 >= 1) { scale = 6.5; } else if (dailyDhA*64 >= 1) { scale = 5.5; } else if (dailyDhA*128 >= 1) { scale = 4.5; } else if (dailyDhA*256 >= 1) { scale = 3.5; } else if (dailyDhA*512 >= 1) { scale = 2.5; } else if (dailyDhA*1024 >= 1) { scale = 1.5; } else { scale = 0.5; }
		
		    // Push data to calendar
		    calendarData.entries.push({
		        date: d.toISODate(),
		        intensity: scale,
		        // color: "heat",
		    });
	});
		}
	}
	
	// retrieve the daily money
    moneyInDh += ((page.moneyInDh || 0) + (page.vCDBalance||0) + (page.vCjBank2Bank||0));
	
	// --- update carried state so the next iteration “knows” the previous note ---
	previousNote = page.file.link;   // this is how you “add” previousNote for the next loop
	previousDate = currentDate;      // needed to compute the next numberOfDays 

    
    // Extract the date from the filename
    const pageDate = dv.date(page.file.name).startOf("day");

	//Get averge that should be expected
    const { daily: dDaily, onGoing: remDaily} = dailySWithOnGoing(pageDate);
	dailyPastDh += dDaily;
	let dailyDhA = moneyInDh/dailyPastDh;
	let scale; // Extract the date from the filename 
	if (dailyDhA >= 1) { scale = 11.5; } else if (dailyDhA*2 >= 1) { scale = 10.5; } else if (dailyDhA*4 >= 1) { scale = 9.5; } else if (dailyDhA*8 >= 1) { scale = 8.5; } else if (dailyDhA*16 >= 1) { scale = 7.5; } else if (dailyDhA*32 >= 1) { scale = 6.5; } else if (dailyDhA*64 >= 1) { scale = 5.5; } else if (dailyDhA*128 >= 1) { scale = 4.5; } else if (dailyDhA*256 >= 1) { scale = 3.5; } else if (dailyDhA*512 >= 1) { scale = 2.5; } else if (dailyDhA*1024 >= 1) { scale = 1.5; } else { scale = 0.5; }

    // Push data to calendar
    calendarData.entries.push({
        date: page.file.name,
        intensity: scale,//scaledIntensity,
        // color: "heat",
        //content: await dv.span(`[](${page.file.name})`),
    });
}
//renderHeatmapTracker(this.container, calendarData)

// const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData)

// // Adding container for legends and colored boxes on the same line
// const legendsContainer = document.createElement('div');
// legendsContainer.style.display = 'flex';
// legendsContainer.style.alignItems = 'center'; // Align vertically
// legendsContainer.style.justifyContent = 'center'; // Center horizontally 
// legendsContainer.style.width = '100%'; // Ensure it takes full width for centering

// // Adding first legend with reduced size and custom font
// const firstLegend = document.createElement('div');
// firstLegend.innerText = 'Pooooor'; // Updated to "LESS" with all caps
// firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
// firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
// legendsContainer.appendChild(firstLegend);

// // Adding colored boxes with adjusted size
// const legendContainer = document.createElement('div');
// legendContainer.style.display = 'flex';
// legendContainer.style.alignItems = 'center'; // Align vertically

// for (let color of calendarData.colorScheme.heat2) {
//     const colorBox = document.createElement('div');
//     colorBox.style.width = '9px'; // Reduced box width by 50%
//     colorBox.style.height = '9px'; // Reduced box height by 50%
//     colorBox.style.backgroundColor = color;
//     colorBox.style.marginRight = '5px'; // Adjusted margin
//     legendContainer.appendChild(colorBox);
// }

// // Adding second legend after the colored boxes with reduced size and custom font
// const secondLegend = document.createElement('div');
// secondLegend.innerText = 'Riiiiich'; // Updated to "MORE" with all caps
// secondLegend.style.fontSize = '65%'; // Reduce font size by 50%
// secondLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// secondLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// legendContainer.appendChild(secondLegend);

// legendsContainer.appendChild(legendContainer);
// legendsContainer.style.marginBottom = "12px";

// heatmapTrackerEl.appendChild(legendsContainer);

// dv.span('Money spending tracker statistics:')

const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData);
renderInlineLegend(heatmapTrackerEl, heatmapColors, 'Pooooor', 'Riiiiich');

```
#### 💰 Global transactions 💰
##### V1
```dataviewjs
const heatmapColors = [
  "rgb(204, 0, 0)",
  "rgb(255, 0, 0)",
  "rgb(255, 51, 51)",
  "rgb(255, 102, 102)",
  "rgb(255, 153, 153)",
  "rgb(255, 204, 204)",
  "rgb(128, 138, 166)",
  "rgb(77, 90, 128)",
  "rgb(51, 64, 114)",
  "rgb(25, 38, 99)",
  "rgb(0, 18, 77)",
  "rgb(0, 10, 51)"
];

const calendarData = { year: 2026,
    intensityScaleStart: 0,
    intensityScaleEnd: 12, // I have 12 color levels in heat
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "heat2",
//         "heat2": [
//         "rgb(204, 0, 0)",
//         "rgb(255, 0, 0)", 
//         "rgb(255, 51, 51)",
//         "rgb(255, 102, 102)",
//         "rgb(255, 153, 153)",  
//       "rgb(255, 204, 204)",    
//       "rgb(128, 138, 166)",
//       "rgb(77, 90, 128)",
//       "rgb(51, 64, 114)",
//       "rgb(25, 38, 99)",
//       "rgb(0, 18, 77)",
//       "rgb(0, 10, 51)",
//     ],
//     "heat3": [
//     "rgb(204, 0, 0)", 
//     "rgb(170, 20, 20)", 
//     "rgb(140, 35, 35)", 
//     "rgb(110, 45, 45)", 
//     "rgb(80, 50, 50)", 
//     "rgb(51, 51, 51)", 
//     "rgb(50, 55, 75)", 
//     "rgb(40, 45, 90)", 
//     "rgb(30, 35, 100)", 
//     "rgb(15, 20, 80)", 
//     "rgb(5, 15, 60)", 
//     "rgb(0, 10, 51)"
// ]   
    }
};

  function renderInlineLegend(container, colors, minLabel, maxLabel) {
    const legendsContainer = document.createElement('div');
    legendsContainer.style.display = 'flex';
    legendsContainer.style.alignItems = 'center';
    legendsContainer.style.justifyContent = 'center';
    legendsContainer.style.width = '100%';
    legendsContainer.style.marginBottom = '12px';
    legendsContainer.style.gap = '5px';

    const createLabel = (text) => {
      const label = document.createElement('div');
      label.innerText = text;
      label.style.fontSize = '65%';
      label.style.fontFamily = 'IBM plex mono, sans-serif';
      label.style.textTransform = 'uppercase';
      return label;
    };

    legendsContainer.appendChild(createLabel(minLabel));

    const colorsContainer = document.createElement('div');
    colorsContainer.style.display = 'flex';
    colorsContainer.style.alignItems = 'center';
    colorsContainer.style.gap = '5px';

    for (const color of colors) {
      const colorBox = document.createElement('div');
      colorBox.style.width = '9px';
      colorBox.style.height = '9px';
      colorBox.style.backgroundColor = color;
      colorsContainer.appendChild(colorBox);
    }

    legendsContainer.appendChild(colorsContainer);
    legendsContainer.appendChild(createLabel(maxLabel));
    container.appendChild(legendsContainer);
  }

const DAY_MS = 86_400_000;
const Cap = 16500*12*35+16500*5*3+32500;

const PS = dv.date("2014-02-07").startOf("day");
const PE = dv.date("2106-02-07").startOf("day");
const N = PE.diff(PS, "days")/DAY_MS; // total number of days

const minS = 50;       // minimum daily spend
const maxS = 1000;     // maximum daily spend

const daysPerYear = 365.25;
const Y = N/daysPerYear;

const r = Math.pow(maxS / minS, 1 / Y);   // yearly growth rate

// analytic normalization
const totalRaw =
    (daysPerYear * minS / Math.log(r)) *
    (Math.pow(r, N / daysPerYear) - 1);

const K = Cap / totalRaw;

function dailyS(date) {
    const i =
        (date.startOf("day").toMillis() - PS.toMillis()) / DAY_MS;
    if (i < 0 || i >= N) return 0;

    return K * minS * Math.pow(r, i / daysPerYear);
}


function dailySWithOnGoing(date) {
    const i = Math.floor((date.startOf("day").toMillis() - PS.toMillis()) / DAY_MS)+1;
	if (i < 1) return { daily: 10, onGoing: 1 };
    if (i > N) return { daily: maxS, onGoing: N };

	const daily = dailyS(date);
	const onGoing = i-1;
	
    return { daily, onGoing };
}

let msg = ''
let moneyInDhP = 0;
let moneyInDhN = 0;
let moneyInDh_ = 0;

// Always normalize to start-of-day to avoid time-of-day drift.
const asDayStart = d => d.startOf('day');
const noteDate = (page) =>
  asDayStart(
    page.date            ? dv.date(page.date) :
    dv.date(page.file.name) ?? dv.date(page.file.cday)
  );  


// --- Pass 1: compute all dailyDhA values ---
const collected = [];
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.moneyInDh || p.meTime || p.vOwnerfirstnameOwnerlastname || p.vCjBank2Bank).sort(p => p.file.name, 'asc')) {
    if (!dv.date(page.file.name)) continue;
    const pageDate = dv.date(page.file.name).startOf("day");

    const { daily: dDaily, onGoing: remDaily} = dailySWithOnGoing(pageDate);
    moneyInDhP += (page.moneyInDh || 0)>=0?(page.moneyInDh || 0):0;
    moneyInDhN += (page.moneyInDh || 0)>=0?0:(page.moneyInDh || 0);
	moneyInDh_ += ((page.vCDBalance||0) + (page.vCjBank2Bank||0));

	let dailyDhA = ((moneyInDhP - moneyInDhN + moneyInDh_)/(2*(Cap/N)*remDaily))/dDaily;
	// let dailyDhA = ((moneyInDhP - moneyInDhN)*N/(2*Cap))/remDaily;

    collected.push({ date: page.file.name, value: dailyDhA });
}

// --- Build percentile thresholds for 12 color levels ---
const positives = collected.map(e => e.value).filter(v => v > 0).sort((a, b) => a - b);
const thresholds = [];
for (let i = 1; i < 12; i++) {
    const idx = Math.min(Math.floor(i * positives.length / 12), positives.length - 1);
    thresholds.push(positives[idx]);
}

// --- Pass 2: map each entry to its color level ---
for (const { date, value } of collected) {
    let scale = 0.5;
    if (value > 0) {
        for (let t = 0; t < thresholds.length; t++) {
            if (value >= thresholds[t]) scale = t + 1.5;
            else break;
        }
    }
    calendarData.entries.push({
        date: date,
        intensity: scale,
        // color: "heat",
    });
}

// const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData)

// // Adding container for legends and colored boxes on the same line
// const legendsContainer = document.createElement('div');
// legendsContainer.style.display = 'flex';
// legendsContainer.style.alignItems = 'center'; // Align vertically
// legendsContainer.style.justifyContent = 'center'; // Center horizontally 
// legendsContainer.style.width = '100%'; // Ensure it takes full width for centering

// // Adding first legend with reduced size and custom font
// const firstLegend = document.createElement('div');
// firstLegend.innerText = 'Careful'; // Updated to "LESS" with all caps
// firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
// firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
// legendsContainer.appendChild(firstLegend);

// // Adding colored boxes with adjusted size
// const legendContainer = document.createElement('div');
// legendContainer.style.display = 'flex';
// legendContainer.style.alignItems = 'center'; // Align vertically

// for (let color of calendarData.colorScheme.heat2) {
//     const colorBox = document.createElement('div');
//     colorBox.style.width = '9px'; // Reduced box width by 50%
//     colorBox.style.height = '9px'; // Reduced box height by 50%
//     colorBox.style.backgroundColor = color;
//     colorBox.style.marginRight = '5px'; // Adjusted margin
//     legendContainer.appendChild(colorBox);
// }

// // Adding second legend after the colored boxes with reduced size and custom font
// const secondLegend = document.createElement('div');
// secondLegend.innerText = 'No worries'; // Updated to "MORE" with all caps
// secondLegend.style.fontSize = '65%'; // Reduce font size by 50%
// secondLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// secondLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// legendContainer.appendChild(secondLegend);

// legendsContainer.appendChild(legendContainer);
// legendsContainer.style.marginBottom = "12px";

// heatmapTrackerEl.appendChild(legendsContainer);

// dv.span('Money spending tracker statistics:')

const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData);
renderInlineLegend(heatmapTrackerEl, heatmapColors, 'Careful', 'No worries');

```
##### V2
```dataviewjs
/* ============================================================
   LIFE-CYCLE SPENDING HEATMAP — FINAL DEFINITIVE VERSION
   ============================================================ */

const calendarData = { year: 2026,
    intensityScaleStart: 0,
  intensityScaleEnd: 12,
  entries: [],
  separateMonths: true,
  colorScheme: {
    paletteName: "heat2",
    // heat2: [
    //   "rgb(204, 0, 0)",
    //   "rgb(255, 0, 0)",
    //   "rgb(255, 51, 51)",
    //   "rgb(255, 102, 102)",
    //   "rgb(255, 153, 153)",
    //   "rgb(255, 204, 204)",
    //   "rgb(128, 138, 166)",
    //   "rgb(77, 90, 128)",
    //   "rgb(51, 64, 114)",
    //   "rgb(25, 38, 99)",
    //   "rgb(0, 18, 77)",
    //   "rgb(0, 10, 51)"
    // ]
  }
};

const heatmapColors = [
  "rgb(204, 0, 0)",
  "rgb(255, 0, 0)",
  "rgb(255, 51, 51)",
  "rgb(255, 102, 102)",
  "rgb(255, 153, 153)",
  "rgb(255, 204, 204)",
  "rgb(128, 138, 166)",
  "rgb(77, 90, 128)",
  "rgb(51, 64, 114)",
  "rgb(25, 38, 99)",
  "rgb(0, 18, 77)",
  "rgb(0, 10, 51)"
];

function renderInlineLegend(container, colors, minLabel, maxLabel) {
  const legendsContainer = document.createElement('div');
  legendsContainer.style.display = 'flex';
  legendsContainer.style.alignItems = 'center';
  legendsContainer.style.justifyContent = 'center';
  legendsContainer.style.width = '100%';
  legendsContainer.style.marginBottom = '12px';
  legendsContainer.style.gap = '5px';

  const createLabel = (text) => {
    const label = document.createElement('div');
    label.innerText = text;
    label.style.fontSize = '65%';
    label.style.fontFamily = 'IBM plex mono, sans-serif';
    label.style.textTransform = 'uppercase';
    return label;
  };

  legendsContainer.appendChild(createLabel(minLabel));

  const colorsContainer = document.createElement('div');
  colorsContainer.style.display = 'flex';
  colorsContainer.style.alignItems = 'center';
  colorsContainer.style.gap = '5px';

  for (const color of colors) {
    const colorBox = document.createElement('div');
    colorBox.style.width = '9px';
    colorBox.style.height = '9px';
    colorBox.style.backgroundColor = color;
    colorsContainer.appendChild(colorBox);
  }

  legendsContainer.appendChild(colorsContainer);
  legendsContainer.appendChild(createLabel(maxLabel));
  container.appendChild(legendsContainer);
}

/* -------------------- CONSTANTS -------------------- */
const DAY_MS = 86_400_000;
const daysPerYear = 365.25;

const Cap = 16500*12*35 + 16500*5*3 + 32500;

const PS = dv.date("2014-02-07").startOf("day");
const PE = dv.date("2106-02-07").startOf("day");

const N = PE.diff(PS, "days") / DAY_MS;
const Y = N / daysPerYear;

const minS = 50;
const maxS = 1000;

/* -------------------- EXPECTED DAILY MODEL -------------------- */
const r = Math.pow(maxS / minS, 1 / Y);

const totalRaw =
  (daysPerYear * minS / Math.log(r)) *
  (Math.pow(r, N / daysPerYear) - 1);

const K = Cap / totalRaw;

function expectedDaily(date) {
  const t = ((date.startOf("day").toMillis() - PS.toMillis()) / DAY_MS)||0;
  if (t < 0 || t > N) return 0;
  return K * minS * Math.pow(r, t / daysPerYear);
}

/* -------------------- ROLLING WINDOW -------------------- */
const LAG = 30;
const ring = new Array(LAG).fill(0);
let size = 0, head = 0;

function push(v) {
  if (size < LAG) {
    ring[(head + size) % LAG] = v;
    size++;
  } else {
    ring[head] = v;
    head = (head + 1) % LAG;
  }
}

function avg() {
  if (!size) return 0;
  let s = 0;
  for (let i = 0; i < size; i++)
    s += ring[(head + i) % LAG];
  return s / size;
}

/* -------------------- HEAT SCALING -------------------- */
function heat(actual, expected) {
  if (expected <= 0) return 6;
  const h = Math.log2(actual / expected);
  const c = Math.max(-3, Math.min(3, h));
  return Math.round((c + 3) * 2);
}

/* -------------------- DATE HANDLING -------------------- */
const day = d => d.startOf("day");
const noteDate = p =>
  day(p.date ? dv.date(p.date) : dv.date(p.file.name) ?? dv.date(p.file.cday));

/* -------------------- LOAD PAGES -------------------- */
const pages = dv.pages('"00 - Main vault/Notes/Daily Notes"')
  .where(p => (p.moneyInDh || p.vCDBalance || p.vCjBank2Bank) && dv.date(p.file.name))
  .sort(p => p.file.name, 'asc');

/* -------------------- MAIN LOOP -------------------- */
let currentDate = noteDate(pages[0]);
let lastDate    = noteDate(pages[pages.length - 1]);

let pageIndex = 0;

while (currentDate <= lastDate) {
  let actual;

  if (
    pageIndex < pages.length &&
    noteDate(pages[pageIndex]).toISODate() === currentDate.toISODate()
  ) {
    const p = pages[pageIndex];
    actual =
      (Number(p.moneyInDh) || 0) +
      (Number(p.vCDBalance) || 0) +
      (Number(p.vCjBank2Bank) || 0);
    pageIndex++;
  } else {
    /* ----- ESTIMATED DAY ----- */
    actual = expectedDaily(currentDate);
  }

  push(actual);

  calendarData.entries.push({
    date: currentDate.toISODate(),
    intensity: heat(avg(), expectedDaily(currentDate)),
    // color: "heat"
  });

  currentDate = currentDate.plus({ days: 1 });
}

// /* -------------------- RENDER -------------------- */
// const el = renderHeatmapTracker(this.container, calendarData);

// /* -------------------- LEGEND -------------------- */
// const legend = document.createElement("div");
// legend.style.display = "flex";
// legend.style.justifyContent = "center";
// legend.style.alignItems = "center";
// legend.style.marginBottom = "12px";
// legend.style.fontSize = "65%";
// legend.style.fontFamily = "IBM Plex Mono, sans-serif";
// legend.style.textTransform = "uppercase";

// legend.append("Overspending ");

// for (const c of calendarData.colorScheme.heat2) {
//   const b = document.createElement("div");
//   b.style.width = "9px";
//   b.style.height = "9px";
//   b.style.background = c;
//   b.style.margin = "0 3px";
//   legend.appendChild(b);
// }

// legend.append(" Underspending");
// el.appendChild(legend);

// dv.span("Money spending tracker statistics:");
const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData);
renderInlineLegend(heatmapTrackerEl, heatmapColors, 'Overspending', 'Underspending');

```
#### 🏦 Daily transactions 🏦
```dataviewjs
const heatmapColors = [
  "rgb(204, 0, 0)",
  "rgb(170, 20, 20)",
  "rgb(140, 35, 35)",
  "rgb(110, 45, 45)",
  "rgb(80, 50, 50)",
  "rgb(51, 51, 51)",
  "rgb(50, 55, 75)",
  "rgb(40, 45, 90)",
  "rgb(30, 35, 100)",
  "rgb(15, 20, 80)",
  "rgb(5, 15, 60)",
  "rgb(0, 10, 51)"
];

const calendarData = { year: 2026,
    intensityScaleStart: 0,
    intensityScaleEnd: 12, // I have 12 color levels in heat
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "heat3",
//         "heat2": [
//         "rgb(204, 0, 0)",
//         "rgb(255, 0, 0)", 
//         "rgb(255, 51, 51)",
//         "rgb(255, 102, 102)",
//         "rgb(255, 153, 153)",  
//       "rgb(255, 204, 204)",    
//       "rgb(128, 138, 166)",
//       "rgb(77, 90, 128)",
//       "rgb(51, 64, 114)",
//       "rgb(25, 38, 99)",
//       "rgb(0, 18, 77)",
//       "rgb(0, 10, 51)",
//     ],
//     "heat3": [
//     "rgb(204, 0, 0)", 
//     "rgb(170, 20, 20)", 
//     "rgb(140, 35, 35)", 
//     "rgb(110, 45, 45)", 
//     "rgb(80, 50, 50)", 
//     "rgb(51, 51, 51)", 
//     "rgb(50, 55, 75)", 
//     "rgb(40, 45, 90)", 
//     "rgb(30, 35, 100)", 
//     "rgb(15, 20, 80)", 
//     "rgb(5, 15, 60)", 
//     "rgb(0, 10, 51)"
// ]   
    }
};

  function renderInlineLegend(container, colors, minLabel, maxLabel) {
    const legendsContainer = document.createElement('div');
    legendsContainer.style.display = 'flex';
    legendsContainer.style.alignItems = 'center';
    legendsContainer.style.justifyContent = 'center';
    legendsContainer.style.width = '100%';
    legendsContainer.style.marginBottom = '12px';
    legendsContainer.style.gap = '5px';

    const createLabel = (text) => {
      const label = document.createElement('div');
      label.innerText = text;
      label.style.fontSize = '65%';
      label.style.fontFamily = 'IBM plex mono, sans-serif';
      label.style.textTransform = 'uppercase';
      return label;
    };

    legendsContainer.appendChild(createLabel(minLabel));

    const colorsContainer = document.createElement('div');
    colorsContainer.style.display = 'flex';
    colorsContainer.style.alignItems = 'center';
    colorsContainer.style.gap = '5px';

    for (const color of colors) {
      const colorBox = document.createElement('div');
      colorBox.style.width = '9px';
      colorBox.style.height = '9px';
      colorBox.style.backgroundColor = color;
      colorsContainer.appendChild(colorBox);
    }

    legendsContainer.appendChild(colorsContainer);
    legendsContainer.appendChild(createLabel(maxLabel));
    container.appendChild(legendsContainer);
  }
const SDaily = 69; //The minimum money to fully survive a day

//Function to calculate intensity
function scaleIntensity(money) {
    if (money === 0) return 6; // normal values
    if (money <= 0) return (-money>6)?0:6+money; // I'm in dept 
    if (money > 0) return (money>6)?12:7+money; // saving money
}

let moneyInDh = 0; //current money in vault
let pMoneyInDh = 0;   // cumulative sum 30 entries ago
let pMoneyInDh_ = 0;   // cumulative sum 30 entries ago

const LAG = 31;
const DAY_MS = 86_400_000;
const ring = new Array(LAG);
let size = 0;   // how many cells filled (<= LAG)
let head = 0;   // index of the oldest value

// Always normalize to start-of-day to avoid time-of-day drift.
const asDayStart = d => d.startOf('day');
const noteDate = (page) =>
  asDayStart(
    page.date            ? dv.date(page.date) :
    dv.date(page.file.name) ?? dv.date(page.file.cday)
  );

// --- state carried across iterations ---
let ctr = 0, ctr_ = 0;
let previousNote = null;     // will hold a dv link to the prior note
let previousDate = null;     // will hold the Luxon DateTime of the prior note

// Dates strictly between a and b (exclusive), 1-day steps
function daysBetweenExclusive(a, b) {
  const out = [];
  let d = a.plus({ days: 1 }).startOf('day');
  const end = b.minus({ days: 1 }).startOf('day');
  while (d <= end) { out.push(d); d = d.plus({ days: 1 }); }
  return out;
}

for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.moneyInDh || p.meTime || p.vOwnerfirstnameOwnerlastname || p.vCjBank2Bank).sort(p => p.file.name, 'asc')) {
    if (!dv.date(page.file.name)) continue;
    // current note’s normalized date
	const currentDate = noteDate(page);
	
	// compute gap in whole days between this and the previous; 0 on the first item
	let numberOfDays = previousDate
	? Math.round((currentDate.toMillis() - previousDate.toMillis()) / DAY_MS)
	: 0;
	
	// “successive” means exactly 1 day after the previous note
	const successive = previousDate ? (numberOfDays === 1) : true;
	
	// days missed are the days strictly between the two notes
	const missedDays = previousDate ? Math.max(numberOfDays - 1, 0) : 0;
	
	// print the line you asked for (handle the first entry cleanly)
	if (previousNote) {
		//dv.paragraph(`${++ctr}. ${page.file.link} was logged after ${previousNote} by ${numberOfDays} day(s)` + (successive ? `.` : ` — missed ${missedDays}.`));
		if (missedDays > 0) {
		const missing = daysBetweenExclusive(previousDate, currentDate);
		missing.forEach(d => {
			if (size > 0){
				pMoneyInDh_ = (ring[(head-1)<0?((LAG-1)% LAG):(head-1)%LAG])||0;
			}
			if (size < LAG) {
				ring[(head + size) % LAG] = moneyInDh; // append
				size++;
				pMoneyInDh = 0; // first 30 → 0
			} else {
				pMoneyInDh = ring[head];               // 30 entries ago
				ring[head] = moneyInDh;                // overwrite oldest with current
				head = (head + 1) % LAG;               // advance oldest pointer
			}
			calendarData.entries.push({
		        date: d.toISODate(),
		        intensity: scaleIntensity(((pMoneyInDh_ - pMoneyInDh)/30)/SDaily),
		        // color: "heat",
		    });
		});
		}
	}
	
	// --- update carried state so the next iteration “knows” the previous note ---
	previousNote = page.file.link;   // this is how you “add” previousNote for the next loop
	previousDate = currentDate;      // needed to compute the next numberOfDays
	
    // retrieve the daily money
	let moneyInDh_ = ((Number(page.moneyInDh) || 0) + (page.vCDBalance||0) + (page.vCjBank2Bank||0)); // update cumulative
    moneyInDh += moneyInDh_; // update cumulative
	if (size > 0){
		pMoneyInDh_ = (ring[(head-1)<0?((LAG-1)% LAG):(head-1)%LAG])||0;
	}
	if (size < LAG) {
		ring[(head + size) % LAG] = moneyInDh; // append
		size++;
		pMoneyInDh = 0; // first 30 → 0
	} else {
		pMoneyInDh = ring[head];               // 30 entries ago
		ring[head] = moneyInDh;                // overwrite oldest with current
		head = (head + 1) % LAG;               // advance oldest pointer
	}
	
	let dailyDh = (pMoneyInDh_ - pMoneyInDh)/30;
	
	// Compute intensity
    let scaledIntensity = scaleIntensity((moneyInDh_ + (dailyDh))/SDaily);
	
	// Example output per day:
	//dv.paragraph(`${page.file.name}: today ${moneyInDh_.toFixed(2)}, accumulative = ${moneyInDh.toFixed(2)}, 1day ago = ${pMoneyInDh_}, 30d ago = ${pMoneyInDh.toFixed(2)}, daily = ${dailyDh.toFixed(2)} => ${scaledIntensity}`);
    
    // Push data to calendar
    calendarData.entries.push({
        date: page.file.name,
        intensity: scaledIntensity,
        // color: "heat",
        //content: await dv.span(`[](${page.file.name})`),
    });
}
//renderHeatmapTracker(this.container, calendarData)

// const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData)

// // Adding container for legends and colored boxes on the same line
// const legendsContainer = document.createElement('div');
// legendsContainer.style.display = 'flex';
// legendsContainer.style.alignItems = 'center'; // Align vertically
// legendsContainer.style.justifyContent = 'center'; // Center horizontally 
// legendsContainer.style.width = '100%'; // Ensure it takes full width for centering

// // Adding first legend with reduced size and custom font
// const firstLegend = document.createElement('div');
// firstLegend.innerText = 'Spending ...'; // Updated to "LESS" with all caps
// firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
// firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
// legendsContainer.appendChild(firstLegend);

// // Adding colored boxes with adjusted size
// const legendContainer = document.createElement('div');
// legendContainer.style.display = 'flex';
// legendContainer.style.alignItems = 'center'; // Align vertically

// for (let color of calendarData.colorScheme.heat3) {
//     const colorBox = document.createElement('div');
//     colorBox.style.width = '9px'; // Reduced box width by 50%
//     colorBox.style.height = '9px'; // Reduced box height by 50%
//     colorBox.style.backgroundColor = color;
//     colorBox.style.marginRight = '5px'; // Adjusted margin
//     legendContainer.appendChild(colorBox);
// }

// // Adding second legend after the colored boxes with reduced size and custom font
// const secondLegend = document.createElement('div');
// secondLegend.innerText = '... Saving'; // Updated to "MORE" with all caps
// secondLegend.style.fontSize = '65%'; // Reduce font size by 50%
// secondLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// secondLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// legendContainer.appendChild(secondLegend);

// legendsContainer.appendChild(legendContainer);
// legendsContainer.style.marginBottom = "12px";

// heatmapTrackerEl.appendChild(legendsContainer);

//dv.span('Money spending tracker statistics:')

const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData)
renderInlineLegend(heatmapTrackerEl, heatmapColors, 'Spending ...', '... Saving')

//dv.span(msg)

```

#### 
![[Financial Records#💸 Money Log 💰]]