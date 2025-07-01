---
tags:
  - Logging/Weekly/<%moment(tp.file.title).startOf('Week').add(0,'day').format("YYYY")%><%moment(tp.file.title).startOf('Week').add(6,'day').format("YYYY")%>
banner: "[[Sky1Banner.jpg]]"
banner_x: 0
banner_y: 0.974
cssclasses:
  - daily
  - sunday
isCompleted:
---
## <%moment(tp.file.title).format("gggg-[W]ww")%>
[[00 - Main vault/Notes/Weekly reports/<%moment(tp.file.title).subtract(1,'week').format("YYYY")%>/<%moment(tp.file.title).subtract(1,'week').format("gggg-[W]ww")%>|<%moment(tp.file.title).subtract(1,'week').format("gggg-[W]ww")%>⬅️]]|[[00 - Main vault/Notes/Weekly reports/<%moment(tp.file.title).add(1,'week').format("YYYY")%>/<%moment(tp.file.title).add(1,'week').format("gggg-[W]ww")%>|➡️<%moment(tp.file.title).add(1,'week').format("gggg-[W]ww")%>]]
For a more global view, switch to month: [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title).startOf('Week').add(0,'day').format("YYYY")%>/<%moment(tp.file.title).startOf('Week').add(0,'day').format("YYYY-MM _ MMMM")%>|⤴️]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title).startOf('Week').add(6,'day').format("YYYY")%>/<%moment(tp.file.title).startOf('Week').add(6,'day').format("YYYY-MM _ MMMM")%>|⤵️]]. 
For a more precise view, switch to days: 
[[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('Week').add(0,'day').format("YYYY")%>/<%moment(tp.file.title).startOf('Week').add(0,'day').format("MM")%>/<%moment(tp.file.title).startOf('Week').add(0,'day').format("YYYY-MM-DD")%>| Monday]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('Week').add(1,'day').format("YYYY")%>/<%moment(tp.file.title).startOf('Week').add(1,'day').format("MM")%>/<%moment(tp.file.title).startOf('Week').add(1,'day').format("YYYY-MM-DD")%>| Tuesday]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('Week').add(2,'day').format("YYYY")%>/<%moment(tp.file.title).startOf('Week').add(2,'day').format("MM")%>/<%moment(tp.file.title).startOf('isoWeek').add(2,'day').format("YYYY-MM-DD")%>| Wednesday]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('Week').add(3,'day').format("YYYY")%>/<%moment(tp.file.title).startOf('Week').add(3,'day').format("MM")%>/<%moment(tp.file.title).startOf('isoWeek').add(3,'day').format("YYYY-MM-DD")%>| Thursday]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('Week').add(4,'day').format("YYYY")%>/<%moment(tp.file.title).startOf('Week').add(4,'day').format("MM")%>/<%moment(tp.file.title).startOf('isoWeek').add(4,'day').format("YYYY-MM-DD")%>| Friday]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('Week').add(5,'day').format("YYYY")%>/<%moment(tp.file.title).startOf('Week').add(5,'day').format("MM")%>/<%moment(tp.file.title).startOf('isoWeek').add(5,'day').format("YYYY-MM-DD")%>| Saturday]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('Week').add(6,'day').format("YYYY")%>/<%moment(tp.file.title).startOf('Week').add(6,'day').format("MM")%>/<%moment(tp.file.title).startOf('isoWeek').add(6,'day').format("YYYY-MM-DD")%>|Sunday]]
***

### 🗒️ Summary of the week

***
- [ ] 👨‍💼 Add summary of the week <%moment(tp.file.title).format("[W]ww")%> 📅 <%moment(tp.file.title).startOf('isoWeek').add(6,'day').format("YYYY-MM-DD")%> ⏬  
***

