---
tags:
  - Logging/Annually
banner: "[[Sky3Banner.jpg]]"
banner_x: 0
banner_y: 0.906
cssclasses:
  - daily
  - sNote
isCompleted:
---

[[00 - Main vault/Notes/Annually reports/<%moment(tp.file.title).subtract(1,'year').format("YYYY")%>|<%moment(tp.file.title).subtract(1,'year').format("YYYY")%>⬅️]]|[[00 - Main vault/Notes/Annually reports/<%moment(tp.file.title).add(1,'year').format("YYYY")%>|➡️<%moment(tp.file.title).add(1,'year').format("YYYY")%>]]
Browse each month individually:
[[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title,"YYYY").format("YYYY")%>/<%moment(tp.file.title).startOf('Month').add(0,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(0,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title,"YYYY").format("YYYY")%>/<%moment(tp.file.title).startOf('Month').add(1,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(1,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title,"YYYY").format("YYYY")%>/<%moment(tp.file.title).startOf('Month').add(2,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(2,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title,"YYYY").format("YYYY")%>/<%moment(tp.file.title).startOf('Month').add(3,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(3,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title,"YYYY").format("YYYY")%>/<%moment(tp.file.title).startOf('Month').add(4,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(4,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title,"YYYY").format("YYYY")%>/<%moment(tp.file.title).startOf('Month').add(5,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(5,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title,"YYYY").format("YYYY")%>/<%moment(tp.file.title).startOf('Month').add(6,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(6,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title,"YYYY").format("YYYY")%>/<%moment(tp.file.title).startOf('Month').add(7,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(7,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title,"YYYY").format("YYYY")%>/<%moment(tp.file.title).startOf('Month').add(8,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(8,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title,"YYYY").format("YYYY")%>/<%moment(tp.file.title).startOf('Month').add(9,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(9,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title,"YYYY").format("YYYY")%>/<%moment(tp.file.title).startOf('Month').add(10,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(10,'month').format("MMM")%>]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title,"YYYY").format("YYYY")%>/<%moment(tp.file.title).startOf('Month').add(11,'month').format("YYYY-MM _ MMMM")%>|<%moment(tp.file.title).startOf('Month').add(11,'month').format("MMM")%>]]
***
### Summary about the year <%moment(tp.file.title,"YYYY").format("YYYY")%>🗒️

***
- [ ] 📝 Add the summary of the year <%moment(tp.file.title,"YYYY").format("YYYY")%>  ⏬ 📅 <%moment(tp.file.title).endOf('year').format("YYYY-MM-DD")%>
***
### [[Salat _ Stat|Salat]] 🙏
#### Salat on time
``` tracker
searchType: dvField
searchTarget: salatOnTime
folder: "00 - Main vault/Notes/Daily Notes"
accum: false
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    yAxisLabel: Nbr of prayers 
    showPoint: false
    lineColor: #d5f9f6
    fillGap: true
    yAxisTickInterval: 1
    xAxisTickInterval: 1m
    xAxisTickLabelFormat: MMMM
```
#### Reading quran
``` tracker
searchType: dvField
searchTarget: quranReading
folder: "00 - Main vault/Notes/Daily Notes"
accum: false
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    yAxisLabel: Nbr of a7zab 
    showPoint: false
    lineColor: #d5f9f6
    fillGap: true
    yAxisTickInterval: 1
    xAxisTickInterval: 1m
    xAxisTickLabelFormat: MMMM
```

***
### [[Work _ Stat|Work]] 👨‍💼
#### Active Hours
``` tracker
searchType: dvField
searchTarget: startOWorkAt, finishOWorkAt
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
folder: "00 - Main vault/Notes/Daily Notes"
datasetName: oClock-In, oClock-Out
fitPanelWidth: true
aspectRatio: 20:9
line:
    yAxisLabel: "Time (24h)"
    reverseYAxis: true
    lineColor: '#e1401f, #1fc0e1'
    showPoint: false
    showLegend: true
	yMin: 06:00 AM
    yMax: 11:00 PM
    xAxisTickInterval: 1m
    xAxisTickLabelFormat: MMMM
```
#### Time management
```tracker
searchType: dvField
searchTarget: hWork, rWork, oWork
datasetName: Self-improvements, Research work, Official work
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
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
#### Official work payment
```tracker
searchType: dvField
searchTarget: pWork, oWork
datasetName: Paid work, Free official work
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
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
This year, we got a total of:
```dataviewjs
const startDate = moment("<% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>", "YYYY-MM-DD");
const endDate = moment("<% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>", "YYYY-MM-DD");
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

### [[GYM _ Stat|GYM]] 💪

#### Home training
``` tracker
searchType: dvField
searchTarget: pushUpReps, setUpReps, squadReps, typingSpeed
datasetName: PushUp, SitUp, Squad, Typing
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
month:
    dataset: 0, 1, 2, 3
    startWeekOn: 'Sun'
    threshold: 0, 0, 0, 0
    color: green
    headerMonthColor: orange
    dimNotInMonth: false
    todayRingColor: orange
    selectedRingColor: steelblue
    circleColorByValue: true
    showSelectedValue: true
    initMonth: <% moment(tp.file.title, "YYYY").format("YYYY-01") %>
```
#### GYM exercices (Nbr Reps)
```tracker
searchType: dvField
searchTarget: pushBarMaxRep, pullBarMaxRep, squadBarMaxRep, curlDumpMaxRep
datasetName: ChestRep, BackRep, LegsRep, ArmsRep
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    title: GYM exercices (Nbr Reps)
    yAxisLabel: Count
    lineColor: '#F4A261,#2A9D8F,#FF5733,#3388FF'
    showLegend: true
    showPoint: false
    legendPosition: bottom
	yMin: 0
    yMax: 15
    fillGap: true
    xAxisTickInterval: 1m
    xAxisTickLabelFormat: MMMM
```
#### GYM exercices (Max Kg per rep)
```tracker
searchType: dvField
searchTarget: pushBarMaxKg, pullBarMaxKg, squadBarMaxKg, curlDumpMaxKg
datasetName: ChestRep, BackRep, LegsRep, ArmsRep
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    title: GYM exercices (Max Kg per rep)
    yAxisLabel: Weight (Kg)
    lineColor: '#F4A261,#2A9D8F,#FF5733,#3388FF'
    showLegend: true
    showPoint: false
    legendPosition: bottom
	yMin: 0
    fillGap: true
    xAxisTickInterval: 1m
    xAxisTickLabelFormat: MMMM
```
#### GYM time
```tracker
searchType: dvField
searchTarget: gymKg, gymMin
datasetName: GYM Kg, GYM Min
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    title: GYM time
    lineColor: '#1fc0e1,#e1401f'
    yAxisLabelColor: '#1fc0e1,#e1401f'
    yAxisLocation: left, right
    yAxisLabel: Weight (Kg), Time (Min)
    showLegend: true
    showPoint: false
    legendPosition: bottom
	yMin: 0
    fillGap: true
    showPoint: false
    xAxisTickInterval: 1m
    xAxisTickLabelFormat: MMMM
```
#### Traveling on feet
```tracker
searchType: dvField
searchTarget: travelingDist, runingKm, Steps
datasetName: Traveling, runingKm, Steps
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
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
    showPoint: false
    xAxisTickInterval: 1m
    xAxisTickLabelFormat: MMMM
```
#### Traveling:
``` tracker
searchType: dvField
searchTarget: travelingDist
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
summary:
    template: "Average: {{average()}} Km\t_\tMinimum: {{min()}} Km\t-\tMaximum: {{max()}} Km"
```
#### Running:
``` tracker
searchType: dvField
searchTarget: runingKm
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
summary:
    template: "Average: {{average()}} Km\t_\tMinimum: {{min()}} Km\t-\tMaximum: {{max()}} Km"
```
#### I'm speed
```tracker
searchType: dvField
searchTarget: runingAS, springMaxSpeed
datasetName: Avg Speed, Max Speed
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
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
    showPoint: false
    xAxisTickInterval: 1m
    xAxisTickLabelFormat: MMMM
```
#### Avg Speed:
``` tracker
searchType: dvField
searchTarget: runingAS
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
summary:
    template: "Average: {{average()}} Km/h\t_\tMinimum: {{min()}} Km/h\t_\tMaximum: {{max()}} Km/h"
```
#### Max Speed:
``` tracker
searchType: dvField
searchTarget: springMaxSpeed
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
summary:
    template: "Average: {{average()}} Km/h\t_\tMinimum: {{min()}} Km/h\t_\tMaximum: {{max()}} Km/h"
```
#### Stamina vs Adrenaline
```tracker
searchType: dvField
searchTarget: runingMin, springMaxSS
datasetName: Stamina, Adrenaline
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
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
    showPoint: false
    xAxisTickInterval: 1m
    xAxisTickLabelFormat: MMMM
```
#### Stamina:
``` tracker
searchType: dvField
searchTarget: runingMin
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
summary:
    template: "Average: {{average()}} Min\t_\tMinimum: {{min()::i}} Min\t_\tMaximum: {{max()::i}} Min"
```
#### Adrenaline:
``` tracker
searchType: dvField
searchTarget: springMaxSS
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
summary:
    template: "Average: {{average()}} Seconds\t_\tMinimum: {{min()::i}} Seconds\t_\tMaximum: {{max()::i}} Seconds"
```

***
### [[Weight and Height _ Stat|Weight & Height]] 📏
``` tracker
searchType: dvField
searchTarget: myWeight, myHeight
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
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
    showPoint: false
    xAxisTickInterval: 1m
    xAxisTickLabelFormat: MMMM
```
Globaly, my weight statistics:
``` tracker
searchType: dvField
searchTarget: myWeight
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
summary:
    template: "Average: {{average()}} Kg \n Minimum: {{min()}}kg\nMaximum: {{max()}}kg"
```
__
While for my height
``` tracker
searchType: dvField
searchTarget: myHeight
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
folder: "00 - Main vault/Notes/Daily Notes"
summary:
    template: "Average: {{average()}} cm \nMinimum: {{min()::i}}cm\nMaximum: {{max()}}cm"
```

***
### [[Fun _ Stat|Fun]] 🎮

#### Watching & reading
```tracker
searchType: dvField
searchTarget: animeEp, RManga, BRead, LWRead
datasetName: Animes, Manga, Books, LWNovels
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    lineColor: '#F4A261,#2A9D8F,#FF5733,#3388FF'
    yAxisLabel: Count
    showLegend: true
    legendPosition: bottom
	yMin: 0
	showPoint: false
    fillGap: true
    xAxisTickInterval: 1m
    xAxisTickLabelFormat: MMMM
```

#### Gaming
```tracker
searchType: dvField
searchTarget: gamingMobileMin, gamingPCMin 
datasetName: G-Phone, ROG time
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    lineColor: '#1fc0e1,#e1401f'
    yAxisLabel: Time (Min)
    showLegend: true
    legendPosition: bottom
	yMin: 0
	showPoint: false
    fillGap: true
    xAxisTickInterval: 1m
    xAxisTickLabelFormat: MMMM
```

#### Time on phone
```tracker
searchType: dvField
searchTarget: ScreenTime, smMin, Insta, Fb, UnlockNbr
datasetName: Screen Time, Social Media, Instagram, Facebook, Unlocks
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    lineColor: yellow, red, blue
    yAxisLocation: left, left, left, left, right
    yAxisLabel: Time (Min), Count
    showLegend: true
    legendPosition: bottom
	yMin: 0
    showPoint: false
    fillGap: true
    xAxisTickInterval: 1m
    xAxisTickLabelFormat: MMMM
```

***
### [[Money _ Stat|Money spending]] 💸
#### 💸 Money log 💰
``` tracker
searchType: dvField
searchTarget: moneyInDh
folder: "00 - Main vault/Notes/Daily Notes"
accum: true
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    yAxisLabel: Dirham 
    yAxisUnit: Dh
    showPoint: false
    fillGap: true
    xAxisTickInterval: 1m
    xAxisTickLabelFormat: MMMM
```

***

### [[Sleeping _ Stat|Sleeping & Mood]] 😏
A healthy brain in a healthy body 💤

```tracker
searchType: dvField
searchTarget: meTime, bTime
datasetName: Sleeping, No-Mood
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
fitPanelWidth: true
aspectRatio: 20:9
line:
    lineColor: '#1fc0e1,#e1401f'
    yAxisLocation: left, right
    yAxisLabel: Time (Min), Count
    showLegend: true
    legendPosition: bottom
	yMin: 0
    showPoint: false
    fillGap: true
    xAxisTickInterval: 1m
    xAxisTickLabelFormat: MMMM
```
### Sleeping timer ⌚ 
``` tracker
searchType: dvField
searchTarget: wokedAt,sleptAt
startDate: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY", true).endOf('year').format("YYYY-MM-DD") %>
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
    showPoint: false
    fillGap: true
    xAxisTickInterval: 1m
    xAxisTickLabelFormat: MMMM
    showLegend: true
	yMin: 03:00 AM, 12:00 AM
    yMax: 02:00 PM, 11:59 PM
```
***
### [[Tasks _ Stat|Tasks]] 📆
### [[Good vs Bad _ Stat|Self global judge ⚖️]]