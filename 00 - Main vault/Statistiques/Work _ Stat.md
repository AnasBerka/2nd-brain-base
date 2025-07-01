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

```dataviewjs
const calendarData = {
    intensityScaleStart: 0,
    intensityScaleEnd: 10, // I have 12 color levels in heat
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "metime",
        "metime": [
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
    ],
    }
};
function scaleIntensity(intensity,maxDay) {
    if (intensity < maxDay) {
        return Math.floor((intensity / maxDay) * 9); // Scale to 0-6
    } else {
        return 9; // Assign 6 if intensity is maxDay or greater
    }
};
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.hWork || p.oWork || p.rWork)) {
	let workHH = page.hWork + page.oWork + page.rWork;
	if (workHH === 0) {continue;}
	let scaledIntensity = scaleIntensity(Math.abs(workHH),10*60) +1; //500 is daily salery
    calendarData.entries.push({
        date: page.file.name,
        intensity: scaledIntensity, // Use scaled intensity
        color:"metime",
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
firstLegend.innerText = 'Less'; // Updated to "LESS" with all caps
firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
legendsContainer.appendChild(firstLegend);

// Adding colored boxes with adjusted size
const legendContainer = document.createElement('div');
legendContainer.style.display = 'flex';
legendContainer.style.alignItems = 'center'; // Align vertically

for (let color of calendarData.colorScheme.metime) {
    const colorBox = document.createElement('div');
    colorBox.style.width = '9px'; // Reduced box width by 50%
    colorBox.style.height = '9px'; // Reduced box height by 50%
    colorBox.style.backgroundColor = color;
    colorBox.style.marginRight = '5px'; // Adjusted margin
    legendContainer.appendChild(colorBox);
}

// Adding second legend after the colored boxes with reduced size and custom font
const secondLegend = document.createElement('div');
secondLegend.innerText = 'More'; // Updated to "MORE" with all caps
secondLegend.style.fontSize = '65%'; // Reduce font size by 50%
secondLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
secondLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
legendContainer.appendChild(secondLegend);

legendsContainer.appendChild(legendContainer);
legendsContainer.style.marginBottom = "12px";

heatmapTrackerEl.appendChild(legendsContainer);

dv.span('Working tracker statistics:')

renderHeatmapTrackerStatistics(this.container, calendarData)
```
Up till now, we got a total of:
```dataviewjs
const pages = dv.pages('"00 - Main vault/Notes/Daily Notes"');  
let hWork = 0, oWork = 0, rWork = 0;

for (let p of pages) {
    hWork += p.hWork || 0;
    oWork += p.oWork || 0;
    rWork += p.rWork || 0;
}

// Convert minutes to "Xh Ym" format
const formatTime = (minutes) => {
    const hours = Math.floor(minutes / 60);
    const mins = minutes % 60;
    return `${hours}h ${mins}m`;
};

// Display totals in the note
dv.paragraph(`👨‍💼 **${formatTime(hWork)}**:\t Self-improvements   
👨‍🏫 **${formatTime(oWork)}**:\t Official work   
👨‍🎓 **${formatTime(rWork)}**:\t Research work `);
```

