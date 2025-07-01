---
tags:
  - Logging/Monthly/<%moment(tp.file.title, "YYYY-MM _ MMMM").format("YYYY")%>
banner: "[[Sky2Banner.jpg]]"
banner_x: 0
banner_y: 0.906
cssclasses:
  - daily
  - sNote
isCompleted:
---

[[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title, "YYYY-MM _ MMMM").subtract(1,'month').format("YYYY")%>/<%moment(tp.file.title, "YYYY-MM _ MMMM").subtract(1,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title, "YYYY-MM _ MMMM").subtract(1,'month').format("YYYY-MM _ MMMM")%>⬅️]]|[[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title,  "YYYY-MM _ MMMM").add(1,'month').format("YYYY")%>/<%moment(tp.file.title,  "YYYY-MM _ MMMM").add(1,'month').format("YYYY-MM _ MMMM")%>|➡️<%moment(tp.file.title,  "YYYY-MM _ MMMM").add(1,'month').format("YYYY-MM _ MMMM")%>]]
For a more global view, switch to year: [[00 - Main vault/Notes/Annually reports/<%moment(tp.file.title, "YYYY-MM _ MMMM").format("YYYY")%>|<%moment(tp.file.title, "YYYY-MM _ MMMM").format("YYYY")%>⤴️]]
***
## Summary of <%moment(tp.file.title, "YYYY-MM _ MMMM").format("MMMM YYYY")%> 🗒️

***
- [ ] 👨‍💼 Add a summary for <%moment(tp.file.title, "YYYY-MM _ MMMM").format("MMMM YYYY")%> 📅 <%moment(tp.file.title, "YYYY-MM _ MMMM").endOf('Month').subtract(0,'day').format("YYYY-MM-DD")%> ⏬  
***

### [[00 - Main vault/Notes/Annually reports/<%moment(tp.file.title, "YYYY-MM _ MMMM").format("YYYY")%>#Salat _ Stat Salat 🙏|🙏 Salat 🛐]]
#### Salat on time
``` tracker
searchType: dvField
searchTarget: salatOnTime
folder: "00 - Main vault/Notes/Daily Notes"
accum: false
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    yAxisLabel: Nbr of prayers 
    pointSize: 2.5
    pointColor: white
    pointBorderWidth: 2
    pointBorderColor: "#d65d0e"
    fillGap: true
    yAxisTickInterval: 1
    xAxisTickInterval: 7d
    xAxisTickLabelFormat: MM-DD
```
#### Reading quran
``` tracker
searchType: dvField
searchTarget: quranReading
folder: "00 - Main vault/Notes/Daily Notes"
accum: false
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    yAxisLabel: Nbr of a7zab 
    pointSize: 2.5
    pointColor: white
    pointBorderWidth: 2
    pointBorderColor: "#d65d0e"
    fillGap: true
    yAxisTickInterval: 1
    xAxisTickInterval: 7d
    xAxisTickLabelFormat: MM-DD
```

***

### [[00 - Main vault/Notes/Annually reports/<%moment(tp.file.title, "YYYY-MM _ MMMM").format("YYYY")%>#Work _ Stat Work 👨‍💼|Work]] 👨‍💼
#### Active Hours
``` tracker
searchType: dvField
searchTarget: startOWorkAt, finishOWorkAt
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
folder: "00 - Main vault/Notes/Daily Notes"
datasetName: oClock-In, oClock-Out
fitPanelWidth: true
aspectRatio: 20:9
line:
    yAxisLabel: "Time (24h)"
    reverseYAxis: true
    lineColor: '#e1401f, #1fc0e1'
    showPoint: true
    showLegend: true
	yMin: 06:00 AM
    yMax: 11:00 PM
```
#### Time management
```tracker
searchType: dvField
searchTarget: hWork, rWork, oWork
datasetName: Self-improvements, Research work, Official work
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
pie:
    label: '{{sum(dataset(0))*100/(sum(dataset(0))+sum(dataset(1))+sum(dataset(2)))}}%,{{sum(dataset(1))*100/(sum(dataset(0))+sum(dataset(1))+sum(dataset(2)))}}%,{{sum(dataset(2))*100/(sum(dataset(0))+sum(dataset(1))+sum(dataset(2)))}}%'
    data: '{{sum(dataset(0))}},{{sum(dataset(1))}},{{sum(dataset(2))}}'
    dataColor: '#FF5733,#33FF57,#3388FF'
    ratioInnerRadius: 0.6
    dataName: Self-improvements, Research work, Official work
    showLegend: true
    legendPosition: right
    legendOrientation: vertical	
```

