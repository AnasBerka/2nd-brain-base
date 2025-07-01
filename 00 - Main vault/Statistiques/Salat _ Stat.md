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
#### Salat streaks
```dataviewjs
const calendarData = {
    intensityScaleStart: 0,
    intensityScaleEnd: 5, // I have 12 color levels in heat
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "activate",
        "work": [
    "rgb(51, 51, 51)", 
    "rgb(77, 77, 77)", 
    "rgb(102, 102, 102)", 
    "rgb(128, 128, 128)", 
    "rgb(153, 153, 153)", 
    "rgb(255, 255, 255)"
],
    }
};
function scaleIntensity(intensity,maxDay) {
    if (intensity < maxDay) {
        return Math.floor((intensity / maxDay) * 5); // Scale to 0-5
    } else {
        return 5; // Assign 5 if intensity is maxDay or greater
    }
};
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.salatOnTime)) {
	let salatOnTime = (page.salatOnTime + Number(page.salatFajer) + Number(page.salatDohr) + Number(page.salatAaser) + Number(page.salatMeghrb) + Number(page.salatIshae)) / 2;
	if ( salatOnTime == 0) { continue; }
	if ( (Number(page.salatFajer) + Number(page.salatDohr) + Number(page.salatAaser) + Number(page.salatMeghrb) + Number(page.salatIshae)) == 0) { continue; }
	let scaledIntensity = scaleIntensity(Math.abs(salatOnTime),5); //5 prayers
	calendarData.entries.push({
        date: page.file.name,
        intensity: scaledIntensity, // Use scaled intensity
        color:"work",
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
firstLegend.innerText = 'Evil'; // Updated to "LESS" with all caps
firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
legendsContainer.appendChild(firstLegend);

// Adding colored boxes with adjusted size
const legendContainer = document.createElement('div');
legendContainer.style.display = 'flex';
legendContainer.style.alignItems = 'center'; // Align vertically

for (let color of calendarData.colorScheme.work) {
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

dv.span('Salat tracker statistics:')

renderHeatmapTrackerStatistics(this.container, calendarData)
```
#### Streak Counter and Last Value
```dataviewjs
// Define the variable key to track
const variableKey = "Quran/7izb"; // Change this to your actual variable name

// Get all pages that contain the variable
let pages = dv.pages('"00 - Main vault/Notes/Daily Notes"').filter(p => p[variableKey] !== undefined);

// Sort pages by date (assuming your pages have a `date` field)
pages = pages.sort(p => p.file.name);

// Initialize streak variables
let streak = 0, lastStreak = 0, nonStop=true;
let lastValue = null;
let lastDate = null;

// Iterate through sorted pages to calculate streak
for (let i = 0; i < pages.length; i++) {
    let currentDate = dv.date(pages[i].file.name); // Extract date from file name
    let value = pages[i][variableKey];
    if (value === undefined || value === null){
	    nonStop = false;
	    lastStreak = streak !=0 ? streak:lastStreak;
	    streak = 0;
	    continue;
    }
    nonStop = true;
    // Store the last logged value and its date
    lastValue = value;
    lastDate = currentDate.toISODate(); // Convert to YYYY-MM-DD

    // Check if the streak is consecutive
    if (i > 0) {
        let previousDate = dv.date(pages[i - 1].file.name);
        let expectedDate = previousDate.plus({ days: 1 });

        if (currentDate.equals(expectedDate)) {
            streak++;
        } else {
            streak = 1; // Reset streak if there's a gap
        }
    } else {
        streak = 1; // Start streak at 1 for the first entry
    }
}

// Display results
if(nonStop){
	dv.paragraph(`**Current Streak:** ${streak} days`);
}else{
	dv.paragraph(`**Last Streak:** ${lastStreak} days`);
}
dv.paragraph(`**Last Logged Value:** ${lastValue} (on ${lastDate})`);

```


#### Quran reading streaks
```dataviewjs
const calendarData = {
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "activate",
        "work": [
    "rgb(51, 51, 51)", 
    "rgb(77, 77, 77)", 
    "rgb(102, 102, 102)", 
    "rgb(128, 128, 128)", 
    "rgb(153, 153, 153)", 
    "rgb(255, 255, 255)"
],
    }
};

for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.quranReading)) {
	let quranReading = page.quranReading;
	if ( quranReading == 0) { continue; }
	calendarData.entries.push({
        date: page.file.name,
        intensity: quranReading, 
        color:"work",
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
firstLegend.innerText = 'Evil'; // Updated to "LESS" with all caps
firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
legendsContainer.appendChild(firstLegend);

// Adding colored boxes with adjusted size
const legendContainer = document.createElement('div');
legendContainer.style.display = 'flex';
legendContainer.style.alignItems = 'center'; // Align vertically

for (let color of calendarData.colorScheme.work) {
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

dv.span('Salat tracker statistics:')

renderHeatmapTrackerStatistics(this.container, calendarData)
```
