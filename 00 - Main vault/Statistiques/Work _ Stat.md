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

### ** 👨‍🏫 Work 👨‍💼**
#### Total (In terms of work hours)
```dataviewjs
const heatmapColors = [
  "rgb(230, 221, 217)",
  "rgb(204, 188, 179)",
  "rgb(179, 157, 140)",
  "rgb(153, 127, 102)",
  "rgb(128, 103, 80)",
  "rgb(114, 85, 51)",
  "rgb(99, 67, 26)",
  "rgb(75, 47, 1)",
  "rgb(51, 33, 0)",
  "rgb(26, 16, 0)"
];

const calendarData = { year: 2026,
    intensityScaleStart: 0,
    intensityScaleEnd: 10, // I have 10 color levels in heat
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "metime",
//         "metime": [
//       "rgb(230, 221, 217)",
//       "rgb(204, 188, 179)",
//       "rgb(179, 157, 140)",
//       "rgb(153, 127, 102)",
//       "rgb(128, 103, 80)",
//       "rgb(114, 85, 51)",
//       "rgb(99, 67, 26)",
//       "rgb(75, 47, 1)",
//       "rgb(51, 33, 0)",
//       "rgb(26, 16, 0)"
//     ],
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

function scaleIntensity(intensity,maxDay) {
    if (intensity < maxDay) {
        return Math.floor((intensity / maxDay) * 9); // Scale to 0-9
    } else {
        return 10; // Assign 6 if intensity is maxDay or greater
    }
};
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.hWork || p.oWork || p.rWork || p.sWork || p.pWork || p.tWork || p.mWork || p.eWork)) {
	let workHH = (page.hWork||0) + (page.oWork||0) + (page.tWork||0) + (page.mWork||0) + (page.rWork||0) + (page.pWork||0) + (page.sWork||0)+ (page.eWork||0);
	if (workHH === 0) {continue;}
	//dv.span(workHH+' On '+ page.file.name + '<br>')
	let scaledIntensity = scaleIntensity(Math.abs(workHH),12*60) +1; //12h is daily working hours
	//dv.span(`${page.file.name} : ${workHH} =>${scaledIntensity}</br>`);
    calendarData.entries.push({
        date: page.file.name,
        intensity: scaledIntensity, // Use scaled intensity
//         color:"metime",
        //content: await dv.span(`[](${page.file.name})`), // For hover preview
    });
}
// renderHeatmapTracker(this.container, calendarData)

// const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData)

// // Adding container for legends and colored boxes on the same line
// const legendsContainer = document.createElement('div');
// legendsContainer.style.display = 'flex';
// legendsContainer.style.alignItems = 'center'; // Align vertically
// legendsContainer.style.justifyContent = 'center'; // Center horizontally 
// legendsContainer.style.width = '100%'; // Ensure it takes full width for centering

// // Adding first legend with reduced size and custom font
// const firstLegend = document.createElement('div');
// firstLegend.innerText = 'Less'; // Updated to "LESS" with all caps
// firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
// firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
// legendsContainer.appendChild(firstLegend);

// // Adding colored boxes with adjusted size
// const legendContainer = document.createElement('div');
// legendContainer.style.display = 'flex';
// legendContainer.style.alignItems = 'center'; // Align vertically

// for (let color of calendarData.colorScheme.metime) {
//     const colorBox = document.createElement('div');
//     colorBox.style.width = '9px'; // Reduced box width by 50%
//     colorBox.style.height = '9px'; // Reduced box height by 50%
//     colorBox.style.backgroundColor = color;
//     colorBox.style.marginRight = '5px'; // Adjusted margin
//     legendContainer.appendChild(colorBox);
// }

// // Adding second legend after the colored boxes with reduced size and custom font
// const secondLegend = document.createElement('div');
// secondLegend.innerText = 'More'; // Updated to "MORE" with all caps
// secondLegend.style.fontSize = '65%'; // Reduce font size by 50%
// secondLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// secondLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// legendContainer.appendChild(secondLegend);

// legendsContainer.appendChild(legendContainer);
// legendsContainer.style.marginBottom = "12px";

// heatmapTrackerEl.appendChild(legendsContainer);

// dv.span('Working tracker statistics:')

const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData)
renderInlineLegend(heatmapTrackerEl, heatmapColors, 'Less', 'More')
```

