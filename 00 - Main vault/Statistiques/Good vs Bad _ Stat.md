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
$$
\text{Balance In life} = \sum (\text{Time}_1 \text{ allowed} - \text{Official activities}) + \sum (\text{Fun activities}  - \text{Time}_2 \text{ allowed}) + \frac{\text{GYM activities}}{\text{avg expected}} + \frac{\text{Money spent}}{\text{daily}}
$$

```dataviewjs
const calendarData = {
    intensityScaleStart: 0,
    intensityScaleEnd: 12, // I have 12 color levels in heat
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "heat",
        "heat": [
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
      "rgb(0, 10, 51)",
    ],
    }
};
function scaleIntensity(intensity,maxDay) {
    if (intensity < maxDay) {
        return Math.floor((intensity / maxDay) * 5); // Scale to 0-6
    } else {
        return 5; // Assign 6 if intensity is maxDay or greater
    }
};
function capMax(value,maxVal) {
    if (Math.abs(value) < Math.abs(maxVal)) {
        return value;
    } else {
        return value >= 0 ? maxVal : -maxVal; 
    }
};
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.moneyInDh || p.meTime || p.salatOnTime)) {
	let lifeQuality = capMax((((page.dailyDh||0)-page.moneyInDh)/(page.dailyDh||1)),3) +(page.meTime||0)/60-6 -(page.bTime)*5 -capMax((page.ScreenTime||1)/(page.UnlockNbr||1),2) -(page.smMin||0)/((page.Fb||1)+(page.Insta||1)) +(page.gamingPCMin||0)/(60*3) -((page.gamingMobileMin||0)/60) +(page.animeEp||0)/(3*6) +(page.travelingDist||0)/5 +6-((page.hWork||0)/60) +4-((page.oWork||0)/60) +4-((page.pWork||0)/60) +((page.salatOnTime||0)/5)-5 + (page.pushUpReps||0)/100 + (page.setUpReps||0)/100 + (page.squadReps||0)/100;
	let scaledIntensity = scaleIntensity(Math.abs(lifeQuality),20); 
	let intensityVal = lifeQuality >= 0 ? scaledIntensity + 1 : 7 + scaledIntensity;
	//dv.span(page.file.name+': '+moneyInDh+'<=>'+intensityVal+'<br>');
    calendarData.entries.push({
        date: page.file.name,
        intensity: intensityVal, // Use scaled intensity
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

dv.span('Overall balance tracker statistics:')

renderHeatmapTrackerStatistics(this.container, calendarData)
```
