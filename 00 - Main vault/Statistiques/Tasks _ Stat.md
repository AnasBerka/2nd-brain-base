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

```dataviewjs
const calendarData = {
    intensityScaleStart: 0,
    intensityScaleEnd: 12, // I have 7 shades levels
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "heat3",
        "danger": [
		    "rgb(51, 51, 51)", 
		    "rgb(77, 26, 26)", 
		    "rgb(102, 26, 26)", 
		    "rgb(127, 38, 38)", 
		    "rgb(153, 51, 51)", 
		    "rgb(181, 61, 61)", 
		    "rgb(255, 0, 0)"
			],
		"work": [
	      "rgb(128, 138, 166)",
	      "rgb(77, 90, 128)",
	      "rgb(51, 64, 114)",
	      "rgb(25, 38, 99)",
	      "rgb(0, 18, 77)",
	      "rgb(0, 10, 51)"
	    ],
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
function scaleIntensity(count, isNotDone, date) {
	//dv.span(date+'  '+count+' '+isNotDone);
    if (isNotDone) {
	    //dv.span(' -C'+(count)+'<br>');
        return 6-count;
    } else {
	    //dv.span(' +C'+(count)+'<br>');
        return 5+count; 
    }
};

// Extraction des pages dans les dossiers spécifiés
let pages = dv.pages()
    .where(p => p.file.path.startsWith("00 - Main vault/Notes") 
             || p.file.path.startsWith("00 - Main vault/Meetings"));

// Extraction des tâches ayant une date programmée ou une date d'échéance et ajout du nom de fichier
let tasks = pages.flatMap(p => p.file.tasks
    .filter(t => t.scheduled || t.due)
    .map(t => ({ ...t, fileName: p.file.name })));
// Initialisation des dictionnaires pour chaque état
let doneTasks = {};
let notDoneTasks = {};
let cancelledTasks = {};

// Fonction d'incrémentation dans le dictionnaire correspondant
function addTask(dict, dateKey, task, nonDone, count) {
    dict[dateKey] = {count:count[dateKey],isNotDone:nonDone, task:task[dateKey]}
}

// Répartition des tâches selon leur état
let ctrC={}, ctrD={}, ctrO={};
let tC={}, tD={}, tO={};

tasks.forEach(t => {
    // Priorité : utiliser la date programmée si présente, sinon la date d'échéance
    let dateKey = t.scheduled ? t.scheduled.toISODate() : t.due.toISODate();
    if (t.text.includes('❌')) {
	    ctrC[dateKey] = (ctrC[dateKey] || 0) + 1;
        tC[dateKey] = (tC[dateKey] || '') +'<li>' + t.text +'</li>';
        addTask(cancelledTasks, dateKey, tC, true, ctrC);
    } else if (t.completed) {
        ctrD[dateKey] = (ctrD[dateKey] || 0) + 1;
        tD[dateKey] = (tD[dateKey] || '') +'<li>' + t.text +'</li>';
        addTask(doneTasks, dateKey, tD, false, ctrD);
    } else {
	    ctrO[dateKey] = (ctrO[dateKey] || 0) + 1;
        tO[dateKey] = (tO[dateKey] || '') +'<li>' + t.text +'</li>';
        addTask(notDoneTasks, dateKey, tO, true, ctrO);
    }
});

// Construction de l'ensemble des dates présentes dans les trois dictionnaires
let finalDict = {};
let dates = new Set([
  ...Object.keys(doneTasks),
  ...Object.keys(notDoneTasks),
  ...Object.keys(cancelledTasks)
]);

dates.forEach(dateKey => {
  let nonDone = (notDoneTasks[dateKey] ? (notDoneTasks[dateKey]['count']||0):0);
  finalDict[dateKey] = nonDone > 0 ? nonDone : ((doneTasks[dateKey]?(doneTasks[dateKey]['count'] || 0):0)-(cancelledTasks[dateKey]?(cancelledTasks[dateKey]['count']||0):0));
  finalDict[dateKey] = {  count:finalDict[dateKey],
						  isNotDone:nonDone >0, 
						  task:'Not done tasks:'+(notDoneTasks[dateKey] ? (notDoneTasks[dateKey]['task']||''):'<br>') + 
						       'Cancelled tasks:'+(cancelledTasks[dateKey]?(cancelledTasks[dateKey]['task']||''):'<br>') + 
						       'Done tasks:'+(doneTasks[dateKey] ? (doneTasks[dateKey]['task']||''):'<br>'+'<br>')
						};
});

for (let [date, { count, isNotDone, task }] of Object.entries(finalDict).sort(([dateA], [dateB]) =>
  new Date(dateA) - new Date(dateB)
)) {
	let scaledIntensity = scaleIntensity(count, isNotDone, date); // Adjust maxValue as needed 
	//dv.span('On [['+date+']], I had/have '+count+' task(s), defined as:<br>'+task+'<br>')
	calendarData.entries.push({ 
		date: date, 
		intensity:scaledIntensity, 
		color: 'work',  
		content: dv.span(`[](${date})`),//`<span title="${task}"><a href="${date}">&nbsp;</a></span>`
		}); 
	}
//}
//dv.table(["Text", "Completed", "Cancelled"], 
  //tasks.map(t => [t.text, t.completed, t.text.includes('❌')]));
const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData)

// Adding container for legends and colored boxes on the same line
const legendsContainer = document.createElement('div');
legendsContainer.style.display = 'flex';
legendsContainer.style.alignItems = 'center'; // Align vertically
legendsContainer.style.justifyContent = 'center'; // Center horizontally 
legendsContainer.style.width = '100%'; // Ensure it takes full width for centering

// Adding first legend with reduced size and custom font
const firstLegend = document.createElement('div');
firstLegend.innerText = 'Buzy with tasks to-do'; // Updated to "LESS" with all caps
firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
legendsContainer.appendChild(firstLegend);

// Adding colored boxes with adjusted size
const legendContainer = document.createElement('div');
legendContainer.style.display = 'flex';
legendContainer.style.alignItems = 'center'; // Align vertically

let i=0;
for (let color of calendarData.colorScheme.heat) {
    const colorBox1 = document.createElement('div');
    colorBox1.style.width = '9px'; // Reduced box width by 50%
    colorBox1.style.height = '9px'; // Reduced box height by 50%
    colorBox1.style.backgroundColor = color;
    colorBox1.style.marginRight = '5px'; // Adjusted margin
    legendContainer.appendChild(colorBox1);
    if(i===5){break;}
    else{i+=1;}
}

// Adding second legend after the colored boxes with reduced size and custom font
const medLegend = document.createElement('div');
medLegend.innerText = '...    Free     ...'; // Updated to "MORE" with all caps
medLegend.style.fontSize = '65%'; // Reduce font size by 50%
medLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
medLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
legendContainer.appendChild(medLegend);

i=0;
for (let color of calendarData.colorScheme.heat) {
	if(i<=5){i+=1;continue;}
    const colorBox = document.createElement('div');
    colorBox.style.width = '9px'; // Reduced box width by 50%
    colorBox.style.height = '9px'; // Reduced box height by 50%
    colorBox.style.backgroundColor = color;
    colorBox.style.marginRight = '5px'; // Adjusted margin
    legendContainer.appendChild(colorBox);
}

// Adding second legend after the colored boxes with reduced size and custom font
const secondLegend = document.createElement('div');
secondLegend.innerText = 'Tasks Done'; // Updated to "MORE" with all caps
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