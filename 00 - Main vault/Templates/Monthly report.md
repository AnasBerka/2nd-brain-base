---
tags:
  - Monthly
banner: "[[Sky2Banner.jpg]]"
banner_x: 0
banner_y: 0.906
cssclasses:
  - daily
isCompleted:
---

[[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title, "YYYY-MM _ MMMM").subtract(1,'month').format("YYYY-MM _ MMMM")%>|⬅️]]|[[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title,  "YYYY-MM _ MMMM").add(1,'month').format("YYYY-MM _ MMMM")%>|➡️]]

***
***
### Summary about the month 🗒️
- [ ] Add summary of the month <%moment(tp.file.title).format("YYYY-MM _ MMMM")%> here ⏬  
***
***


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
    title: Home exercices
    yAxisLabel: Count
    lineColor: yellow, red, blue
    showLegend: true
    legendPosition: bottom
	yMin: 0
    yMax: 100
    fillGap: true
    xAxisTickInterval: 7d
    xAxisTickLabelFormat: MM-DD
```
***
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
    title: "💸 Money log 💰"
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
***
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

```tracker
searchType: dvField
searchTarget: hWork, rWork, oWork
datasetName: Self-improvements, Research work, Official work
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
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
### ** ⚖️ Weight & Height 📏 **

In this month, regadring my weight:
``` tracker
searchType: dvField
searchTarget: myWeight, myHeight
folder: "00 - Main vault/Notes/Daily Notes"
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
summary:
    template: "Minimum: {{min()}}kg\nMaximum: {{max()}}kg"
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
    template: "Minimum: {{min()}}cm\nMaximum: {{max()}}cm"
```
***
``` tracker
searchType: dvField
searchTarget: pushUpReps, setUpReps, squadReps
datasetName: PushUp, SetUp, Squad
folder: "00 - Main vault/Notes/Daily Notes"
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
month:
    dataset: 0, 1, 2
    startWeekOn: 'Sun'
    threshold: 40, 0, 0
    color: green
    headerMonthColor: orange
    dimNotInMonth: false
    todayRingColor: orange
    selectedRingColor: steelblue
    circleColorByValue: true
    showSelectedValue: true
    initMonth: 2025-01
```
***
Add sleeping info

``` tracker
searchType: dvField
searchTarget: startHWorkAt, finishHWorkAt, startOWorkAt, finishOWorkAt, startRWorkAt, finishRWorkAt
startDate: <% moment(tp.file.title, "YYYY-MM _ MMMM").startOf('month').format("YYYY-MM-DD") %>
endDate: <% moment(tp.file.title, "YYYY-MM _ MMMM", true).endOf('month').format("YYYY-MM-DD") %>
folder: "00 - Main vault/Notes/Daily Notes"
datasetName: hClock-In, hClock-Out, oClock-In, oClock-Out, rClock-In, rClock-Out 
fitPanelWidth: true
aspectRatio: 20:9
line:
    title: "Active Hours"
    yAxisLabel: "Time (24h)"
    reverseYAxis: true
    lineColor: yellow, red, yellow, red, yellow, red
    showPoint: true
    showLegend: true
```