#### Total (In terms of Wage)
```dataviewjs
const heatmapColors = [
  "rgb(128, 138, 166)",
  "rgb(77, 90, 128)",
  "rgb(51, 64, 114)",
  "rgb(25, 38, 99)",
  "rgb(0, 18, 77)",
  "rgb(0, 10, 51)"
];

const calendarData = { year: 2026,
    intensityScaleStart: 0,
    intensityScaleEnd: 10, // I have 12 color levels in heat
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "work",
//         "metime": [
//       "rgb(230, 221, 217)",
//       "rgb(204, 188, 179)",
//       "rgb(179, 157, 140)",
//       "rgb(153, 127, 102)",
//       "rgb(128, 103, 80)",
//       "rgb(114, 85, 51)",
//       "rgb(99, 67, 26)",
//       "rgb(75, 47, 1)",
//       "rgb(51, 33, 0)",
//       "rgb(26, 16, 0)"
// 	    ],
// 	    "work": [
// 	      "rgb(128, 138, 166)",
// 	      "rgb(77, 90, 128)",
// 	      "rgb(51, 64, 114)",
// 	      "rgb(25, 38, 99)",
// 	      "rgb(0, 18, 77)",
// 	      "rgb(0, 10, 51)"
// 	    ]
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

function scaleIntensity(intensity,maxDay) {
    if (intensity < maxDay) {
        return Math.floor((intensity / maxDay) * 9); // Scale to 0-6
    } else {
        return 10; // Assign 6 if intensity is maxDay or greater
    }
};
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.hWork || p.oWork || p.rWork || p.sWork || p.pWork || p.tWork || p.mWork || p.eWork)) {
	let workDh = ((page.hWork||0)*Math.abs(page.hWorkDh||0) + (page.oWork||0)*Math.abs(page.oWorkDh||70) + (page.tWork||0)*Math.abs(page.tWorkDh||0) +  (page.eWork||0)*Math.abs(page.eWorkDh||0) + (page.mWork||0)*Math.abs(page.mWorkDh||0) + (page.rWork||0)*Math.abs(page.rWorkDh||0) + (page.pWork||0)*Math.abs(page.pWorkDh||0) + (page.sWork||0)*Math.abs(page.sWorkDh||0))/60;
	if (workDh === 0) {continue;}
	//dv.span(workHH+' On '+ page.file.name + '<br>')
	let scaledIntensity = scaleIntensity(Math.abs(workDh),200*10) +1; //500 is daily salery
    calendarData.entries.push({
        date: page.file.name,
        intensity: scaledIntensity, // Use scaled intensity
//         color:"work",
        //content: await dv.span(`[](${page.file.name})`), // For hover preview
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
// firstLegend.innerText = 'Minimum'; // Updated to "LESS" with all caps
// firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
// firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
// legendsContainer.appendChild(firstLegend);

// // Adding colored boxes with adjusted size
// const legendContainer = document.createElement('div');
// legendContainer.style.display = 'flex';
// legendContainer.style.alignItems = 'center'; // Align vertically

// for (let color of calendarData.colorScheme.work) {
//     const colorBox = document.createElement('div');
//     colorBox.style.width = '9px'; // Reduced box width by 50%
//     colorBox.style.height = '9px'; // Reduced box height by 50%
//     colorBox.style.backgroundColor = color;
//     colorBox.style.marginRight = '5px'; // Adjusted margin
//     legendContainer.appendChild(colorBox);
// }

// // Adding second legend after the colored boxes with reduced size and custom font
// const secondLegend = document.createElement('div');
// secondLegend.innerText = 'Worth it'; // Updated to "MORE" with all caps
// secondLegend.style.fontSize = '65%'; // Reduce font size by 50%
// secondLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// secondLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// legendContainer.appendChild(secondLegend);

// legendsContainer.appendChild(legendContainer);
// legendsContainer.style.marginBottom = "12px";

// heatmapTrackerEl.appendChild(legendsContainer);

// dv.span('Working tracker statistics:')

const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData)
renderInlineLegend(heatmapTrackerEl, heatmapColors, 'Minimum', 'Worth it')
```
#### Global statistiques 
##### Time management
```tracker
searchType: dvField
searchTarget: hWork, oWork, rWork, sWork, tWork, pWork, mWork, eWork
datasetName: hWork, oWork, rWork, sWork, tWork, pWork, mWork, eWork
fitPanelWidth: true
aspectRatio: 1
folder: "00 - Main vault/Notes/Daily Notes"

pie:
    title: Time management
    label: '{{(sum(dataset(4))+sum(dataset(6))+sum(dataset(7)))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}}%,    {{sum(dataset(2))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}}%,    {{sum(dataset(3))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}}%,    {{sum(dataset(5))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}}%,    {{sum(dataset(1))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}}%,{{sum(dataset(0))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}}%,{{(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7)))-(sum(dataset(0))+sum(dataset(1))+sum(dataset(2))+sum(dataset(3))+sum(dataset(4))+sum(dataset(5))+sum(dataset(6))+sum(dataset(7))))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}}%'
    data: '{{(sum(dataset(4))+sum(dataset(6))+sum(dataset(7)))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}},    {{sum(dataset(2))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}},    {{sum(dataset(3))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}},    {{sum(dataset(5))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}},    {{sum(dataset(1))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}},{{sum(dataset(0))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}},{{(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7)))-(sum(dataset(0))+sum(dataset(1))+sum(dataset(2))+sum(dataset(3))+sum(dataset(4))+sum(dataset(5))+sum(dataset(6))+sum(dataset(7))))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}}'
    extLabel: '{{(sum(dataset(4))+sum(dataset(6))+sum(dataset(7)))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}}%,    {{sum(dataset(2))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}}%,    {{sum(dataset(3))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}}%,    {{sum(dataset(5))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}}%,    {{sum(dataset(1))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}}%,{{sum(dataset(0))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}}%,{{(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7)))-(sum(dataset(0))+sum(dataset(1))+sum(dataset(2))+sum(dataset(3))+sum(dataset(4))+sum(dataset(5))+sum(dataset(6))+sum(dataset(7))))*100/(12*60*(numTargets(dataset(0))+numTargets(dataset(1))+numTargets(dataset(2))+numTargets(dataset(3))+numTargets(dataset(4))+numTargets(dataset(5))+numTargets(dataset(6))+numTargets(dataset(7))))}}%'

    
	showExtLabelOnlyIfNoLabel: true
    dataColor: '#FF6F00, #B71C1C, #1B5E20, #5D4037, #00838F, #0D47E1, #311B92'
	ratioInnerRadius: 0.6
	dataName: Teaching, Research, Studies, Bonus work, Office Work, Home Work, Free time
    showLegend: true
    legendPosition: right
    legendOrientation: vertical
```
##### Summary 
Up till now, we got a total of:
```dataviewjs
let hWork = 0, oWork = 0, rWork = 0, pWork=0, sWork=0, tWork=0, mWork=0, eWork=0;
let hWork_ = 0, oWork_ = 0, rWork_ = 0, pWork_=0, sWork_=0, tWork_=0, mWork_=0, eWork_=0;
const pages = dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.hWork || p.oWork || p.rWork || p.sWork || p.pWork || p.tWork || p.mWork || p.eWork);    
const pages_ = dv.pages('"00 - Main vault/Notes/Calenders"').where(p => p.hWork || p.oWork || p.rWork || p.sWork || p.pWork || p.tWork || p.mWork || p.eWork);

let payH=0,payS=0,payO=0,payR=0,payP=0,payT=0,payM=0,payE=0;

// Function to safely handle both single numbers and lists
const sumValues = (value) => {
	let sum=0;
	try{
		for(var k of value){
			sum+=(Number(k)||0);
		}
	}
	catch{
		sum = value;
	}
	return sum;
};

for (let p of pages) {
    hWork += sumValues(p.hWork || 0);
    sWork += sumValues(p.sWork || 0);
    tWork += sumValues(p.tWork || 0);
    eWork += sumValues(p.eWork || 0);
    mWork += sumValues(p.mWork || 0);
    oWork += sumValues(p.oWork || 0);
    rWork += sumValues(p.rWork || 0);
    pWork += sumValues(p.pWork || 0);

	payH += sumValues(p.hWork || 0)*sumValues(p.hWorkDh || 0)/60;
	payS += sumValues(p.sWork || 0)*sumValues(p.sWorkDh || 0)/60;
	payT += sumValues(p.tWork || 0)*sumValues(p.tWorkDh || 0)/60;
	payE += sumValues(p.eWork || 0)*sumValues(p.eWorkDh || 0)/60;
	payM += sumValues(p.mWork || 0)*sumValues(p.mWorkDh || p.tWorkDh || 0)/60;
	payO += sumValues(p.oWork || 0)*sumValues(p.oWorkDh || 0)/60;
	payR += sumValues(p.rWork || 0)*sumValues(p.rWorkDh || 0)/60;
	payP += sumValues(p.pWork || 0)*sumValues(p.pWorkDh || 0)/60;

}
for (let p of pages_) {
    hWork_ += sumValues(p.hWork || 0);
    sWork_ += sumValues(p.sWork || 0);
    tWork_ += sumValues(p.tWork || 0);
    eWork_ += sumValues(p.eWork || 0);
    //dv.span(eWork_+p.file.link+p.eWork+"</br>")
    mWork_ += sumValues(p.mWork || 0);
    oWork_ += sumValues(p.oWork || 0);
    rWork_ += sumValues(p.rWork || 0);
    pWork_ += sumValues(p.pWork || 0);
}

// Convert minutes to "Xh Ym" format
const formatTime = (minutes) => {
    const years = Math.floor(minutes / (60*24*365.25));
    const months = Math.floor(minutes / (60*24*(365.25/12))) % 12;
    const days = Math.floor(minutes / (60*24)) % 30;
    const hours = Math.floor(minutes / 60) % 24;
    const hours_ = Math.floor(minutes / 60);
    const mins = minutes % 60;
    if (minutes>(60*24*365.25)){
	    return [`{years}y ${months}m ${days}d ${hours}h ${mins}min`,`(= ${hours_}h ${mins}min)`];
    }else if (minutes>(60*24*30)){
	    return [`${months}m ${days}d ${hours}h ${mins}min`,`(= ${hours_}h ${mins}min)`];
    }else if (minutes>(60*24)){
	    return [`${days}d ${hours}h ${mins}min`,`(= ${hours_}h ${mins}min)`];
    }
	return [`${hours}h ${mins}min`,`(= ${hours_}h ${mins}min)`];
};

let O = formatTime(oWork+tWork+rWork+mWork+eWork);
let H = formatTime(hWork);
let S = formatTime(sWork);
let R = formatTime(rWork);
let T = formatTime(tWork);
let E = formatTime(eWork);
let M = formatTime(mWork);
let P = formatTime(pWork);
let TT = formatTime(hWork+sWork+oWork+tWork+mWork+rWork+pWork+eWork);

let O_ = formatTime(oWork_+tWork_+rWork_+mWork_+eWork_);
let H_ = formatTime(hWork_);
let S_ = formatTime(sWork_);
let R_ = formatTime(rWork_);
let T_ = formatTime(tWork_);
let E_ = formatTime(eWork_);
let M_ = formatTime(mWork_);
let P_ = formatTime(pWork_);
let TT_ = formatTime(hWork_+sWork_+oWork_+tWork_+mWork_+rWork_+pWork_+eWork_);

// Display totals in the note
dv.table(
    ["Category", "Tracked Time", "Official Time","Expected payment"], // Table headers
    [
        ["👨‍💼 Official work",`<div class="cell-split"><span>${O[0]}</span><span>${O[1]}</span></div>`,`<div class="cell-split"><span>${O_[0]}</span><span>${O_[1]}</span></div>`,`<div class="cell-right">${(payO+payT+payM+payR).toFixed(2)} Dh</div>`],
        ["🤹‍♂️ Self-improvements", `<div class="cell-split"><span>${H[0]}</span><span>${H[1]}</span></div>`,`<div class="cell-split"><span>${H_[0]}</span><span>${H_[1]}</span></div>`,`<div class="cell-right">${(payH).toFixed(2)} Dh</div>`],
        ["👶 Studies", `<div class="cell-split"><span>${S[0]}</span><span>${S[1]}</span></div>`,`<div class="cell-split"><span>${S_[0]}</span><span>${S_[1]}</span></div>`,`<div class="cell-right">${(payS).toFixed(2)} Dh</div>`],
        ["👨‍🎓 Research work",     `<div class="cell-split"><span>${R[0]}</span><span>${R[1]}</span></div>`,`<div class="cell-split"><span>${R_[0]}</span><span>${R_[1]}</span></div>`,`<div class="cell-right">${(payR).toFixed(2)} Dh</div>`],
        ["👨‍🏫 Teaching work",     `<div class="cell-split"><span>${T[0]}</span><span>${T[1]}</span></div>`,`<div class="cell-split"><span>${T_[0]}</span><span>${T_[1]}</span></div>`,`<div class="cell-right">${(payT).toFixed(2)} Dh</div>`],
        ["👥 Monitoring work",     `<div class="cell-split"><span>${M[0]}</span><span>${M[1]}</span></div>`,`<div class="cell-split"><span>${M_[0]}</span><span>${M_[1]}</span></div>`,`<div class="cell-right">${(payM).toFixed(2)} Dh</div>`],
        ["🕵️‍♂️ Examination work",     `<div class="cell-split"><span>${E[0]}</span><span>${E[1]}</span></div>`,`<div class="cell-split"><span>${E_[0]}</span><span>${E_[1]}</span></div>`,`<div class="cell-right">${(payE).toFixed(2)} Dh</div>`],
        ["💸 Temporary work",      `<div class="cell-split"><span>${P[0]}</span><span>${P[1]}</span></div>`,`<div class="cell-split"><span>${P_[0]}</span><span>${P_[1]}</span></div>`,`<div class="cell-right">${(payP).toFixed(2)} Dh</div>`],
        ["---", "---", "---", "---"],
    // Totals row
    ["**TOTAL**", `<div class="cell-split"><span>${TT[0]}</span><span>${TT[1]}</span></div>`,`<div class="cell-split"><span>${TT_[0]}</span><span>${TT_[1]}</span></div>`,`<div class="cell-right">${(payP+payS+payR+payH+payO+payT+payM).toFixed(2)} Dh</div>`]]
);
```
##### teaching statistics 
Up till now, we got a total of:
```dataviewjs
let pWork=0, pWorkE=0, tWork=0, twWork=0, eWorkP=0;
const pages = dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.hWork || p.oWork || p.rWork || p.sWork || p.pWork || p.tWork || p.mWork || p.eWork);
    
const toRight = (text) => {
	return `<div class="cell-right">${text}</div>`
}
const forEachCalc = (L1,L2) => {
	let sum=0;
	for (let i=0; i<L1.length;i++){
		sum += L1[i]*L2[i];
	}
	return sum;
}; 
   
let tAnasBerkaCM=0, tAnasBerkaTP=0, tAnasBerkaTD=0, SecW=0;
for (let p of pages) {
    tWork += (p.tWork || 0);
    twWork += (p.twWork || (p.tWork || 0));
    pWork += (p.pWork || 0);
    pWorkE += (p.tAnasBerkaEM || 0);
    eWorkP += (p.tAnasBerkaES || 0);
    tAnasBerkaCM += (p.tAnasBerkaCM || 0);
    tAnasBerkaTP += (p.tAnasBerkaTP || 0);
    tAnasBerkaTD += (p.tAnasBerkaTD || 0); 
}
SecW = tAnasBerkaCM+tAnasBerkaTP+tAnasBerkaTD;

let tWorkR = tWork;
let tWorkC = (tWork/(SecW || 1))*(tAnasBerkaCM+(2/3)*tAnasBerkaTD+tAnasBerkaTP*.5);
let tWorkD = (tWork/(SecW || 1))*(tAnasBerkaCM*(3/2)+tAnasBerkaTD+.75*tAnasBerkaTP);
let tWorkP = (tWork/(SecW || 1))*(tAnasBerkaCM*2+(4/3)*tAnasBerkaTD+tAnasBerkaTP);

let tWorkR_ = twWork;
let tWorkC_ = (twWork/(SecW || 1))*(tAnasBerkaCM+(2/3)*tAnasBerkaTD+tAnasBerkaTP*.5);
let tWorkD_ = (twWork/(SecW || 1))*(tAnasBerkaCM*(3/2)+tAnasBerkaTD+.75*tAnasBerkaTP);
let tWorkP_ = (twWork/(SecW || 1))*(tAnasBerkaCM*2+(4/3)*tAnasBerkaTD+tAnasBerkaTP);

// Duration
const Duration=1.75;
const YOS=1;

// Fall semester
let coursF=[0,0], TDsF=[0,0], TPsF=0, FSE = 0, FSEI = 0;
let classCoursF=[0,0], GrpTDsF=[0,0], GrpTPsF=[0,0];

// Spring semester
let coursS=[0,0], TDsS=[0,0], TPsS=[0,0], SSE = 0, SSEI = 0;
let classCoursS=[0,0], GrpTDsS=[0,0], GrpTPsS=[0,0]; 

// Calculation Officiel:
let FS=(forEachCalc(coursF,classCoursF)+
forEachCalc(TDsF,GrpTDsF)+
forEachCalc(TPsF,GrpTPsF))*Duration-FSEI;
let SS=(forEachCalc(coursS,classCoursS)+
forEachCalc(TDsS,GrpTDsS)+
forEachCalc(TPsS,GrpTPsS))*Duration-SSEI;

let FSC=(forEachCalc(coursF,classCoursF)+
forEachCalc(TDsF,GrpTDsF)*(2/3)+
forEachCalc(TPsF,GrpTPsF)*.5)*Duration-FSEI*.5;
let SSC=(forEachCalc(coursS,classCoursS)+
forEachCalc(TDsS,GrpTDsS)*(2/3)+
forEachCalc(TPsS,GrpTPsS)*.5)*Duration-SSEI*.5;

let FSD=(forEachCalc(coursF,classCoursF)*1.5+
forEachCalc(TDsF,GrpTDsF)+
forEachCalc(TPsF,GrpTPsF)*.75)*Duration-FSEI*.75;
let SSD=(forEachCalc(coursS,classCoursS)*1.5+
forEachCalc(TDsS,GrpTDsS)+
forEachCalc(TPsS,GrpTPsS)*.75)*Duration-SSEI*.75;

let FSP=(forEachCalc(coursF,classCoursF)*2+
forEachCalc(TDsF,GrpTDsF)*(4/3)+
forEachCalc(TPsF,GrpTPsF))*Duration-FSEI;
let SSP=(forEachCalc(coursS,classCoursS)*2+
forEachCalc(TDsS,GrpTDsS)*(4/3)+
forEachCalc(TPsS,GrpTPsS))*Duration-SSEI;

// Calculation Strict:
let coursFH=[0,0], TDsFH=[0,0], TPsFH=[0,0], DsFH=[0,0];
let classCoursFH=[0,0], GrpTDsFH=[0,0], GrpTPsFH=[0,0], GrpDsFH=[0,0];
let coursSH=[0,0,0], TDsSH=[0,0,0], TPsSH=[0,0,0], DsSH=[0,0,0];
let classCoursSH=[0,0,0], GrpTDsSH=[0,0,0], GrpTPsSH=[0,0,0], GrpDsSH=[0,0,0]; 

let FS_=forEachCalc(coursFH,classCoursFH)+forEachCalc(TDsFH,GrpTDsFH)+forEachCalc(TPsFH,GrpTPsFH);
let SS_=forEachCalc(coursS,classCoursS)+
forEachCalc(TDsS,GrpTDsS)+
forEachCalc(TPsS,GrpTPsS);

let FSC_=forEachCalc(coursFH,classCoursFH)+forEachCalc(TDsFH,GrpTDsFH)*(2/3)+forEachCalc(TPsFH,GrpTPsFH)*.5;
let SSC_=forEachCalc(coursS,classCoursS)+
forEachCalc(TDsS,GrpTDsS)*(2/3)+
forEachCalc(TPsS,GrpTPsS)*.5;

let FSD_=forEachCalc(coursFH,classCoursFH)*1.5+forEachCalc(TDsFH,GrpTDsFH)+forEachCalc(TPsFH,GrpTPsFH)*.75;
let SSD_=forEachCalc(coursS,classCoursS)*1.5+
forEachCalc(TDsS,GrpTDsS)+
forEachCalc(TPsS,GrpTPsS)*.75;

let FSP_=forEachCalc(coursFH,classCoursFH)*2+forEachCalc(TDsFH,GrpTDsFH)*(4/3)+forEachCalc(TPsFH,GrpTPsFH);
let SSP_=forEachCalc(coursS,classCoursS)*2+
forEachCalc(TDsS,GrpTDsS)*(4/3)+
forEachCalc(TPsS,GrpTPsS);

const rows = [
  [
    "🗒️ By Descriptive",
    toRight((SS_+FS_).toFixed(2)),
    toRight((SSC_+FSC_).toFixed(2)),
    toRight((SSD_+FSD_).toFixed(2)),
    toRight((SSP_+FSP_).toFixed(2)),
    toRight((forEachCalc(DsFH,GrpDsFH)+forEachCalc(DsSH,GrpDsSH)).toFixed(2)),
    toRight((forEachCalc(DsFH,GrpDsFH)+forEachCalc(DsSH,GrpDsSH)+SSP_+FSP_).toFixed(2)),
  ],
  [
    "👨‍🏫 Work done (raw)",
    toRight((tWorkR/60).toFixed(2)),
    toRight((tWorkC/60).toFixed(2)),
    toRight((tWorkD/60).toFixed(2)),
    toRight((tWorkP/60).toFixed(2)),
    toRight((eWorkP/60).toFixed(2)),
    toRight(((eWorkP+tWorkP)/60).toFixed(2))
  ],
  [
    "👨‍🏫 Work done (majoration)",
    toRight((tWorkR_/60).toFixed(2)),
    toRight((tWorkC_/60).toFixed(2)),
    toRight((tWorkD_/60).toFixed(2)),
    toRight((tWorkP_/60).toFixed(2)),
    toRight((eWorkP/60).toFixed(2)),
    toRight(((eWorkP+tWorkP_)/60).toFixed(2))
  ],
  [
    "🤦‍♂️ Overwork time",
    toRight((((tWorkR/60)-(300*YOS))>0?((tWorkR/60)-(300*YOS)):0).toFixed(2)),
    toRight((((tWorkC/60)-(300*YOS))>0?((tWorkC/60)-(300*YOS)):0).toFixed(2)),
    toRight((((tWorkD/60)-(300*YOS))>0?((tWorkD/60)-(300*YOS)):0).toFixed(2)),
    toRight((((tWorkP/60)-(300*YOS))>0?((tWorkP/60)-(300*YOS)):0).toFixed(2)),
    toRight((((eWorkP/60)-(4*YOS))>0?((eWorkP/60)-(4*YOS)):0).toFixed(2)),
    toRight(((((eWorkP/60)-(4*YOS))>0?(((eWorkP+tWorkP)/60)-(4*YOS)):0)+(((tWorkP/60)-(300*YOS))>0?((tWorkP/60)-(300*YOS)):0)).toFixed(2))
  ],
  [
    "💲 Bonus work",
    toRight((((tWorkR>(18000*YOS)?(tWork-(300*YOS)):0)+pWork)/60).toFixed(2)),
    toRight((((tWorkC>(18000*YOS)?(tWork-(300*YOS)):0)+pWork)*.5/60).toFixed(2)),
    toRight((((tWorkD>(18000*YOS)?(tWork-(300*YOS)):0)+pWork)*.75/60).toFixed(2)),
    toRight((((tWorkP>(18000*YOS)?(tWork-(300*YOS)):0)+pWork)/60).toFixed(2)),
    toRight(((pWorkE/60).toFixed(2))),
    toRight((((pWorkE+(((tWorkD>(18000*YOS)?(tWork-(300*YOS)):0)+pWork)*.75/60))/60).toFixed(2))),
  ],
  [
    "🍂 Fall semester",
    toRight(FS.toFixed(2)),
    toRight(FSC.toFixed(2)),
    toRight(FSD.toFixed(2)),
    toRight(FSP.toFixed(2)),
    toRight((FSE+FSEI).toFixed(2)),
    toRight((FSE+FSEI+FSP).toFixed(2)),
  ],
  [
    "🌱 Spring semester",
    toRight(SS.toFixed(2)),
    toRight(SSC.toFixed(2)),
    toRight(SSD.toFixed(2)),
    toRight(SSP.toFixed(2)),
    toRight((SSE+SSEI).toFixed(2)),
    toRight((SSE+SSEI+SSP).toFixed(2)),
  ],
  [
    "🏫 By annual planning",
    toRight((FS+SS).toFixed(2)),
    toRight((FSC+SSC).toFixed(2)),
    toRight((FSD+SSD).toFixed(2)),
    toRight((FSP+SSP).toFixed(2)),
    toRight((FSE+FSEI+SSE+SSEI).toFixed(2)),
    toRight((FSE+FSEI+SSE+SSEI+FSP+SSP).toFixed(2)),
  ]
];

dv.table(
  ["Teaching workload", "Heurs (brut)", "Heurs (cours)", "Heurs (TD)", "Heurs (TP)", "Heurs (Exams)", "Heurs (Total)"],
  rows
);
dv.paragraph(`⚠️ Additional unpaid work hours: **${(((tWork-500*60*YOS)<0?0:(tWork-500*60*YOS))/60).toFixed(2)}**h`);
```
##### Per institution statistiques
Up till now, we got a total of:
```dataviewjs
let vINSACVLT=0, vUCAESTKT=0, vUIZENSAAT=0, vUIZFLSHT=0, vUIZFPTT=0, vUIZFSAT=0, vUIZFSJESCUAMT=0;
let vINSACVLE=0, vUCAESTKE=0, vUIZENSAAE=0, vUIZFLSHE=0, vUIZFPTE=0, vUIZFSAE=0, vUIZFSJESCUAME=0;
let vINSACVLP=0, vUCAESTKP=0, vUIZENSAAP=0, vUIZFLSHP=0, vUIZFPTP=0, vUIZFSAP=0, vUIZFSJESCUAMP=0;

const pages = dv.pages('"00 - Main vault/Notes"');

// Function to safely handle both single numbers and lists
const sumValues = (value) => {
	let sum=0;
	try{
		for(var k of value){
			sum+=(Number(k)||0);
		}
	}
	catch{
		sum = value;
	}
	return sum;
};
const timeToTable = (timeVar) => {
  timeVar = formatTime(timeVar)
  //return `<div class="cell-split"><span>${timeVar[0]}</span><span>${timeVar[1]}</span></div>`
  return `<div class="cell-stack">
            <div class="stack-top">${timeVar[0]}</div>
            <div class="stack-bottom">${timeVar[1]}</div>
         </div>`
}
    
for (let p of pages) {
	
    vINSACVLT += sumValues(p["Fr/INSA/CVL/T"] || 0);
    vUCAESTKT += sumValues(p["Ma/UCA/ESTK/T"] || 0);
    vUIZENSAAT += sumValues(p["Ma/UIZ/ENSAA/T"] || 0);
    vUIZFLSHT += sumValues(p["Ma/UIZ/FLSH/T"] || 0);
    vUIZFPTT += sumValues(p["Ma/UIZ/FPT/T"] || 0);
    vUIZFSAT += sumValues(p["Ma/UIZ/FSA/T"] || 0);
    vUIZFSJESCUAMT += sumValues(p["Ma/UIZ/FSJESCUAM/T"] || 0);

    vINSACVLE += sumValues((p["Fr/INSA/CVL/E"] || 0));
    vUCAESTKE += sumValues(p["Ma/UCA/ESTK/E"] || 0);
    vUIZENSAAE += sumValues(p["Ma/UIZ/ENSAA/E"] || 0);
    vUIZFLSHE += sumValues(p["Ma/UIZ/FLSH/E"] || 0);
    vUIZFPTE += sumValues(p["Ma/UIZ/FPT/E"] || 0);
    vUIZFSAE += sumValues(p["Ma/UIZ/FSA/E"] || 0);
    vUIZFSJESCUAME += sumValues(p["Ma/UIZ/FSJESCUAM/E"] || 0);

    vINSACVLP += sumValues(p["Fr/INSA/CVL/P"] || 0);
    vUCAESTKP += sumValues(p["Ma/UCA/ESTK/P"] || 0);
    vUIZENSAAP += sumValues(p["Ma/UIZ/ENSAA/P"] || 0);
    vUIZFLSHP += sumValues(p["Ma/UIZ/FLSH/P"] || 0);
    vUIZFPTP += sumValues(p["Ma/UIZ/FPT/P"] || 0);
    vUIZFSAP += sumValues(p["Ma/UIZ/FSA/P"] || 0);
    vUIZFSJESCUAMP += sumValues(p["Ma/UIZ/FSJESCUAM/P"] || 0);

}
    
// Convert minutes to "Xh Ym" format
// Convert minutes to "Xh Ym" format
const formatTime = (minutes) => {
    const years = Math.floor(minutes / (60*24*365.25));
    const months = Math.floor(minutes / (60*24*(365.25/12))) % 12;
    const days = Math.floor(minutes / (60*24)) % 30;
    const hours = Math.floor(minutes / 60) % 24;
    const hours_ = Math.floor(minutes / 60);
    const mins = minutes % 60;
    if (minutes>(60*24*365.25)){
	    return [`{years}y ${months}m ${days}d ${hours}h ${mins}min`,`(= ${hours_}h ${mins}min)`];
    }else if (minutes>(60*24*30)){
	    return [`${months}m ${days}d ${hours}h ${mins}min`,`(= ${hours_}h ${mins}min)`];
    }else if (minutes>(60*24)){
	    return [`${days}d ${hours}h ${mins}min`,`(= ${hours_}h ${mins}min)`];
    }
	return [`${hours}h ${mins}min`,`(= ${hours_}h ${mins}min)`];
};
let timeList=[];
timeList.push(vINSACVLT);
timeList.push(vUCAESTKT);
timeList.push(vUIZENSAAT);
timeList.push(vUIZFLSHT);
timeList.push(vUIZFPTT);
timeList.push(vUIZFSAT);
timeList.push(vUIZFSJESCUAMT);

const formatMoneyS = (money) => {
 return `<div class="cell-right">${(money).toFixed(2)} Dh</div>`;
};

const formatMoneyE = (money) => {
 return `<div class="cell-right">${(money).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })} Dh</div>`;
};

// Display totals in the note
dv.table(
    ["Institution", "Tracked time working", "Expected payment", "Actuel payment","Difference 💰"], // Table headers
    [
        ["INSA-CVL",timeToTable(timeList[0]), formatMoneyE(vINSACVLE),formatMoneyE(vINSACVLP),formatMoneyE(vINSACVLP-vINSACVLE)],
        ["UCA ESTK",timeToTable(timeList[1]), formatMoneyE(vUCAESTKE),formatMoneyE(vUCAESTKP),formatMoneyE(vUCAESTKP-vUCAESTKE)],
        ["UIZ ENSAA",timeToTable(timeList[2]), formatMoneyE(vUIZENSAAE),formatMoneyE(vUIZENSAAP),formatMoneyE(vUIZENSAAP-vUIZENSAAE)],
        ["UIZ FLSH",timeToTable(timeList[3]), formatMoneyE(vUIZFLSHE),formatMoneyE(vUIZFLSHP),formatMoneyE(vUIZFLSHP-vUIZFLSHE)],
        ["UIZ FPT",timeToTable(timeList[4]), formatMoneyE(vUIZFPTE),formatMoneyE(vUIZFPTP),formatMoneyE(vUIZFPTP-vUIZFPTE)],
        ["UIZ FSA",timeToTable(timeList[5]), formatMoneyE(vUIZFSAE),formatMoneyE(vUIZFSAP),formatMoneyE(vUIZFSAP-vUIZFSAE)],
        ["UIZ FSJES-CUAM",timeToTable(timeList[6]), formatMoneyE(vUIZFSJESCUAME), formatMoneyE(vUIZFSJESCUAMP),formatMoneyE(vUIZFSJESCUAMP-vUIZFSJESCUAME)],
    ]
);
```
##### Per module statistiques 
Up till now, we got a total of:
```dataviewjs
	const varNames = [
        "Algorithmique et Programmation", 
        "Bases de Données", 
        "Bases de Données avancées", 
        "Culture Digital",
        "Data Mining", 
        "Deep Learning",
        "Développement Web", 
        "Machine Learning", 
        "Programmation C", 
        "Programmation C++", 
    ];
const varCodes = [
    "AP", 
    "DB", 
    "DBA", 
    "CD", 
    "DM", 
    "DL",
    "Web",
    "ML", 
    "C", 
    "Cpp", 
     
    ];
const subVars = ["CT", "CC", "TPT", "TPC", "ET", "EC"];
const subVarsTitles = ["Lectures duration", "Lectures sessions", "TPs duration", "TPs sessions", "Exams durations", "Exams sessions", "Total duration (TDR)", "Total duration (TDC)", "Total duration (TDT)", "Worth of money"]

const pages = dv.pages('"00 - Main vault/Notes"');

// Convert minutes to "Xm Yd Zh Wm" format
const formatTime = (minutes) => {
    const years = Math.floor(minutes / (60*24*365.25));
    const months = Math.floor(minutes / (60*24*(365.25/12))) % 12;
    const days = Math.floor(minutes / (60*24)) % 30;
    const hours = Math.floor(minutes / 60) % 24;
    const hours_ = Math.floor(minutes / 60);
    const mins = minutes % 60;
    if (minutes>(60*24*365.25)){
	    return [`{years}y ${months}m ${days}d ${hours}h ${mins}min`,`(= ${hours_}h ${mins}min)`];
    }else if (minutes>(60*24*30)){
	    return [`${months}m ${days}d ${hours}h ${mins}min`,`(= ${hours_}h ${mins}min)`];
    }else if (minutes>(60*24)){
	    return [`${days}d ${hours}h ${mins}min`,`(= ${hours_}h ${mins}min)`];
    }
	return [`${hours}h ${mins}min`,`(= ${hours_}h ${mins}min)`];
};
const timeToTable = (timeVar) => {
  timeVar = formatTime(timeVar)
  //return `<div class="cell-split"><span>${timeVar[0]}</span><span>${timeVar[1]}</span></div>`
  return `<div class="cell-stack">
            <div class="stack-top">${timeVar[0]}</div>
            <div class="stack-bottom">${timeVar[1]}</div>
         </div>`
}

//Format money:
const formatMoneyS = (money) => {
 return `<div class="cell-right">${(money).toFixed(2)} Dh</div>`;
};

const formatMoneyE = (money) => {
 return `<div class="cell-right">${(money).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })} Dh</div>`;
};

// Function to safely handle both single numbers and lists
const sumValues = (value) => {
	let sum=0;
	try{
		for(var k of value){
			sum+=(Number(k)||0);
		}
	}
	catch{
		sum = value;
	}
	return sum;
};
    
let tableData = [];

for (let i = 0; i < varCodes.length; i++) {
    const varName = varNames[i];
    const varCode = varCodes[i];
    let row = { Modules: varName };

    // Initialize counters
    for (let subVar of subVars) {
        row[subVar] = 0;
    }

    // Sum all pages for this module
    for (let p of pages) {
        for (let subVar of subVars) {
            const varKey = `${varCode}${subVar}`;
            if (p[varKey]) row[subVar] += sumValues(p[varKey]);
        }
    }
    row["WM"] = formatMoneyE((row["CT"]*2+row["TPT"]+row["ET"]/2)*200/60);
    row["TDR"] = timeToTable(row["CT"]+row["TPT"]+row["ET"]);
    row["TDC"] = timeToTable(row["CT"]+row["TPT"]/2);
    row["TDT"] = timeToTable(row["CT"]*2+row["TPT"]);
    row["CT"] = timeToTable(row["CT"]);
    row["TPT"] = timeToTable(row["TPT"]);
    row["ET"] = timeToTable(row["ET"]);
    tableData.push(row);
}

const header = ["Modules", ...subVarsTitles];
const headers = ["Modules", ...subVars, "TDR", "TDC", "TDT","WM"];

// Render the dataview table
dv.table(header, tableData.map(row => headers.map(h => row[h] ?? 0)));
```

