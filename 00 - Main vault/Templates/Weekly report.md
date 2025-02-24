---
tags:
  - Weekly
banner: "[[Sky1Banner.jpg]]"
banner_x: 0
banner_y: 0.974
cssclasses:
  - daily
isCompleted:
---

[[00 - Main vault/Notes/Weekly reports/<%moment(tp.file.title).subtract(1,'week').format("gggg-[W]ww")%>|⬅️]]|[[00 - Main vault/Notes/Weekly reports/<%moment(tp.file.title).add(1,'week').format("gggg-[W]ww")%>|➡️]]
***
Browse each day individually: 
[[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('Week').add(0,'day').format("YYYY-MM-DD")%>| Monday]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('Week').add(1,'day').format("YYYY-MM-DD")%>| Tuesday]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('isoWeek').add(2,'day').format("YYYY-MM-DD")%>| Wednesday]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('isoWeek').add(3,'day').format("YYYY-MM-DD")%>| Thursday]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('isoWeek').add(4,'day').format("YYYY-MM-DD")%>| Friday]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('isoWeek').add(5,'day').format("YYYY-MM-DD")%>| Saturday]] | [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title).startOf('isoWeek').add(6,'day').format("YYYY-MM-DD")%>|Sunday]]
***
***

### Summary about the week 🗒️
- [ ] Add summary of the week <%moment(tp.file.title).format("[W]ww")%> here ⏬  
***
***

 ```dataview
 table without id
 file.link AS "Day",
 choice(gTime,"✔️","❌") AS "😁",
 salatOnTime AS "🛐",
 moneyInDh AS "💸",
 hWork AS "👨‍🎓",
 oWork AS "👨‍💼",
 rWork AS "👨‍🏫",
 gymMin AS "🏋️‍♂️",
 pushUpReps AS "Push-up",
 setUpReps AS "Sit-up",
 squadReps AS "Squat",
 runingKm AS "Runing"
 
 from "00 - Main vault/Notes/Daily Notes"
 where week = "<%moment(tp.file.title).format("gggg-[W]ww")%>"
 sort file.name ASC
```