#### Official work paiment
```tracker
searchType: dvField
searchTarget: pWork, oWork
datasetName: Paid work, Free official work
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
pie:
    label: '{{100*(1-(sum(dataset(1))-sum(dataset(0)))/sum(dataset(1)))}}%,{{100*(sum(dataset(1))-sum(dataset(0)))/sum(dataset(1))}}%'
    data: '{{1-(sum(dataset(1))-sum(dataset(0)))/sum(dataset(1))}},{{(sum(dataset(1))-sum(dataset(0)))/sum(dataset(1))}}'
    dataColor: '#1fc0e1,#e1401f'
    ratioInnerRadius: 0.6
    dataName: Paid work, Free official work
    showLegend: true
    legendPosition: right
    legendOrientation: vertical	
```
#### Statistique for work
This month, we got a total of:
```dataviewjs
const startDate = moment("<% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>", "YYYY-MM-DD");
const endDate = moment("<% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>", "YYYY-MM-DD");
let hWork = 0, oWork = 0, rWork = 0, pWork=0;
const pages = dv.pages('"00 - Main vault/Notes/Daily Notes"')
    .filter(p => {
        // Try to extract the date from filename (assuming YYYY-MM-DD format)
        let fileDate = moment(p.file.name, "YYYY-MM-DD");
        
        // If the date is stored in metadata, use that instead
        if (p.date) {
            fileDate = moment(p.date, "YYYY-MM-DD");
        }

        // Include only pages within the year 2025
        return fileDate.isBetween(startDate, endDate, null, "[]"); // Inclusive range
    });
    
for (let p of pages) {
    hWork += p.hWork || 0;
    oWork += p.oWork || (p.pWork || 0);
    rWork += p.rWork || 0;
    pWork += p.pWork || 0;
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
👨‍🎓 **${formatTime(rWork)}**:\t Research work 
💸 **${formatTime(pWork)}**:\t Payed work`);
```

***

### [[00 - Main vault/Notes/Annually reports/<%moment(tp.file.title, "YYYY-MM _ MMMM").format("YYYY")%>#GYM _ Stat GYM 💪|GYM]] 💪

#### Home exercices
```tracker
searchType: dvField
searchTarget: pushUpReps, setUpReps, squadReps
datasetName: PushUp, SetUp, Squad
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    yAxisLabel: Count
    lineColor: '#FF5733,#33FF57,#3388FF'
    showLegend: true
    legendPosition: bottom
	yMin: 0
    yMax: 100
    fillGap: true
    xAxisTickInterval: 7d
    xAxisTickLabelFormat: MM-DD
```
#### GYM exercices (Nbr Reps)
```tracker
searchType: dvField
searchTarget: pushBarMaxRep, pullBarMaxRep, squadBarMaxRep, curlDumpMaxRep
datasetName: ChestRep, BackRep, LegsRep, ArmsRep
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    yAxisLabel: Count
    lineColor: '#F4A261,#2A9D8F,#FF5733,#3388FF'
    showLegend: true
    legendPosition: bottom
	yMin: 0
    yMax: 15
    fillGap: true
    xAxisTickInterval: 7d
    xAxisTickLabelFormat: MM-DD
```
#### GYM exercices (Max Kg per rep)
```tracker
searchType: dvField
searchTarget: pushBarMaxKg, pullBarMaxKg, squadBarMaxKg, curlDumpMaxKg
datasetName: ChestRep, BackRep, LegsRep, ArmsRep
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    yAxisLabel: Weight (Kg)
    lineColor: '#F4A261,#2A9D8F,#FF5733,#3388FF'
    showLegend: true
    legendPosition: bottom
	yMin: 0
    fillGap: true
    xAxisTickInterval: 7d
    xAxisTickLabelFormat: MM-DD
```
#### GYM time
```tracker
searchType: dvField
searchTarget: gymKg, gymMin
datasetName: GYM Kg, GYM Min
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    lineColor: '#1fc0e1,#e1401f'
    yAxisLabelColor: '#1fc0e1,#e1401f'
    yAxisLocation: left, right
    yAxisLabel: Weight (Kg), Time (Min)
    showLegend: true
    legendPosition: bottom
	yMin: 0
    fillGap: true
    xAxisTickInterval: 7d
    xAxisTickLabelFormat: MM-DD