### 🛐 Salat
 
 ```dataview
 table without id
 file.link AS "Day",
 choice(salatFajer,"✔️","❌") AS "Fajer",
 choice(salatDohr,"✔️","❌") AS "Dohr",
 choice(salatAaser,"✔️","❌") AS "Aaser",
 choice(salatMeghrb,"✔️","❌") AS "Meghrb",
 choice(salatIshae,"✔️","❌") AS "Ishae",
 salatOnTime AS "🛐",
 quranReading AS "📖"
 
 from "00 - Main vault/Notes/Daily Notes"
 where contains(week, "<%moment(tp.file.title).format("gggg-[W]ww")%>")
 sort file.name ASC
```
***
### 👨‍💼 Work time
```dataview
 table without id
 file.link AS "Day",
 (floor(default(hWork, 0) / 60))+"H "+(default(hWork, 0) % 60)+"Min" AS "👨‍💼",
 (floor(default(rWork, 0) / 60))+"H "+(default(rWork, 0) % 60)+"Min" AS "👨‍🎓",
 (floor(default(oWork, 0) / 60))+"H "+(default(oWork, 0) % 60)+"Min" AS "👨‍🏫",
 round(default(pWork, 0)*default(pWorkDh,1)/60,2)+"Dh" AS "💸",
 startOWorkAt AS "⏰",
 finishOWorkAt AS "🕰️"
 
 from "00 - Main vault/Notes/Daily Notes"
 where contains(week, "<%moment(tp.file.title).format("gggg-[W]ww")%>")
 sort file.name ASC
```
***
### 🏋️‍♂️ GYM time
```dataview
 table without id
 file.link AS "Day",
 (floor(default(gymMin, 0) / 60))+"H "+(default(gymMin, 0) % 60)+"Min"  AS "🏋️‍♂️",
 default(gymKg, 0)+"Kg" AS "🏋️",
 (floor(default(runingMin, 0) / 60))+"H "+(default(floor(runingMin), 0) % 60)+"Min " + 
 ((default(runingMin,0)-floor(default(runingMin, 0)))*60) +"s" AS "🏃",
 default(runingKm+"Km", null) AS "🏃‍♂️",
 default(runingAS+"Km/h", null) AS "🏃💨",
 default(springMaxSpeed+"Km/h", null) AS "🏎️💨",
 Steps AS "👨‍🦯",
 default(travelingDist+"Km",null) AS "🚶‍♂️",
 pushUpReps AS "Push-up",
 setUpReps AS "Sit-up",
 squadReps AS "Squat "
 
 from "00 - Main vault/Notes/Daily Notes"
 where contains(week, "<%moment(tp.file.title).format("gggg-[W]ww")%>")
 sort file.name ASC
```
***
### 🖥️ Fun Time
```dataview
 table without id
 file.link AS "Day",
 floor(default(default(animeEp,0)*25+default(movieMin,0),0)/60)+"H "+default(default(animeEp,0)*25+default(movieMin,0),0)%60+"Min" AS "🎬",
 RManga AS "👶",
 (default(BRead,0)+default(LWRead,0)) AS "📚",
 default(LWReadMin,0)+"Min" AS "👴",
 (floor(default(gamingPCMin, 0) / 60))+"H "+(default(gamingPCMin, 0) % 60)+"Min" AS "🎮",
 (floor(default(gamingMobileMin, 0) / 60))+"H "+(default(gamingMobileMin, 0) % 60)+"Min" AS "👾",
 UnlockNbr AS "🙆‍♂️",
 (floor(default(smMin, 0) / 60))+"H "+(default(smMin, 0) % 60)+"Min" AS "📱",
 (floor(default(ScreenTime, 0) / 60))+"H "+(default(ScreenTime, 0) % 60)+"Min" AS "⌛"
 
 from "00 - Main vault/Notes/Daily Notes"
 where contains(week, "<%moment(tp.file.title).format("gggg-[W]ww")%>")
 sort file.name ASC
```
***
### 👮 Personal Space
```dataview
 table without id
 file.link AS "Day",
 choice(gTime,"✔️","❌") AS "😁",
 default(moneyInDh,0)+"Dh" AS "💸",
 default(moneyInDh,0)+round(default(pWork, 0)*default(pWorkDh,1)/60,2)+"Dh" AS "💰",
 (floor(default(meTime, 0) / 60))+"H "+(default(meTime, 0) % 60)+"Min" AS "💤",
 bTime AS "😒",
 wokedAt AS "⏰",
 sleptAt AS "🕰️"
 
 from "00 - Main vault/Notes/Daily Notes"
 where contains(week, "<%moment(tp.file.title).format("gggg-[W]ww")%>")
 sort file.name ASC
```


