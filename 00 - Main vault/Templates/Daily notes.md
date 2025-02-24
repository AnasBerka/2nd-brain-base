---
tags:
  - Daily
Creation date: <%tp.date.now("YYYY/MM/DD HH:mm")%>
week:
  - <%moment(tp.file.title).format("gggg-[W]ww")%>
cssclasses:
  - daily
  - <%tp.date.now("dddd",0,tp.file.title,"YYYY-MM-DD").toLowerCase()%>
banner: "[[NoteBanner.jpg]]"
banner_x: 0
banner_y: 0.644
isCompleted:
---
 
# DAILY NOTE
## <%moment(tp.file.title).format("dddd, MMMM Do YYYY")%>
***
### Journal
#### {{for TIME}} use ‘ctrl + shift + /’
Customize this template to your liking!

***

### New tasks
- [ ] Morning check for 📅 <%moment(tp.file.title).format("YYYY-MM-DD")%> about everything ⏬ 
***
### On-going tasks:
```tasks
not done
priority is above lowest
sort by priority 
sort by due date 
sort by description
```
***

### Habits
#### Salat
How many prayers I couldn't pray on time (valid only if all on time)
- salatOnTime:: 0 

	- salatFajer:: false
	- salatDohr:: false
	- salatAaser:: false
	- salatMeghrb:: false
	- salatIshae:: false

#### Work time
Self-improvements (in HH):
- hWork:: 0 
- startHWorkAt:: 
- finishHWorkAt:: 

Official Work (in HH):
- oWork:: 0 
- startOWorkAt:: 
- finishOWorkAt:: 

Research Work (in HH):
- rWork:: 0 
- startRWorkAt:: 
- finishRWorkAt:: 

#### GYM time
How much weight I trained with (ref the app):
- gymKg:: 0
- myWeight:: 0
- myHeight:: 0
- pushBarbellMaxKg:: 0
- pushBarbellMaxRep:: 0
- pullBarMaxKg:: 0
- pullBarMaxRep:: 0
- pressLegMaxKg:: 0
- pressLegMaxRep:: 0
- pullDumpMaxKg:: 0
- pullDumpMaxRep:: 0
- SpringMaxSpeed:: 0
- SpringMaxSS:: 0

GYM activities (GYM in Min & number of repetition for others):
- gymMin:: 0 

	- pushUpReps:: 0 
	- setUpReps:: 0 
	- squadReps:: 0 

How much I ran this day (in Km)
- runingKm:: 0 

#### Fun Time
Episodes watched (num of episodes):
- animeEp:: 0

Watching random stuffs (in Min):
- movieMin:: 0 

Gaming (in Min):
- gamingMin:: 0 

Browsing Social Media (in Min):
- smMin:: 0 

Doing random stuffs on the ROG (in HH):
rwROG:: 0 

#### Money
How much mony I spent or saved (in Dh)
moneyInDh::  0

#### Personal Space
How many hours for me to sleep & relax (in HH): 
meTime:: 0
gTime:: false
bTime:: 0
sleptAt:: 
wokedAt:: 
***
### Links
=> [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title,"YYYY-MM-DD").subtract(1,'day').format("YYYY-MM-DD")%>|View previous day]]
=> [[00 - Main vault/Notes/Weekly reports/<%moment(tp.file.title).format("gggg-[W]ww")%>|View the weekly report]]
=> [[00 - Main vault/Notes/Monthly reports/<%moment(tp.file.title).format("YYYY-MM _ MMMM")%>|View the monthly report]]
=> [[00 - Main vault/Notes/Annually reports/<%moment(tp.file.title).format("YYYY")%>|View the annually report]]

