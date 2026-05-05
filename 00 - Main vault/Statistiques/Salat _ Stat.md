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
const heatmapColors = [
    "rgb(51, 51, 51)",
    "rgb(77, 77, 77)",
    "rgb(102, 102, 102)",
    "rgb(128, 128, 128)",
    "rgb(153, 153, 153)",
    "rgb(255, 255, 255)"
];

const calendarData = { year: 2026,
    intensityScaleStart: 0,
//     monthsToShow:12,
//     layout:"monthly",
    intensityScaleEnd: 5, // I have 12 color levels in heat
    entries: [],
    separateMonths: true,
    colorScheme: {
        customColors: heatmapColors,
    }
};

function renderInlineLegend(container, colors, minLabel, maxLabel) {
    const legendsContainer = container.createDiv();
    legendsContainer.style.display = "flex";
    legendsContainer.style.alignItems = "center";
    legendsContainer.style.justifyContent = "center";
    legendsContainer.style.width = "100%";
    legendsContainer.style.marginBottom = "12px";
    legendsContainer.style.gap = "5px";

    const createLabel = (text) => {
        const label = legendsContainer.createDiv({ text });
        label.style.fontSize = "65%";
        label.style.fontFamily = "IBM plex mono, sans-serif";
        label.style.textTransform = "uppercase";
        return label;
    };

    createLabel(minLabel);

    const colorsContainer = legendsContainer.createDiv();
    colorsContainer.style.display = "flex";
    colorsContainer.style.alignItems = "center";
    colorsContainer.style.gap = "5px";

    for (const color of colors) {
        const colorBox = colorsContainer.createDiv();
        colorBox.style.width = "9px";
        colorBox.style.height = "9px";
        colorBox.style.backgroundColor = color;
    }

    createLabel(maxLabel);
}

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
//         color:"work",
        //content: await dv.span(`[](${page.file.name})`), // For hover preview
    });
}
const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData)
renderInlineLegend(heatmapTrackerEl, heatmapColors, "Less", "More")
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
    if (!currentDate) continue;
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
const heatmapColors = [
    "rgb(51, 51, 51)",
    "rgb(77, 77, 77)",
    "rgb(102, 102, 102)",
    "rgb(128, 128, 128)",
    "rgb(153, 153, 153)",
    "rgb(255, 255, 255)"
];

const calendarData = { year: 2026,
    intensityScaleStart:1,
    entries: [],
    separateMonths: true,
    colorScheme: {
        customColors: heatmapColors,
    }
};

function renderInlineLegend(container, colors, minLabel, maxLabel) {
    const legendsContainer = container.createDiv();
    legendsContainer.style.display = "flex";
    legendsContainer.style.alignItems = "center";
    legendsContainer.style.justifyContent = "center";
    legendsContainer.style.width = "100%";
    legendsContainer.style.marginBottom = "12px";
    legendsContainer.style.gap = "5px";

    const createLabel = (text) => {
        const label = legendsContainer.createDiv({ text });
        label.style.fontSize = "65%";
        label.style.fontFamily = "IBM plex mono, sans-serif";
        label.style.textTransform = "uppercase";
        return label;
    };

    createLabel(minLabel);

    const colorsContainer = legendsContainer.createDiv();
    colorsContainer.style.display = "flex";
    colorsContainer.style.alignItems = "center";
    colorsContainer.style.gap = "5px";

    for (const color of colors) {
        const colorBox = colorsContainer.createDiv();
        colorBox.style.width = "9px";
        colorBox.style.height = "9px";
        colorBox.style.backgroundColor = color;
    }

    createLabel(maxLabel);
}

for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.quranReading)) {
	let quranReading = (page.quranReading||0) + (page.quranReadingO||0) + (page.quranReadingE||0);
	if ( quranReading == 0) { continue; }
	calendarData.entries.push({
        date: page.file.name,
        intensity: quranReading, 
//         color:"work",
        //content: await dv.span(`[](${page.file.name})`), // For hover preview
    });
}
const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData)
renderInlineLegend(heatmapTrackerEl, heatmapColors, "Less", "More")
```
