---
tags:
  - Logging/Weekly/<%moment(tp.file.title).startOf('isoWeek').format("GGGG")%><%moment(tp.file.title).endOf('isoWeek').format("GGGG")%>
banner: "[[Sky1Banner.jpg]]"
banner_x: 0
banner_y: 0.974
cssclasses:
  - daily
  - sunday
isCompleted:
---
## <%moment(tp.file.title).format("GGGG-[W]WW")%>
[[00 - Main vault/Notes/Weekly reports/<%moment(tp.file.title).subtract(1,'week').format("GGGG")%>/<%moment(tp.file.title).subtract(1,'week').format("GGGG-[W]WW")%>|<%moment(tp.file.title).subtract(1,'week').format("GGGG-[W]WW")%>⬅️]]|[[00 - Main vault/Notes/Weekly reports/<%moment(tp.file.title).add(1,'week').format("GGGG")%>/<%moment(tp.file.title).add(1,'week').format("GGGG-[W]WW")%>|➡️<%moment(tp.file.title).add(1,'week').format("GGGG-[W]WW")%>]]
For a more global view, switch to month: [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title).startOf('isoWeek').add(0,'day').format("GGGG")%>/<%moment(tp.file.title).startOf('isoWeek').add(0,'day').format("GGGG-MM _ MMMM")%>|⤴️]] | [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title).startOf('isoWeek').add(6,'day').format("GGGG")%>/<%moment(tp.file.title).startOf('isoWeek').add(6,'day').format("GGGG-MM _ MMMM")%>|⤵️]]. 

For a more precise view, switch to days: 
[[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('isoWeek').add(0,'day').format("YYYY")%>/<%moment(tp.file.title).startOf('isoWeek').add(0,'day').format("MM")%>/<%moment(tp.file.title).startOf('isoWeek').add(0,'day').format("YYYY-MM-DD")%>| Monday ]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('isoWeek').add(1,'day').format("GGGG")%>/<%moment(tp.file.title).startOf('isoWeek').add(1,'day').format("MM")%>/<%moment(tp.file.title).startOf('isoWeek').add(1,'day').format("GGGG-MM-DD")%>| Tuesday]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('isoWeek').add(2,'day').format("GGGG")%>/<%moment(tp.file.title).startOf('isoWeek').add(2,'day').format("MM")%>/<%moment(tp.file.title).startOf('isoWeek').add(2,'day').format("GGGG-MM-DD")%>| Wednesday]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('isoWeek').add(3,'day').format("GGGG")%>/<%moment(tp.file.title).startOf('isoWeek').add(3,'day').format("MM")%>/<%moment(tp.file.title).startOf('isoWeek').add(3,'day').format("GGGG-MM-DD")%>| Thursday]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('isoWeek').add(4,'day').format("GGGG")%>/<%moment(tp.file.title).startOf('isoWeek').add(4,'day').format("MM")%>/<%moment(tp.file.title).startOf('isoWeek').add(4,'day').format("GGGG-MM-DD")%>| Friday]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('isoWeek').add(5,'day').format("GGGG")%>/<%moment(tp.file.title).startOf('isoWeek').add(5,'day').format("MM")%>/<%moment(tp.file.title).startOf('isoWeek').add(5,'day').format("GGGG-MM-DD")%>| Saturday]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('isoWeek').add(6,'day').format("GGGG")%>/<%moment(tp.file.title).startOf('isoWeek').add(6,'day').format("MM")%>/<%moment(tp.file.title).startOf('isoWeek').add(6,'day').format("GGGG-MM-DD")%>|Sunday]]
***

### 🗒️ Summary of the week

***
- [-] 👨‍💼 Add summary of the week <%moment(tp.file.title).format("[W]WW")%> 📅 <%moment(tp.file.title).startOf('isoWeek').add(6,'day').format("GGGG-MM-DD")%> ⏬  
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
 where contains(week, "<%moment(tp.file.title).format("GGGG-[W]WW")%>")
 sort file.name ASC
```
***
### 👨‍💼 Work time
```dataview
 table without id
 file.link AS "Day",
 (floor(default(hWork, 0) / 60))+"H "+(default(hWork, 0) % 60)+"Min" AS "🤹‍♂️",
 (floor(default(sWork, 0) / 60))+"H "+(default(sWork, 0) % 60)+"Min" AS "👶",
 (floor(default(oWork, 0) / 60))+"H "+(default(oWork, 0) % 60)+"Min" AS "👨‍💼",
 (floor(default(rWork, 0) / 60))+"H "+(default(rWork, 0) % 60)+"Min" AS "👨‍🎓",
 (floor(default(tWork, 0) / 60))+"H "+(default(tWork, 0) % 60)+"Min" AS "👨‍🏫",
 (floor(default(pWork, 0) / 60))+"H "+(default(pWork, 0) % 60)+"Min" AS "👷",
 startOWorkAt AS "⏰",
 finishOWorkAt AS "🕰️"
 
 from "00 - Main vault/Notes/Daily Notes"
 where contains(week, "<%moment(tp.file.title).format("GGGG-[W]WW")%>")
 sort file.name ASC
