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

```dataviewjs
const calendarData = {
    intensityScaleStart: 0,
    intensityScaleEnd: 12, // I have 12 color levels in heat
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "heat3",
        "heat": [
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
],
    }
};
function scaleIntensity(intensity,maxDay) {
    if (intensity < maxDay) return 0;
    return Math.floor(1+11*(intensity-180)/300);//(intensity/480)*12); 
};
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.meTime).sort(p => p.file.name, 'dsc')) {
	let meTime = page.meTime;
	let scaledIntensity = scaleIntensity(meTime,180);
    calendarData.entries.push({
        date: page.file.name,
        intensity: scaledIntensity, // Use scaled intensity
        color:"heat",
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
firstLegend.innerText = 'Bad'; // Updated to "LESS" with all caps
firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
legendsContainer.appendChild(firstLegend);

// Adding colored boxes with adjusted size
const legendContainer = document.createElement('div');
legendContainer.style.display = 'flex';
legendContainer.style.alignItems = 'center'; // Align vertically

for (let color of calendarData.colorScheme.heat) {
    const colorBox = document.createElement('div');
    colorBox.style.width = '9px'; // Reduced box width by 50%
    colorBox.style.height = '9px'; // Reduced box height by 50%
    colorBox.style.backgroundColor = color;
    colorBox.style.marginRight = '5px'; // Adjusted margin
    legendContainer.appendChild(colorBox);
}

// Adding second legend after the colored boxes with reduced size and custom font
const secondLegend = document.createElement('div');
secondLegend.innerText = 'Good'; // Updated to "MORE" with all caps
secondLegend.style.fontSize = '65%'; // Reduce font size by 50%
secondLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
secondLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
legendContainer.appendChild(secondLegend);

legendsContainer.appendChild(legendContainer);
legendsContainer.style.marginBottom = "12px";

heatmapTrackerEl.appendChild(legendsContainer);

dv.span('Relaxing tracker statistics:')

renderHeatmapTrackerStatistics(this.container, calendarData)
```