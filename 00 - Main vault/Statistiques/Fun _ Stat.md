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
#### FUN 😋
```dataviewjs
const heatmapColors = [
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
];

const calendarData = { year: 2026,
    intensityScaleStart: 0,
    intensityScaleEnd: 10, // I have 10 color shades in gaming
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "gaming",
    //     "gaming": [
    // "rgb(51, 51, 51)", 
    // "rgb(77, 77, 77)", 
    // "rgb(102, 102, 102)", 
    // "rgb(160, 160, 160)", 
    // "rgb(217, 221, 222)", 
    // "rgb(150, 160, 180)", 
    // "rgb(80, 90, 120)", 
    // "rgb(40, 50, 80)", 
    // "rgb(20, 30, 60)", 
    // "rgb(0, 10, 26)"
// ],
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
        return ((intensity / maxDay) * 9); // Scale to 0-10
    } else {
        return 9; // Assign 10 if intensity is maxDay or greater
    }
};
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.gamingPCMin || p.gamingMobileMin || p.RManga || p.BRead || p.LWRead || p.movieMin || p.animeEp)) {
	let fun = ((page.gamingPCMin||0)/60) + ((page.gamingMobileMin||0)/60) + ((page.movieMin||0)/60) + ((page.animeEp||0)/3) + ((page.BRead||0) + (page.LWRead||0) + (page.RManga||0) + (page.quranReading||0))/10;
	if ( fun == 0) { continue; }
	let scaledIntensity = scaleIntensity(fun,6) + 1; 
    calendarData.entries.push({
        date: page.file.name,
        filePath: page.file.path,
        intensity: scaledIntensity, // Use scaled intensity
//         color:"gaming",
        //content: await dv.span(`[](${page.file.name})`), // For hover preview
    });
}
const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData);
renderInlineLegend(heatmapTrackerEl, heatmapColors, 'LESS', 'MORE');
```

#### ROG Time 🎮
```dataviewjs
const heatmapColors = [
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
];

const calendarData = { year: 2026,
    intensityScaleStart: 0,
    intensityScaleEnd: 10, // I have 10 color shades in gaming
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "gaming",
//         "gaming": [
//     "rgb(51, 51, 51)", 
//     "rgb(77, 77, 77)", 
//     "rgb(102, 102, 102)", 
//     "rgb(160, 160, 160)", 
//     "rgb(217, 221, 222)", 
//     "rgb(150, 160, 180)", 
//     "rgb(80, 90, 120)", 
//     "rgb(40, 50, 80)", 
//     "rgb(20, 30, 60)", 
//     "rgb(0, 10, 26)"
// ],
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
        return ((intensity / maxDay) * 9); // Scale to 0-10
    } else {
        return 9; // Assign 10 if intensity is maxDay or greater
    }
};
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.gamingPCMin)) {
	let fun = page.gamingPCMin/60;
	if ( fun == 0) { continue; }
	let scaledIntensity = scaleIntensity(fun,3) + 1; 
    calendarData.entries.push({
        date: page.file.name,
        intensity: scaledIntensity, // Use scaled intensity
//         color:"gaming",
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
// firstLegend.innerText = 'LESS'; // Updated to "LESS" with all caps
// firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
// firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
// legendsContainer.appendChild(firstLegend);

// // Adding colored boxes with adjusted size
// const legendContainer = document.createElement('div');
// legendContainer.style.display = 'flex';
// legendContainer.style.alignItems = 'center'; // Align vertically

// // for (let color of calendarData.colorScheme.gaming) {
// //     const colorBox = document.createElement('div');
// //     colorBox.style.width = '9px'; // Reduced box width by 50%
// //     colorBox.style.height = '9px'; // Reduced box height by 50%
// //     colorBox.style.backgroundColor = color;
// //     colorBox.style.marginRight = '5px'; // Adjusted margin
// //     legendContainer.appendChild(colorBox);
// // }

// // Adding second legend after the colored boxes with reduced size and custom font
// const secondLegend = document.createElement('div');
// secondLegend.innerText = 'MORE'; // Updated to "MORE" with all caps
// secondLegend.style.fontSize = '65%'; // Reduce font size by 50%
// secondLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// secondLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// legendContainer.appendChild(secondLegend);

// legendsContainer.appendChild(legendContainer);
// legendsContainer.style.marginBottom = "12px";

// heatmapTrackerEl.appendChild(legendsContainer);

// // dv.span('Fun time with my ROG tracker statistics:')

const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData)
renderInlineLegend(heatmapTrackerEl, heatmapColors, 'LESS', 'MORE')
```