```
***
### 💰 Work payment
```dataviewjs
// Convert minutes to "Xh Ym" format
const formatTime = (minutes) => {
    const hours = Math.floor(minutes / 60) % 24;
    const mins = minutes % 60;
    return `${hours}H ${mins}Min`;
};

dv.table(
    ["Day", "🤹‍♂️", "👶", "👨‍💼", "👨‍🎓", "👨‍🏫", "👷", "⏱️", "💸"],
    dv.pages('"00 - Main vault/Notes/Daily Notes"')
      .where(p => p.week && p.week.includes("<%moment(tp.file.title).format("GGGG-[W]WW")%>"))
      .sort(p => p.file.name, 'asc')
      .map(p => [
          p.file.link,
          Math.abs((p.hWork||0)*(p.hWorkDh||1)/60).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + "Dh",
          Math.abs((p.sWork||0)*(p.sWorkDh||1)/60).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + "Dh",
          Math.abs((p.oWork||0)*(p.oWorkDh||1)/60).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + "Dh",
          Math.abs((p.rWork||0)*(p.rWorkDh||1)/60).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + "Dh",
          Math.abs((p.tWork||0)*(p.tWorkDh||1)/60).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + "Dh",
          Math.abs((p.pWork||0)*(p.pWorkDh||1)/60).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + "Dh",
          formatTime((p.hWork||0)+(p.sWork||0)+(p.oWork||0)+(p.rWork||0)+(p.pWork||0)),
          (Math.abs((p.hWork||0)*(p.hWorkDh||1)/60)+
          Math.abs((p.sWork||0)*(p.sWorkDh||1)/60)+ 
          Math.abs((p.oWork||0)*(p.oWorkDh||1)/60)+ 
          Math.abs((p.rWork||0)*(p.rWorkDh||1)/60)+ 
          Math.abs((p.pWork||0)*(p.pWorkDh||1)/60)).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + "Dh"
      ])
);
```
***
### 🏋️‍♂️ GYM time
```dataview
 table without id
 file.link AS "Day",
 Cal AS "🔥",
 (floor(default(gymMin, 0) / 60))+"H "+(default(gymMin, 0) % 60)+"Min"  AS "🏋️‍♂️",
 default(gymKg, 0)+"Kg" AS "🏋️",
 (floor(default(runingMin, 0)/(60*60))) + "H " + (floor(default(runingMin, 0)/60)%60) + "Min " + 
 (default(runingMin,0)%60) +"s" AS "🏃",
 default(runingKm+"Km", null) AS "🏃‍♂️",
 default(runingAS+"Km/h", null) AS "🏃💨",
 default(springMaxSpeed+"Km/h", null) AS "🏎️💨",
 Steps AS "👨‍🦯",
 default(travelingDist+"Km",null) AS "🚶‍♂️",
 pushUpReps AS "Push-up",
 setUpReps AS "Sit-up",
 squadReps AS "Squat "
 
 from "00 - Main vault/Notes/Daily Notes"
 where contains(week, "<%moment(tp.file.title).format("GGGG-[W]WW")%>")
 sort file.name ASC
```
***
### 💻 Fun Time
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
 where contains(week, "<%moment(tp.file.title).format("GGGG-[W]WW")%>")
 sort file.name ASC
```
***
### 👮 Personal Space
```dataviewjs
dv.table(
    ["Day", "😁", "💸", "💰", "💤", "😒", "⏰", "🕰️"],
    dv.pages('"00 - Main vault/Notes/Daily Notes"')
      .where(p => p.week && p.week.includes("<%moment(tp.file.title).format("GGGG-[W]WW")%>"))
      .sort(p => p.file.name, 'asc')
      .map(p => [
          p.file.link,
          p.gTime ? "✔️" : "❌", 
          (p.moneyInDh||0).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + "Dh", 
          (p.moneyInDh||0 + Math.abs((p.hWork||0)*(p.hWorkDh||1)/60)+
          Math.abs((p.sWork||0)*(p.sWorkDh||1)/60)+ 
          Math.abs((p.eWork||0)*(p.eWorkDh||1)/60)+ 
          Math.abs((p.oWork||0)*(p.oWorkDh||1)/60)+ 
          Math.abs((p.rWork||0)*(p.rWorkDh||1)/60)+ 
          Math.abs((p.pWork||0)*(p.pWorkDh||1)/60)).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + "Dh",
          Math.floor(dv.func.default(p.meTime, 0) / 60) + "H " +
          (dv.func.default(p.meTime, 0) % 60) + "Min",
          p.bTime ? "❌ "+p.bTime : "✔️",
          p.wokedAt || '_',
          (p.sleptAt || "_")
      ])
);
```


