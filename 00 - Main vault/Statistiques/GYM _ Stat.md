---
tags:
  - Personal/Stats
Creation date: 2025-03-04 15:43
banner: "[[DeathNoteBanner.jpg]]"
banner_x: 0
banner_y: 0.906
cssclasses:
  - daily
  - sNote
---
## Global fitness goal 🏋️‍♂️

```dataviewjs
const calendarData = {
    intensityScaleStart: 0,
    intensityScaleEnd: 10, // I have 10 color shades in gaming
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "gaming",
        "gaming": [
    "rgb(51, 51, 51)", 
    "rgb(77, 77, 77)", 
    "rgb(102, 102, 102)", 
    "rgb(160, 160, 160)", 
    "rgb(217, 221, 222)", 
    "rgb(150, 160, 180)", 
    "rgb(80, 90, 120)", 
    "rgb(40, 50, 80)", 
    "rgb(20, 30, 60)", 
    "rgb(0, 10, 26)"
],
    }
};
function scaleIntensity(intensity,maxDay) {
    if (intensity < maxDay) {
        return ((intensity / maxDay) * 9); // Scale to 0-10
    } else {
        return 9; // Assign 10 if intensity is maxDay or greater
    }
};
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.gymMin || p.pushUpReps || p.setUpReps || p.squadReps || p.runingKm || p.travelingDist )) {
	let fun = ((page.gymMin||0) / 90) + (((page.pushUpReps||0) / 100) + ((page.setUpReps||0) / 100) + ((page.squadReps||0) / 100))/3 + ((page.runingKm||0) / 2) + ((page.travelingDist||0) / 5);
	if ( fun === 0) { continue; }
	let scaledIntensity = scaleIntensity(fun,4) +1; //500 is daily salery
    calendarData.entries.push({
        date: page.file.name,
        intensity: scaledIntensity, // Use scaled intensity
        color:"gaming",
        content: await dv.span(`[](${page.file.name})`), // For hover preview
    });
}
//renderHeatmapTracker(this.container, calendarData)

const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData)

// Adding container for legends and colored boxes on the same line
const legendsContainer = document.createElement('div');
legendsContainer.style.display = 'flex';
legendsContainer.style.alignItems = 'center'; // Align vertically
legendsContainer.style.justifyContent = 'center'; // Center horizontally 
legendsContainer.style.width = '100%'; // Ensure it takes full width for centering

// Adding first legend with reduced size and custom font
const firstLegend = document.createElement('div');
firstLegend.innerText = 'LESS'; // Updated to "LESS" with all caps
firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
legendsContainer.appendChild(firstLegend);

// Adding colored boxes with adjusted size
const legendContainer = document.createElement('div');
legendContainer.style.display = 'flex';
legendContainer.style.alignItems = 'center'; // Align vertically

for (let color of calendarData.colorScheme.gaming) {
    const colorBox = document.createElement('div');
    colorBox.style.width = '9px'; // Reduced box width by 50%
    colorBox.style.height = '9px'; // Reduced box height by 50%
    colorBox.style.backgroundColor = color;
    colorBox.style.marginRight = '5px'; // Adjusted margin
    legendContainer.appendChild(colorBox);
}

// Adding second legend after the colored boxes with reduced size and custom font
const secondLegend = document.createElement('div');
secondLegend.innerText = 'MORE'; // Updated to "MORE" with all caps
secondLegend.style.fontSize = '65%'; // Reduce font size by 50%
secondLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
secondLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
legendContainer.appendChild(secondLegend);

legendsContainer.appendChild(legendContainer);
legendsContainer.style.marginBottom = "12px";

heatmapTrackerEl.appendChild(legendsContainer);

dv.span('Training tracker statistics:')

renderHeatmapTrackerStatistics(this.container, calendarData)

```
***
## Traveling Distance 🚶‍♂️