#### G-Phone time 👾
```dataviewjs
const heatmapColors = [
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
];

const calendarData = { year: 2026,
    intensityScaleStart: 0,
    intensityScaleEnd: 10, // I have 10 color shades in gaming
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "gaming",
//         "gaming": [
//     "rgb(51, 51, 51)", 
//     "rgb(77, 77, 77)", 
//     "rgb(102, 102, 102)", 
//     "rgb(160, 160, 160)", 
//     "rgb(217, 221, 222)", 
//     "rgb(150, 160, 180)", 
//     "rgb(80, 90, 120)", 
//     "rgb(40, 50, 80)", 
//     "rgb(20, 30, 60)", 
//     "rgb(0, 10, 26)"
// ],
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
        return ((intensity / maxDay) * 9); // Scale to 0-10
    } else {
        return 9; // Assign 10 if intensity is maxDay or greater
    }
};
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.gamingMobileMin)) {
	let fun = page.gamingMobileMin/60;
	if ( fun == 0) { continue; }
	let scaledIntensity = scaleIntensity(fun,2) + 1; 
    calendarData.entries.push({
        date: page.file.name,
        intensity: scaledIntensity, // Use scaled intensity
//         color:"gaming",
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
// firstLegend.innerText = 'LESS'; // Updated to "LESS" with all caps
// firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
// firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
// legendsContainer.appendChild(firstLegend);

// // Adding colored boxes with adjusted size
// const legendContainer = document.createElement('div');
// legendContainer.style.display = 'flex';
// legendContainer.style.alignItems = 'center'; // Align vertically

// // for (let color of calendarData.colorScheme.gaming) {
// //     const colorBox = document.createElement('div');
// //     colorBox.style.width = '9px'; // Reduced box width by 50%
// //     colorBox.style.height = '9px'; // Reduced box height by 50%
// //     colorBox.style.backgroundColor = color;
// //     colorBox.style.marginRight = '5px'; // Adjusted margin
// //     legendContainer.appendChild(colorBox);
// // }

// // Adding second legend after the colored boxes with reduced size and custom font
// const secondLegend = document.createElement('div');
// secondLegend.innerText = 'MORE'; // Updated to "MORE" with all caps
// secondLegend.style.fontSize = '65%'; // Reduce font size by 50%
// secondLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// secondLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// legendContainer.appendChild(secondLegend);

// legendsContainer.appendChild(legendContainer);
// legendsContainer.style.marginBottom = "12px";

// heatmapTrackerEl.appendChild(legendsContainer);

// dv.span('Fun time playing on my phone tracker statistics:')

const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData)
renderInlineLegend(heatmapTrackerEl, heatmapColors, 'LESS', 'MORE')
```

#### Chilling 😜


```dataviewjs
// --- CONFIG ---
const YEAR = 2026;
const LEVELS = 10; // matches heat3 palette

const heatmapColors = [
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
];


const calendarData = { year: YEAR,
    intensityScaleStart: 0,
    intensityScaleEnd: 10, // I have 10 color shades in gaming
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "gaming",
//         "gaming": [
//     "rgb(51, 51, 51)", 
//     "rgb(77, 77, 77)", 
//     "rgb(102, 102, 102)", 
//     "rgb(160, 160, 160)", 
//     "rgb(217, 221, 222)", 
//     "rgb(150, 160, 180)", 
//     "rgb(80, 90, 120)", 
//     "rgb(40, 50, 80)", 
//     "rgb(20, 30, 60)", 
//     "rgb(0, 10, 26)"
// ],
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
        return ((intensity / maxDay) * 9); // Scale to 0-10
    } else {
        return 9; // Assign 10 if intensity is maxDay or greater
    }
};
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.RManga || p.BRead || p.LWRead || p.movieMin || p.animeEp)) {
	let fun = ((page.movieMin||0) / 60) + ((page.animeEp||0) / 3) + ((page.BRead||0) + (page.LWRead||0) + (page.RManga||0) + (page.quranReading||0))/10;
	if ( fun == 0) { continue; }
	let scaledIntensity = scaleIntensity(fun,3) + 1; 
    calendarData.entries.push({
        date: page.file.name,
        intensity: scaledIntensity, // Use scaled intensity
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
// firstLegend.innerText = 'LESS'; // Updated to "LESS" with all caps
// firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
// firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
// legendsContainer.appendChild(firstLegend);

// // Adding colored boxes with adjusted size
// const legendContainer = document.createElement('div');
// legendContainer.style.display = 'flex';
// legendContainer.style.alignItems = 'center'; // Align vertically

// // for (let color of calendarData.colorScheme.gaming) {
// //     const colorBox = document.createElement('div');
// //     colorBox.style.width = '9px'; // Reduced box width by 50%
// //     colorBox.style.height = '9px'; // Reduced box height by 50%
// //     colorBox.style.backgroundColor = color;
// //     colorBox.style.marginRight = '5px'; // Adjusted margin
// //     legendContainer.appendChild(colorBox);
// // }

// // Adding second legend after the colored boxes with reduced size and custom font
// const secondLegend = document.createElement('div');
// secondLegend.innerText = 'MORE'; // Updated to "MORE" with all caps
// secondLegend.style.fontSize = '65%'; // Reduce font size by 50%
// secondLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// secondLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// legendContainer.appendChild(secondLegend);

// legendsContainer.appendChild(legendContainer);
// legendsContainer.style.marginBottom = "12px";

// heatmapTrackerEl.appendChild(legendsContainer);

// dv.span('Fun time tracker statistics:')

const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData);
renderInlineLegend(heatmapTrackerEl, heatmapColors, 'LESS', 'MORE');
```