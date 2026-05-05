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
#### 💤 Sleeping quality 
```dataviewjs
// --- CONFIG ---
const YEAR = 2026;
const MIN = 180;   // threshold
const MAX = 480;   // expected upper bound
const LEVELS = 12; // matches heat3 palette
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

// --- SCALE FUNCTION (robust, bounded) ---
function scaleIntensity(value) {
    if (value == null) return 0;
    const clamped = Math.max(MIN, Math.min(MAX, value));
    return Math.floor((clamped - MIN) / (MAX - MIN) * (LEVELS - 1));
}

// --- BUILD DATA ---
const calendarData = {
    year: YEAR,
    intensityScaleStart: 0,
    intensityScaleEnd: LEVELS,
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "heat3" // ← use predefined palette ONLY
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

// --- QUERY ---
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"')
    .where(p => p.meTime)
    .sort(p => p.file.name, 'asc')) {

    calendarData.entries.push({
        date: page.file.name,
        intensity: scaleIntensity(page.meTime)
    });
}

const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData);
renderInlineLegend(heatmapTrackerEl, heatmapColors, 'Bad', 'Good');
```