##### Encadrement
```dataviewjs
// --- modules
const varNames = ["Support", "PFE DUT","PFE DEUG","PFE Licence","PFA Master","PFE Master","Thesis"];

const varCodesTags = [
    "Contacts/Professional/Mentees",
    "Contacts/Professional/Mentees/DUT",
    "Contacts/Professional/Mentees/DEUG",
    "Contacts/Professional/Mentees/Licence",
    "Contacts/Professional/Mentees/Master/PFA", 
    "Contacts/Professional/Mentees/Master/PFE",
    "Contacts/Professional/Mentees/PhD"
];

const varCodes = ["Support","PFE/DUT","PFE/DEUG","PFE/Licence","PFA/Master","PFE/Master","Thesis"];

// --- init dictionaries
let dictStuFull = {};
for (let i = 0; i < varCodes.length; i++) dictStuFull[varCodes[i]] = [];


// --- exclusion list (lowercase)
const excludedContacts = [
    "my professional circle"
].map(x => x.toLowerCase());

// --- contact folders (store raw paths, no embedded quotes)
const contactFolders = [
    "00 - Main vault/Notes/Relationships",
    "06 - Projects/Supervision"
];

// --- collect students from multiple folders with exclusion
contactFolders
  .flatMap(folder => Array.from(dv.pages(`"${folder}"`)))   // ensure we pass a quoted string to dv.pages
  .filter(p => !excludedContacts.some(ex => (p.file.name || "").toLowerCase().includes(ex)))
  .sort(p => p.file.name,'asc')
  .forEach(page => {
    const tags = (page.file.tags || [])
      .map(t => (t + "").replace(/^#/, "").replace(/-/g, " ").trim());

    for (let i = 0; i < varCodes.length; i++) {
      const targetTag = varCodesTags[i].toLowerCase();
      const match = tags.find(t => t.toLowerCase() === targetTag);
      if (match) dictStuFull[varCodes[i]].push(page.file.name);
    }
  });

// --- normalize / pseudos
const normalizeName = (name) =>
  (name + "")
    .normalize("NFD")
    .replace(/[\u0300-\u036f]/g, "")
    .replace(/[^a-zA-Z0-9]/g, "")
    .trim();

let dictStuCode = {};
for (const k of Object.keys(dictStuFull)) {
  dictStuCode[k] = (dictStuFull[k] || []).map(n => normalizeName(n));
}

// --- configuration
const subVars = ["EP","EO","RS","SS","SE"];
const subVarsTitles = [
  "Encadrement présentiel",
  "Encadrement online",
  "Répétition soutenance",
  "Soutenance (Encadrant)",
  "Soutenance (Examinateur)"
];

// --- pages to scan for time entries (you can add more folders if needed)
const pages = Array.from(dv.pages(`"00 - Main vault/Notes"`));

// --- helpers
const formatTime = (minutes) => {
    const years = Math.floor(minutes / (60*24*365.25));
    const months = Math.floor(minutes / (60*24*(365.25/12))) % 12;
    const days = Math.floor(minutes / (60*24)) % 30;
    const hours = Math.floor(minutes / 60) % 24;
    const hours_ = Math.floor(minutes / 60);
    const mins = minutes % 60;
    if (minutes>(60*24*365.25)){
	    return [`{years}y ${months}m ${days}d ${hours}h ${mins}min`,`(= ${hours_}h ${mins}min)`];
    }else if (minutes>(60*24*30)){
	    return [`${months}m ${days}d ${hours}h ${mins}min`,`(= ${hours_}h ${mins}min)`];
    }else if (minutes>(60*24)){
	    return [`${days}d ${hours}h ${mins}min`,`(= ${hours_}h ${mins}min)`];
    }
	return [`${hours}h ${mins}min`,`(= ${hours_}h ${mins}min)`];
};
const timeToTable = (timeVar) => {
  timeVar = formatTime(timeVar)
  //return `<div class="cell-split"><span>${timeVar[0]}</span><span>${timeVar[1]}</span></div>`
  return `<div class="cell-stack">
            <div class="stack-top">${timeVar[0]}</div>
            <div class="stack-bottom">${timeVar[1]}</div>
         </div>`
}

const sumValues = (value) => {
  let sum = 0;
  if (value == null) return 0;
  if (Array.isArray(value) || (typeof value === "object" && Symbol.iterator in value)) {
    for (const k of value) sum += (Number(k) || 0);
  } else {
    sum = Number(value) || 0;
  }
  return sum;
};

//Format money:
const formatMoneyS = (money) => {
 return `<div class="cell-right">${(money).toFixed(2)} Dh</div>`;
};

const formatMoneyE = (money) => {
 return `<div class="cell-right">${(money).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })} Dh</div>`;
};


// --- build table
let tableData = [];

for (let i = 0; i < varCodes.length; i++) {
  const varName = varNames[i];
  const varCode = varCodes[i];
  const fullNames = dictStuFull[varCode] || [];
  const codeNames = dictStuCode[varCode] || [];

  if (!fullNames.length) continue;

  let first = true;
  for (let j = 0; j < fullNames.length; j++) {
    const full = fullNames[j];
    // fallback: if codeNames[j] missing, generate from full
    const code = codeNames[j] || normalizeName(full);
    let row = {};
    row["Stu"] = `[[${full}]]`;

    // numeric accumulators
    let numeric = {};
    for (const s of subVars) numeric[s] = 0;

    for (const p of pages) {
      for (const s of subVars) {
        const key = `${varCode}/v${code}/${s}`;
        if (p[key] !== undefined) numeric[s] += sumValues(p[key]);
      }
    }

    // compute numeric WM and formatted WM
    const numericTT = numeric["EP"] + numeric["EO"] + numeric["RS"] + numeric["SS"] + numeric["SE"];
    row["TT"] = timeToTable(numericTT);
    const numericWM = (((numeric["EP"] + numeric["EO"]) * 1.5 + numeric["RS"] + (numeric["SS"] + numeric["SE"]) * 2) * 200) / 60;
    row["WM_numeric"] = numericWM;
    row["WM"] = formatMoneyE(numericWM);

    // format times for display
    for (const s of subVars) row[s] = timeToTable(numeric[s]);

    // push only if numericWM > 0 (filter by numeric, not by formatted string)
    if (numericWM > 0) {
      row["Modules"] = varName;//first ? varName : "";
      tableData.push(row);
      first = false;
    }
    
  }
}

function extractStudentName(stu) {
  return (stu || "")
    .replace(/\[\[/g, "")
    .replace(/\]\]/g, "")
    .trim();
}

function naturalCompare(aStr, bStr) {
  const a = aStr.split(/(\d+)/).filter(Boolean);
  const b = bStr.split(/(\d+)/).filter(Boolean);

  const len = Math.min(a.length, b.length);
  for (let i = 0; i < len; i++) {
    const ai = a[i], bi = b[i];
    const na = Number(ai), nb = Number(bi);

    const bothNumbers = !isNaN(na) && !isNaN(nb);
    if (bothNumbers) {
      if (na !== nb) return na - nb;
    } else {
      const cmp = ai.localeCompare(bi, "fr", { sensitivity: "base" });
      if (cmp !== 0) return cmp;
    }
  }
  return a.length - b.length;
}

tableData.sort((a, b) => {
  const nameA = extractStudentName(a["Modules"]);
  const nameB = extractStudentName(b["Modules"]);
  return naturalCompare(nameA, nameB);
}).sort((a, b) => {
  const nameA = extractStudentName(a["Stu"]);
  const nameB = extractStudentName(b["Stu"]);
  return naturalCompare(nameA, nameB);
});

// --- render
const header = ["Projets","Étudiant(e)(s)",...subVarsTitles,"Total time","Worth of money"];
const headers = ["Modules","Stu",...subVars,"TT","WM"];
console.log("DEBUG tableData:", JSON.parse(JSON.stringify(tableData)));

dv.table(header, tableData.map(row => headers.map(h => row[h] ?? 0)));

```
