---
tags:
  - Annually
banner: "[[Sky3Banner.jpg]]"
banner_x: 0
banner_y: 0.906
cssclasses:
  - daily
isCompleted:
---

[[00 - Main vault/Notes/Annually reports/<%moment(tp.file.title).subtract(1,'year').format("YYYY")%>|⬅️]]|[[00 - Main vault/Notes/Annually reports/<%moment(tp.file.title).add(1,'year').format("YYYY")%>|➡️]]

Browse each month individually:
[[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title).startOf('Month').add(0,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(0,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title).startOf('Month').add(1,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(1,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title).startOf('Month').add(2,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(2,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title).startOf('Month').add(3,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(3,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title).startOf('Month').add(4,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(4,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title).startOf('Month').add(5,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(5,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title).startOf('Month').add(6,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(6,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title).startOf('Month').add(7,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(7,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title).startOf('Month').add(8,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(8,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title).startOf('Month').add(9,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(9,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title).startOf('Month').add(10,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(10,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title).startOf('Month').add(11,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(11,'month').format("MMM")%>]]
***
***

### Summary about the year 🗒️
- [ ] Add summary of the year <%moment(tp.file.title).format("YYYY")%> here ⏬  
***
***
### ** 🙏 Salat 🛐 **
```dataviewjs
const calendarData = {
    year: <%moment(tp.file.title).format("YYYY")%>,
    intensityScaleStart: 0,
    intensityScaleEnd: 5, // I have 12 color levels in heat
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "work",
        "work": [
      "rgb(128, 138, 166)",
      "rgb(77, 90, 128)",
      "rgb(51, 64, 114)",
      "rgb(25, 38, 99)",
      "rgb(0, 18, 77)",
      "rgb(0, 10, 51)"
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

***

### ** ✔️ Tasks 📆 **
```dataviewjs
const calendarData = {
    year: <%moment(tp.file.title).format("YYYY")%>,
    intensityScaleStart: 0,
    intensityScaleEnd: 10, // I have 6 shades levels
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "danger",
        "danger": [
      "rgb(255, 204, 204)",  
      "rgb(255, 153, 153)",  
      "rgb(255, 102, 102)",  
      "rgb(255, 51, 51)",    
      "rgb(255, 0, 0)",      
      "rgb(204, 0, 0)",      
      "rgb(153, 0, 0)",      
      "rgb(102, 0, 0)",      
      "rgb(51, 0, 0)",      
      "rgb(25, 0, 0)"
    ],
    }
};
function scaleIntensity(intensity,maxDay) {
    if (intensity < maxDay) {
        return Math.floor((intensity / maxDay) * 9); // Scale to 0-5
    } else {
        return 9; // Assign 5 if intensity is maxDay or greater
    }
};
let tasks = dv.pages('"00 - Main vault/Notes/Daily Notes"').file.tasks.filter(t => t.due && t.due.year === 2025);
let taskCounts = {}; 
for (let task of tasks) { 
	let dueDate = task.due.toISODate(); 
	taskCounts[dueDate] = (taskCounts[dueDate] || 0) + 1; 
	}
for (let [date, count] of Object.entries(taskCounts)) {
	let scaledIntensity = scaleIntensity(count, 7); // Adjust maxValue as needed 
	calendarData.entries.push({ 
		date: date, 
		intensity: scaledIntensity +1, 
		color: "danger",  
		content: await dv.span(`[](${date})`),
		}); 
	}
	//let moneyInDh = page.moneyInDh;
	//let scaledIntensity = scaleIntensity(Math.abs(moneyInDh),6); //500 is daily salery
	//let intensityVal = moneyInDh >= 0 ? scaledIntensity + 1 : 7 + scaledIntensity;
    //calendarData.entries.push({
      //  date: page.file.name,
        //intensity: intensityVal, // Use scaled intensity
        //color:"heat",
        //content: await dv.span(`[](${page.file.name})`), // For hover preview
    //});
//}
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
firstLegend.innerText = 'Free'; // Updated to "LESS" with all caps
firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
legendsContainer.appendChild(firstLegend);

// Adding colored boxes with adjusted size
const legendContainer = document.createElement('div');
legendContainer.style.display = 'flex';
legendContainer.style.alignItems = 'center'; // Align vertically

for (let color of calendarData.colorScheme.danger) {
    const colorBox = document.createElement('div');
    colorBox.style.width = '9px'; // Reduced box width by 50%
    colorBox.style.height = '9px'; // Reduced box height by 50%
    colorBox.style.backgroundColor = color;
    colorBox.style.marginRight = '5px'; // Adjusted margin
    legendContainer.appendChild(colorBox);
}

// Adding second legend after the colored boxes with reduced size and custom font
const secondLegend = document.createElement('div');
secondLegend.innerText = 'Busy'; // Updated to "MORE" with all caps
secondLegend.style.fontSize = '65%'; // Reduce font size by 50%
secondLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
secondLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
legendContainer.appendChild(secondLegend);

legendsContainer.appendChild(legendContainer);
legendsContainer.style.marginBottom = "12px";

heatmapTrackerEl.appendChild(legendsContainer);

dv.span('Tasks tracker statistics:')

renderHeatmapTrackerStatistics(this.container, calendarData)
```

***

### ** 👨‍🏫 Work 👨‍💼**
```dataviewjs
const calendarData = {
    year: <%moment(tp.file.title).format("YYYY")%>,
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
	let scaledIntensity = scaleIntensity(Math.abs(workHH),10) +1; //500 is daily salery
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

// Display totals in the note
dv.paragraph(`👨‍🎓 **${hWork}h**: Self-improvements   
👨‍💼 **${oWork}h**: Official work   
👨‍🏫 **${rWork}h**: Research work `);

```
For this year <%moment(tp.file.title).format("YYYY")%>:
```tracker
searchType: dvField
searchTarget: hWork, rWork, oWork
datasetName: Self-improvements, Research work, Official work
startDate: <%moment(tp.file.title).startOf('Month').add(0,'month').format("YYYY-MM-DD")%>
endDate: <%moment(tp.file.title).endOf('Month').add(11,'month').format("YYYY-MM-DD")%>
pie:
    title: Time management
    label: '{{sum(dataset(0))/sum(dataset(0)+dataset(1)+dataset(2))*100}}%,{{sum(dataset(1))/sum(dataset(0)+dataset(1)+dataset(2))*100}}%,{{sum(dataset(2))/sum(dataset(0)+dataset(1)+dataset(2))*100}}%'
    data: '{{sum(dataset(0))}},{{sum(dataset(1))}},{{sum(dataset(2))}}'
    dataColor: '#4daf4a,#377eb8,#ff7f00'
    ratioInnerRadius: 0.6
    dataName: Self-improvements, Research work, Official work
    showLegend: true
    legendPosition: right
    legendOrientation: vertical	
```
***

### ** 💪 GYM 🏋️‍♂️**
```dataviewjs
const calendarData = {
    year: <%moment(tp.file.title).format("YYYY")%>,
    intensityScaleStart: 0,
    intensityScaleEnd: 10, // I have 10 color shades in gaming
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "gaming",
        "gaming": [
      "rgb(217, 221, 230)",
      "rgb(179, 186, 204)",
      "rgb(140, 152, 179)",
      "rgb(102, 119, 153)",
      "rgb(77, 92, 128)",
      "rgb(51, 67, 102)",
      "rgb(25, 41, 77)",
      "rgb(1, 31, 75)",
      "rgb(0, 21, 51)",
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
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.gymMin || p.pushUpReps || p.setUpReps || p.squadReps || p.runingKm )) {
	let fun = (page.gymMin / 90) + ((page.pushUpReps / 100) + (page.setUpReps / 100) + (page.squadReps / 100))/3 + (page.runingKm / 2);
	if ( fun == 0) { continue; }
	let scaledIntensity = scaleIntensity(fun,3) +1; //500 is daily salery
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

### ** ⚖️ Weight & Height 📏 **
Globaly, my weight statistics:
``` tracker
searchType: dvField
searchTarget: myWeight
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <%moment(tp.file.title).startOf('Month').add(0,'month').format("YYYY-MM-DD")%>
endDate: <%moment(tp.file.title).endOf('Month').add(11,'month').format("YYYY-MM-DD")%>
summary:
    template: "Last: {{last()}}kg\nMinimum: {{min()}}kg\nMaximum: {{max()}}kg"
```
__
While for my height
``` tracker
searchType: dvField
searchTarget: myHeight
startDate: <%moment(tp.file.title).startOf('Month').add(0,'month').format("YYYY-MM-DD")%>
endDate: <%moment(tp.file.title).endOf('Month').add(11,'month').format("YYYY-MM-DD")%>
folder: "00 - Main vault/Notes/Daily Notes"
summary:
    template: "Last: {{last()}}cm\nMinimum: {{min()}}cm\nMaximum: {{max()}}cm"
```

***

### ** 🎮 Fun 👾**
```dataviewjs
const calendarData = {
    year: <%moment(tp.file.title).format("YYYY")%>,
    intensityScaleStart: 0,
    intensityScaleEnd: 10, // I have 10 color shades in gaming
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "gaming",
        "gaming": [
      "rgb(217, 221, 230)",
      "rgb(179, 186, 204)",
      "rgb(140, 152, 179)",
      "rgb(102, 119, 153)",
      "rgb(77, 92, 128)",
      "rgb(51, 67, 102)",
      "rgb(25, 41, 77)",
      "rgb(1, 31, 75)",
      "rgb(0, 21, 51)",
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
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.smMin || p.gamingMin || p.movieMin || p.animeEp)) {
	let fun = (page.smMin / 60) + (page.gamingMin / 60) + (page.movieMin / 60) + (page.animeEp / 3) + (page.rwROG / 60);
	if ( fun == 0) { continue; }
	let scaledIntensity = scaleIntensity(fun,16) + 1; 
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

dv.span('Fun time tracker statistics:')

renderHeatmapTrackerStatistics(this.container, calendarData)
```

***

### **💸 Money spending 💸**
````dataviewjs
const calendarData = {
    year: <%moment(tp.file.title).format("YYYY")%>,
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
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.moneyInDh)) {
	let moneyInDh = page.moneyInDh;
	let scaledIntensity = scaleIntensity(Math.abs(moneyInDh),500); //500 is daily salery
	let intensityVal = moneyInDh >= 0 ? scaledIntensity + 1 : 7 + scaledIntensity;
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
````

***

### ** 😴 Sleeping & Mood 😏 **
A healthy brain in a healthy body 💤
```dataviewjs
const calendarData = {
    year: <%moment(tp.file.title).format("YYYY")%>,
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
for (let page of dv.pages('"00 - Main vault/Notes/Daily Notes"').where(p => p.meTime)) {
	if ( page.bTime > 0) { continue; }
	let meTime = page.gTime ? page.meTime : 0 -page.meTime;
	let scaledIntensity = scaleIntensity(Math.abs(meTime),6); //500 is daily salery
	let intensityVal = meTime >= 0 ? scaledIntensity + 1 : 7 + scaledIntensity;
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
