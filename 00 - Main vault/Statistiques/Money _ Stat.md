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
        paletteName: "heat2",
        "heat2": [
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
    "heat3": [
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
]   
    }
};
function scaleIntensity(money, sDay) {
    if (sDay <= 0) return 0; // I'm in dept => big problem 
    if (money <= -sDay) return 1; // bad values
    if (money > (2*sDay)) return 11;
    return Math.floor(((money+sDay) / (2*sDay)) * 11);
}
function scaleIntensity2(money, ADay) {
  if (ADay <= 0) return 0;  // I'm in dept => big problem 

  if (money < -ADay) return 1;
  if (money > (2*ADay)) return 11;
  if (money === ADay) return 6;

  if (money < 0) {
    const ratio = 1-(money/ADay);
    return Math.round(ratio * 5);
  } else {
    const ratio = money/ADay;
    return 7 + Math.round(ratio * 4);
  }
}
// Function to get the 7th day's dailyDh
function get7thDayDailyDh(targetDate) {
    let year = targetDate.year;
    let month = targetDate.month;

    // If before the 7th, get from previous month
    if (targetDate.day < 7) {
        month -= 1;
        if (month < 1) {
            month = 12;
            year -= 1;
        }
    }

    let seventhDayStr = `${year}-${String(month).padStart(2, '0')}-07`;
    let refEntry = dv.pages('"00 - Main vault/Notes/Daily Notes"')
        .where(p => p.file.name === seventhDayStr)
        .first();
	//dv.span(seventhDayStr+' '+((refEntry||0) && typeof refEntry.dailyDh === 'number' ? (refEntry.dailyDh.toFixed(2) ||0) : 69) +' ')
    return (refEntry||0) && typeof refEntry.dailyDh === 'number' ? (refEntry.dailyDh ||0) : 69; // Default to 50 if not found
}
let msg = ''
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.moneyInDh || p.meTime).sort(p => p.file.name, 'asc')) {
    let moneyInDh = (page.moneyInDh || 0) + (page.vAnasBerka || 0);
    let pageDate = dv.date(page.file.name); // Extract the date from the filename

	 // Get the 7th day's value as default
    let defaultDailyDh = get7thDayDailyDh(pageDate);

    // Ensure pastEntries is always an array
    let pastEntries = Array.from(dv.pages('"00 - Main vault/Notes/Daily Notes"')
        .where(p => p.moneyInDh || p.meTime)
        .filter(p => {
            let entryDate = dv.date(p.file.name).toMillis();
            return entryDate >= pageDate.toMillis() - (29 * 24 * 60 * 60 * 1000) && entryDate <= pageDate.toMillis();// + (24 * 60 * 60 * 1000) && entryDate;
        }).sort(p => p.file.name, 'asc')
    );

    let sumDailyDh = 0;
    let countDailyDh = 0, ctr=0;
	//dv.span('<br>')
    for (let pp of pastEntries) {
	    defaultDailyDh = get7thDayDailyDh(dv.date(pp.file.name));
        let value = (pp.dailyDh !== undefined && pp.dailyDh !== null) ? pp.dailyDh : defaultDailyDh;
        sumDailyDh += (value + (pp.moneyInDh||0) + (pp.vAnasBerka||0));
        countDailyDh++; // Now always counts valid numbers
        //dv.span('On: [['+p.file.name+']] M='+value+' S '+((p.moneyInDh||0) + (p.vAnasBerka||0))+' Ctr '+countDailyDh+'<br>')
    }
    if(countDailyDh<30){
	    let fix = 30 - countDailyDh;
	    ctr = countDailyDh;
	    countDailyDh+=fix;
	    sumDailyDh+= (fix*defaultDailyDh)
    }else{
	    ctr=countDailyDh;
    }
    let dailyDhA = countDailyDh > 0 ? sumDailyDh / countDailyDh : defaultDailyDh; // Use default if no past data
	let dailyDh = (p.dailyDh !== undefined && p.dailyDh !== null) ? p.dailyDh : defaultDailyDh;
	if ((moneyInDh+dailyDhA) <= 3 && (moneyInDh+dailyDhA) >= -2) { continue; }

    // Compute intensity
    let scaledIntensity = scaleIntensity((moneyInDh + dailyDhA), dailyDh);
		//dv.span(
		msg += "[["+page.file.name+']]\t_M '+ moneyInDh +'\t_DDh '+dailyDh.toFixed(2)+'\t_DDhA '+dailyDhA.toFixed(2)+'\t_SumDh '+sumDailyDh.toFixed(2)+'\t_CNbr '+ctr+'<br>'//+' C'+scaledIntensity
    // Push data to calendar
    calendarData.entries.push({
        date: page.file.name,
        intensity: scaledIntensity,
        color: "heat",
        content: await dv.span(`[](${page.file.name})`),
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
firstLegend.innerText = 'Spending'; // Updated to "LESS" with all caps
firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
legendsContainer.appendChild(firstLegend);

// Adding colored boxes with adjusted size
const legendContainer = document.createElement('div');
legendContainer.style.display = 'flex';
legendContainer.style.alignItems = 'center'; // Align vertically

for (let color of calendarData.colorScheme.heat2) {
    const colorBox = document.createElement('div');
    colorBox.style.width = '9px'; // Reduced box width by 50%
    colorBox.style.height = '9px'; // Reduced box height by 50%
    colorBox.style.backgroundColor = color;
    colorBox.style.marginRight = '5px'; // Adjusted margin
    legendContainer.appendChild(colorBox);
}

// Adding second legend after the colored boxes with reduced size and custom font
const secondLegend = document.createElement('div');
secondLegend.innerText = 'Saving'; // Updated to "MORE" with all caps
secondLegend.style.fontSize = '65%'; // Reduce font size by 50%
secondLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
secondLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
legendContainer.appendChild(secondLegend);

legendsContainer.appendChild(legendContainer);
legendsContainer.style.marginBottom = "12px";

heatmapTrackerEl.appendChild(legendsContainer);

dv.span('Money spending tracker statistics:')

renderHeatmapTrackerStatistics(this.container, calendarData)

dv.span(msg)

```