```
#### Traveling on feet
```tracker
searchType: dvField
searchTarget: travelingDist, runingKm, Steps
datasetName: Traveling, runingKm, Steps
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    yAxisLabel: Weight (Kg)
    lineColor: '#FF5733,#33FF57,#3388FF'
    yAxisLocation: left, left, right
    yAxisLabel: Distance (Km), Steps (Count)
    showLegend: true
    legendPosition: bottom
	yMin: 0
    fillGap: true
    xAxisTickInterval: 7d
    xAxisTickLabelFormat: MM-DD
```
#### Traveling:
``` tracker
searchType: dvField
searchTarget: travelingDist
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
summary:
    template: "Average: {{average()}} Km\t_\tMinimum: {{min()}} Km\t-\tMaximum: {{max()}} Km"
```
#### Running:
``` tracker
searchType: dvField
searchTarget: runingKm
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
summary:
    template: "Average: {{average()}} Km\t_\tMinimum: {{min()}} Km\t-\tMaximum: {{max()}} Km"
```
#### I'm speed
```tracker
searchType: dvField
searchTarget: runingAS, springMaxSpeed
datasetName: Avg Speed, Max Speed
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    yAxisLabel: Speed (Km/h)
    yAxisLabelColor: '#1fc0e1,#e1401f'
    lineColor: '#1fc0e1,#e1401f'
    yAxisLocation: left, right
    showLegend: true
    legendPosition: bottom
	yMin: 0
    fillGap: true
    xAxisTickInterval: 7d
    xAxisTickLabelFormat: MM-DD
```
#### Avg Speed:
``` tracker
searchType: dvField
searchTarget: runingAS
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
summary:
    template: "Average: {{average()}} Km/h\t_\tMinimum: {{min()}} Km/h\t_\tMaximum: {{max()}} Km/h"
```
#### Max Speed:
``` tracker
searchType: dvField
searchTarget: springMaxSpeed
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
summary:
    template: "Average: {{average()}} Km/h\t_\tMinimum: {{min()}} Km/h\t_\tMaximum: {{max()}} Km/h"
```
#### Stamina vs Adrenaline
```tracker
searchType: dvField
searchTarget: runingMin, springMaxSS
datasetName: Stamina, Adrenaline
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    title: How much can I last ?
    lineColor: '#1fc0e1,#e1401f'
    yAxisLabelColor: '#1fc0e1,#e1401f'
    yAxisLocation: left, right
    yAxisLabel: Duration (Mim), Duration (Seconds)
    showLegend: true
    legendPosition: bottom
	yMin: 0
    fillGap: true
    xAxisTickInterval: 7d
    xAxisTickLabelFormat: MM-DD
```
#### Stamina:
``` tracker
searchType: dvField
searchTarget: runingMin
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
summary:
    template: "Average: {{average()}} Min\t_\tMinimum: {{min()::i}} Min\t_\tMaximum: {{max()::i}} Min"
```
#### Adrenaline:
``` tracker
searchType: dvField
searchTarget: springMaxSS
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
summary:
    template: "Average: {{average()}} Seconds\t_\tMinimum: {{min()::i}} Seconds\t_\tMaximum: {{max()::i}} Seconds"
```

***

### [[00 - Main vault/Notes/Annually reports/<%moment(tp.file.title, "YYYY-MM _ MMMM").format("YYYY")%>#Weight and Height _ Stat Weight & Height 📏|Weight & Height]] 📏 

``` tracker
searchType: dvField
searchTarget: myWeight, myHeight
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    title: Weight Log
    yAxisLabel: Weight, Height
    lineColor: yellow
    fillGap: true
    yAxisLabel: Weight, Height
    yAxisUnit: Kg, cm
    yAxisLocation: left, right
    yAxisColor: yellow, blue
    yAxisLabelColor: yellow, blue
    lineColor: yellow, blue
    yAxisTickLabelFormat: .2f, .0f
    xAxisTickInterval: 7d
    xAxisTickLabelFormat: MM-DD