```dataviewjs
const calendarData = {
    intensityScaleStart: 0,
    intensityScaleEnd: 10, // I have 10 color shades in gaming
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "gaming",
        "gaming": [
    "rgb(51, 51, 51)", 
    "rgb(77, 77, 77)", 
    "rgb(102, 102, 102)", 
    "rgb(160, 160, 160)", 
    "rgb(217, 221, 222)", 
    "rgb(150, 160, 180)", 
    "rgb(80, 90, 120)", 
    "rgb(40, 50, 80)", 
    "rgb(20, 30, 60)", 
    "rgb(0, 10, 26)"
],
    }
};
function scaleIntensity(intensity,maxDay) {
    if (intensity < maxDay) {
        return intensity; // Scale to 0-10
    } else {
        return 10; // Assign 10 if intensity is maxDay or greater
    }
};
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.travelingDist )) {
	let fun = page.travelingDist;
	if ( fun < 1) { continue; }
	let scaledIntensity = scaleIntensity(fun,10); 
    calendarData.entries.push({
        date: page.file.name,
        intensity: scaledIntensity, // Use scaled intensity
        color:"gaming",
        content: await dv.span(`[](${page.file.name})`), // For hover preview
    });
}
//renderHeatmapTracker(this.container, calendarData)

const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData)

// Adding container for legends and colored boxes on the same line
const legendsContainer = document.createElement('div');
legendsContainer.style.display = 'flex';
legendsContainer.style.alignItems = 'center'; // Align vertically
legendsContainer.style.justifyContent = 'center'; // Center horizontally 
legendsContainer.style.width = '100%'; // Ensure it takes full width for centering

// Adding first legend with reduced size and custom font
const firstLegend = document.createElement('div');
firstLegend.innerText = 'LESS'; // Updated to "LESS" with all caps
firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
legendsContainer.appendChild(firstLegend);

// Adding colored boxes with adjusted size
const legendContainer = document.createElement('div');
legendContainer.style.display = 'flex';
legendContainer.style.alignItems = 'center'; // Align vertically

for (let color of calendarData.colorScheme.gaming) {
    const colorBox = document.createElement('div');
    colorBox.style.width = '9px'; // Reduced box width by 50%
    colorBox.style.height = '9px'; // Reduced box height by 50%
    colorBox.style.backgroundColor = color;
    colorBox.style.marginRight = '5px'; // Adjusted margin
    legendContainer.appendChild(colorBox);
}

// Adding second legend after the colored boxes with reduced size and custom font
const secondLegend = document.createElement('div');
secondLegend.innerText = 'MORE'; // Updated to "MORE" with all caps
secondLegend.style.fontSize = '65%'; // Reduce font size by 50%
secondLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
secondLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
legendContainer.appendChild(secondLegend);

legendsContainer.appendChild(legendContainer);
legendsContainer.style.marginBottom = "12px";

heatmapTrackerEl.appendChild(legendsContainer);

dv.span('Traveling tracker statistics:')

renderHeatmapTrackerStatistics(this.container, calendarData)

```

***

## GYM only stats 🗿
```dataviewjs
const calendarData = {
    intensityScaleStart: 0,
    intensityScaleEnd: 10, // I have 10 color shades in gaming
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "gaming",
        "gaming": [
    "rgb(51, 51, 51)", 
    "rgb(77, 77, 77)", 
    "rgb(102, 102, 102)", 
    "rgb(160, 160, 160)", 
    "rgb(217, 221, 222)", 
    "rgb(150, 160, 180)", 
    "rgb(80, 90, 120)", 
    "rgb(40, 50, 80)", 
    "rgb(20, 30, 60)", 
    "rgb(0, 10, 26)"
],
    }
};
function scaleIntensity(intensity,maxDay) {
    if (intensity < maxDay) {
        return ((intensity / maxDay) * 9); // Scale to 0-10
    } else {
        return 9; // Assign 10 if intensity is maxDay or greater
    }
};
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.gymMin || p.gymKg || p.myWeight )) {
	if (page.gymMin == 0) { continue; }
	let myWeight = page.myWeight||89;
	//if ( myWeight == 0) { myWeight=89; }
	let fun = page.gymKg / page.gymMin;
	if ( fun == 0) { fun = (page.pushUpReps + page.setUpReps + page.squadReps)* myWeight / page.gymMin; }
	let scaledIntensity = scaleIntensity(fun,15*myWeight*3*3/90) +1; //500 is daily salery
    calendarData.entries.push({
        date: page.file.name,
        intensity: scaledIntensity, // Use scaled intensity
        color:"gaming",
        content: await dv.span(`[](${page.file.name})`), // For hover preview
    });
}
//renderHeatmapTracker(this.container, calendarData)

const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData)

// Adding container for legends and colored boxes on the same line
const legendsContainer = document.createElement('div');
legendsContainer.style.display = 'flex';
legendsContainer.style.alignItems = 'center'; // Align vertically
legendsContainer.style.justifyContent = 'center'; // Center horizontally 
legendsContainer.style.width = '100%'; // Ensure it takes full width for centering

// Adding first legend with reduced size and custom font
const firstLegend = document.createElement('div');
firstLegend.innerText = 'LESS'; // Updated to "LESS" with all caps
firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
legendsContainer.appendChild(firstLegend);

// Adding colored boxes with adjusted size
const legendContainer = document.createElement('div');
legendContainer.style.display = 'flex';
legendContainer.style.alignItems = 'center'; // Align vertically

for (let color of calendarData.colorScheme.gaming) {
    const colorBox = document.createElement('div');
    colorBox.style.width = '9px'; // Reduced box width by 50%
    colorBox.style.height = '9px'; // Reduced box height by 50%
    colorBox.style.backgroundColor = color;
    colorBox.style.marginRight = '5px'; // Adjusted margin
    legendContainer.appendChild(colorBox);
}

// Adding second legend after the colored boxes with reduced size and custom font
const secondLegend = document.createElement('div');
secondLegend.innerText = 'MORE'; // Updated to "MORE" with all caps
secondLegend.style.fontSize = '65%'; // Reduce font size by 50%
secondLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
secondLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
legendContainer.appendChild(secondLegend);

legendsContainer.appendChild(legendContainer);
legendsContainer.style.marginBottom = "12px";

heatmapTrackerEl.appendChild(legendsContainer);

dv.span('GYM tracker statistics:')

renderHeatmapTrackerStatistics(this.container, calendarData)

```
