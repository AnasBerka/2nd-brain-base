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
#### Scale of life
$$
\text{Balance In life} = \sum (\text{Time}_1 \text{ allowed} - \text{Official activities}) + \sum (\text{Fun activities}  - \text{Time}_2 \text{ allowed}) + \frac{\text{GYM activities}}{\text{avg expected}} + \frac{\text{Money spent}}{\text{daily}}
$$

```dataviewjs
const heatmapColors = [
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
  "rgb(0, 10, 51)"
];

const calendarData = { year: 2026,
    intensityScaleStart: 0,
    intensityScaleEnd: 12, // I have 12 color levels in heat
    entries: [],
    separateMonths: true,
    colorScheme: {
        paletteName: "heat",
//         "heat": [
//         "rgb(204, 0, 0)",
//         "rgb(255, 0, 0)", 
//         "rgb(255, 51, 51)",
//         "rgb(255, 102, 102)",
//         "rgb(255, 153, 153)",  
//       "rgb(255, 204, 204)",    
//       "rgb(128, 138, 166)",
//       "rgb(77, 90, 128)",
//       "rgb(51, 64, 114)",
//       "rgb(25, 38, 99)",
//       "rgb(0, 18, 77)",
//       "rgb(0, 10, 51)",
//     ],
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
	//let lifeQuality = capMax((((page.moneyInDh||0)-(page.dailyDh||0))/(page.dailyDh||1)),3) +(page.meTime||0)/60-6 -(page.bTime)*5 -capMax((page.ScreenTime||1)/(page.UnlockNbr||1),2) -(page.smMin||0)/((page.Fb||1)+(page.Insta||1)) +(page.gamingPCMin||0)/(60*3) -((page.gamingMobileMin||0)/60) +(page.animeEp||0)/(3*6) +(page.travelingDist||0)/5 +6-((page.hWork||0)/60) +4-((page.oWork||0)/60) +4-((page.pWork||0)/60) +((page.salatOnTime||0)/5)-5 + (page.pushUpReps||0)/100 + (page.setUpReps||0)/100 + (page.squadReps||0)/100;
	let Money = capMax((((page.moneyInDh||0)+(page.dailyDh||0))/(page.dailyDh||1)),6);   //Money's balance 50% of the scale 
	let Fun = capMax(                                                                     //Fun 25% of the scale
              (4-((page.ScreenTime||1)/60)+(72-(page.UnlockNbr||1))/72                      //general use of the phone 
              +2-((page.smMin||0)/60)                                                       //Social media impact
              +(((page.gamingPCMin||0)+(page.gamingMobileMin||0))/60)                       //Gaming time
              +(page.animeEp||0)/(3*60)+((page.movieMin)/60))                               //Watching anime & YouTube 
            ,3);
	let Work = capMax(                                                                //Work's time 25% of the scale
              ((page.hWork||0)/60) -2                                                  //Home's work
              +((page.rWork||0)/60) -2                                                  //Reaserch's work
              -((page.oWork||0)/60)                                                     //Office work
              +3.5-((page.tWork||0)/60)                                                     //Exra work
              -((page.mWork||0)/60)                                                     //Exra work
              -((page.pWork||0)/60)                                                     //Exra work
              +((page.sWork||0)/60)
              //Official studies
            ,6);
	let Body = capMax(                                                                //Body's share, 25% of the scale
              + ((page.pushUpReps||0)+(page.squadReps||0)+(page.setUpReps||0))/300      //Exercices at home
              + (page.gymMin||0)/120                                                       //Time training
              + (page.gymKg||0)/(300*((page.myWeight||90)/2))                              //Weight to train with
              + (page.travelingDist||0)/10                                              //Walking reward 
              + (page.runingKm||0)/2                                                    //Running reward
            ,3);
	let Punishment =  capMax((page.meTime||(60*6))/60-3 -(page.bTime||0)*5                            //Punishment when not provided enough rest
			         +(page.salatOnTime||5)-5,3);                                                 //Punishment when not prayed at time
	let lifeQuality = Money + Work + Body + Punishment;
	let scaledIntensity = scaleIntensity(Math.abs(lifeQuality),12); 
	let intensityVal = lifeQuality >= 0 ? scaledIntensity + 1 : 7 + scaledIntensity;
	//dv.span(page.file.name+'<spam>: <spam>'+(page.moneyInDh||0).toFixed(2)+'<spam>   <=>    <spam>'+lifeQuality.toFixed(2)+'<spam>  =>     <spam>'+intensityVal+'<br>');
	//dv.span('Money:'+Money.toFixed(2)+'<spam> Work:'+Work.toFixed(2)+'<spam> Body:'+Body.toFixed(2)+'<spam> Punishment:'+Punishment.toFixed(2)+'<spam> lifeQuality:'+lifeQuality.toFixed(2)+' '+Math.abs(lifeQuality)+'<spam> intensityVal:'+intensityVal.toFixed(2)+' '+scaledIntensity+'<br>');
    calendarData.entries.push({
        date: page.file.name,
        intensity: intensityVal, // Use scaled intensity
//         color:"heat",
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
// firstLegend.innerText = 'Evil'; // Updated to "LESS" with all caps
// firstLegend.style.fontSize = '65%'; // Reduce font size by 50%
// firstLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// firstLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// firstLegend.style.marginRight = '5px'; // Add margin to separate from the boxes
// legendsContainer.appendChild(firstLegend);

// // Adding colored boxes with adjusted size
// const legendContainer = document.createElement('div');
// legendContainer.style.display = 'flex';
// legendContainer.style.alignItems = 'center'; // Align vertically

// for (let color of calendarData.colorScheme.heat) {
//     const colorBox = document.createElement('div');
//     colorBox.style.width = '9px'; // Reduced box width by 50%
//     colorBox.style.height = '9px'; // Reduced box height by 50%
//     colorBox.style.backgroundColor = color;
//     colorBox.style.marginRight = '5px'; // Adjusted margin
//     legendContainer.appendChild(colorBox);
// }

// // Adding second legend after the colored boxes with reduced size and custom font
// const secondLegend = document.createElement('div');
// secondLegend.innerText = 'Good'; // Updated to "MORE" with all caps
// secondLegend.style.fontSize = '65%'; // Reduce font size by 50%
// secondLegend.style.fontFamily = 'IBM plex mono, sans-serif'; // Set custom font
// secondLegend.style.textTransform = 'uppercase'; // Convert text to uppercase
// legendContainer.appendChild(secondLegend);

// legendsContainer.appendChild(legendContainer);
// legendsContainer.style.marginBottom = "12px";

// heatmapTrackerEl.appendChild(legendsContainer);

// dv.span('Overall balance tracker statistics:')

const heatmapTrackerEl = renderHeatmapTracker(this.container, calendarData)
renderInlineLegend(heatmapTrackerEl, heatmapColors, 'Evil', 'Good')
```