```
In this month, regadring my weight:
``` tracker
searchType: dvField
searchTarget: myWeight, myHeight
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
summary:
    template: "Average: {{average()}} Kg \n Minimum: {{min()}} Kg \t_\t Maximum: {{max()}} Kg"
```
__
While for my height:
``` tracker
searchType: dvField
searchTarget: myHeight
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
summary:
    template: "Average: {{average()}} cm \nMinimum: {{min()}} cm \t_\t Maximum: {{max()}} cm"
```
***
### [[00 - Main vault/Notes/Annually reports/<%moment(tp.file.title, "YYYY-MM _ MMMM").format("YYYY")%>#Fun _ Stat Fun 🎮|Fun]] 🎮

#### Watching & reading
```tracker
searchType: dvField
searchTarget: animeEp, RManga, BRead, LWRead
datasetName: Animes, Manga, Books, LWNovels
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    lineColor: '#F4A261,#2A9D8F,#FF5733,#3388FF'
    yAxisLabel: Count
    showLegend: true
    legendPosition: bottom
	yMin: 0
    fillGap: true
    xAxisTickInterval: 7d
    xAxisTickLabelFormat: MM-DD
```

#### Gaming
```tracker
searchType: dvField
searchTarget: gamingMobileMin, gamingPCMin 
datasetName: G-Phone, ROG time
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    lineColor: '#1fc0e1,#e1401f'
    yAxisLabel: Time (Min)
    showLegend: true
    legendPosition: bottom
	yMin: 0
    fillGap: true
    xAxisTickInterval: 7d
    xAxisTickLabelFormat: MM-DD
```

#### Time on phone
```tracker
searchType: dvField
searchTarget: ScreenTime, smMin, Insta, Fb, UnlockNbr
datasetName: Screen Time, Social Media, Instagram, Facebook, Unlocks
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    lineColor: '#FFD166, #2A9D8F, #e1401f, #1fc0e1, white'
    yAxisLocation: left, left, left, left, right
    yAxisLabel: Time (Min), Count
    showLegend: true
    legendPosition: bottom
	yMin: 0
    fillGap: true
    xAxisTickInterval: 7d
    xAxisTickLabelFormat: MM-DD
```

***

### [[00 - Main vault/Notes/Annually reports/<%moment(tp.file.title, "YYYY-MM _ MMMM").format("YYYY")%>#Money _ Stat Money spending 💸|Money spending]] 💸
#### 💸 Money log 💰
``` tracker
searchType: dvField
searchTarget: moneyInDh
folder: "00 - Main vault/Notes/Daily Notes"
accum: true
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    yAxisLabel: Dirham 
    yAxisUnit: Dh
    pointSize: 2.5
    pointColor: white
    pointBorderWidth: 2
    pointBorderColor: "#d65d0e"
    fillGap: true
    xAxisTickInterval: 7d
    xAxisTickLabelFormat: MM-DD
```

***
### [[00 - Main vault/Notes/Annually reports/<%moment(tp.file.title, "YYYY-MM _ MMMM").format("YYYY")%>#Sleeping _ Stat Sleeping & Mood 😏|Sleeping & Mood]] 😏 
A healthy brain in a healthy body 💤
```tracker
searchType: dvField
searchTarget: meTime, bTime
datasetName: Sleeping, No-Mood
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    lineColor: '#1fc0e1,#e1401f'
    yAxisLocation: left, right
    yAxisLabel: Time (Min), Count
    showLegend: true
    legendPosition: bottom
	yMin: 0
    fillGap: true
    xAxisTickInterval: 7d
    xAxisTickLabelFormat: MM-DD
```

### Sleeping timer ⌚ 
``` tracker
searchType: dvField
searchTarget: wokedAt,sleptAt
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
folder: "00 - Main vault/Notes/Daily Notes"
datasetName: Waking up, Sleeping
fitPanelWidth: true
aspectRatio: 20:9
line:
    yAxisLabel: "Time (24h)"
    reverseYAxis: true, false
    yAxisLocation: left, right
    lineColor: '#e1401f, #1fc0e1'
    yAxisColor: '#e1401f, #1fc0e1'
    showPoint: true
    showLegend: true
    fillGap: true
    xAxisTickInterval: 7d
    xAxisTickLabelFormat: MM-DD
	yMin: 03:00 AM, 12:00 AM
    yMax: 02:00 PM, 11:59 PM
```