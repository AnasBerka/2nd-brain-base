---
tags:
  - Logging/Daily/<%moment(tp.file.title,"YYYY-MM-DD").format("YYYY")%>/<%moment(tp.file.title,"YYYY-MM-DD").format("MM")%>
Creation date: <%tp.date.now("YYYY/MM/DD HH:mm")%>
week:
  - <%moment(tp.file.title).format("GGGG-[W]WW")%>
cssclasses:
  - daily
  - <%tp.date.now("dddd",0,tp.file.title,"YYYY-MM-DD").toLowerCase()%>
banner: "[[NoteBanner.jpg]]"
banner_x: 0
banner_y: 0.644
isCompleted: 
aliases:
---
 
# DAILY NOTE
## <%moment(tp.file.title).format("dddd, MMMM Do YYYY")%>

***
### 📜 Journal
####  Log without timing


***
### 📝 Today’s tasks
```tasks
due <%moment(tp.file.title).format("YYYY-MM-DD")%>
sort by priority
sort by description ASC
```
---
### 🔔 Upcoming events (this month)
```tasks
(tag includes #Logging/SDay/BDay) OR (tag includes #RIP ) OR (tag includes #SDay) OR (tag includes #Payment)
scheduled in <%moment(tp.file.title).subtract(1, "days").format("YYYY-MM-DD")%> <%moment(tp.file.title).add(30, "days").format("YYYY-MM-DD")%>
sort by status
sort by priority 
sort by scheduled 
sort by description ASC
```
***

### ☢️Habits
#### 🛐 Salat

- 🕋 Time for Quran & Salat Fajer ⏲️ 05:00 - 06:00   
	- Quran reading 
		- [quranReading::] 
		- [quranReadingO::] 
		- [quranReadingE::]
	- Quran’s 7izb 
		- [Quran/7izb::] 
		- [Quran/7izbO::] 
		- [Quran/7izbE::] 

- 🛐 Prayers on time ⏲️ 22:00 - 22:15  
	- Salat on time [salatOnTime::] 
	- Fajer [salatFajer::] 
	- Doher [salatDohr::] 
	- Aaser [salatAaser::] 
	- Meghrb [salatMeghrb::] 
	- Ishae [salatIshae::]
	

#### 👨‍💼 Work time
Self-improvements (in Min): 
- [hWork::]
- [sWork::]

Research (in Min):
- [rWork::]

Work (in Min):
- [oWork::]
- [tWork::]  [twWork::]
- [eWork::]   
- [mWork::]
- [pWork::] 

Payment (in Dh/H):
- [hWorkDh::0]
- [sWorkDh::30]
- [rWorkDh::100]
- [oWorkDh::100]
- [tWorkDh::100]
- [mWorkDh::100]
- [eWorkDh::50]
- [pWorkDh::108]

Work timing:
- [startOWorkAt::]
- [finishOWorkAt::]
- [startHWorkAt::]
- [finishHWorkAt::]


#### 🎓 Research Index:
- Google based :  
	- [AB/hGIndex::] 
	- [AB/i10GIndex::] 
	- [AB/GCitations::] 
	- [AB/gGIndex::] 
	- [AB/CPPGScore::] 
	- [AB/hGScore::] 
	- [AB/gGScore::] 
	- [AB/GCiteScore::]   
	- [AB/CitationsGY::] 
- Researchgate : 
	- [AB/hRIndex::] 
	- [AB/i10RIndex::] 
	- [AB/RCitations::] 
	- [AB/gRIndex::] 
	- [AB/CPPRScore::] 
	- [AB/hRScore::] 
	- [AB/gRScore::] 
	- [AB/RCiteScore::] 
	- [AB/CitationsRY::]
	- [AB/RIS::] 
- General : 
	- [AB/CoAScore::]  
	- [AB/OScore::]  
	- [AB/PScore::] 
	- [AB/PapersS::] 
	- [AB/PapersP::]

#### 🏋️‍♂️ GYM time
- ⭐ Personal stats:
	- [myWeight::]
	- [myHeight::]

- 🏃Run Lord Cj RUUUN ⏲️ 06:00 - 06:20 
	- Running 
		- [runingKm::] 
		- [runingMin::] 
		- [runingAS::]
	- Springing 
		- [springMaxSpeed::] 
		- [springMaxSS::]

- 💪 GYM time  ⏲️ 06:20 - 07:00 
	- Stats 
		- [gymKg::] 
		- [gymMin::] 
		- [Cal::]
	- Active time 
		- [activeTime::] 
		- [activeTravelingDist::] 
		- [activeCal::] 
		- [activeSteps::]
	- Leveling up 
		- [pushUpReps:: ] 
		- [pushUpRepsMax::] 
		- [setUpReps:: ] 
		- [setUpRepsMax::] 
		- [squadReps::  ]
		- [squadRepsMax::]
	- Basic exercices 
		- [pushBarMaxKg::] 
		- [pushBarMaxRep::] 
		- [pullBarMaxKg::] 
		- [pullBarMaxRep::] 
		- [squadBarMaxKg::] 
		- [squadBarMaxRep::] 
		- [curlDumpMaxKg::] 
		- [curlDumpMaxRep::]
	- IT training 
		- [typingTraining::] 
		- [typingSpeed::]

How much I moved this day :
- [travelingDist::]
- [Steps::]
- [wCal::]

#### 🖥️ Fun Time

- 👺 Having fun while watching stuffs ⏲️ 23:00 - 23:30 :
	- Movies [movieMin::]
	- Animes [animeEp::]
	
- 📓 Manga & Manhwa ⏲️ 23:30 - 23:59 :
	- Reading Manga [RManga::]

- 📙 Light & Web novel ⏲️ 23:30 - 23:59 :
	- Books reading [BRead::]
	- Lignt/Web novels reading [LWRead::]
	- Lignt/Web novels time [LWReadMin::]
 
 - 👾 Gaming / ROG time ⏲️ 18:00-20:00 :
	- StriX [gamingPCMin::]
	- AS21 [gamingMobileMin::]

- 📱 Browsing Social Media ⏲️ 22:15-23:00 :
	- Check all SMs [smMin::]
	- Facebook  [Fb::]
	- Instagram [Insta::]

Phone statics :
- [UnlockNbr::]
- [ScreenTime::]

#### 💰 Money
Various transaction for the day :
	- 

- [vOwnerfirstnameOwnerlastname::] 
- [vCDBalance::]
- [vCjBank2Bank::]
- [vBBM::]
- [vCIH::]
- [vBNP::]
- [vCache::]

How much money I spent or saved (in Dh)
- [moneyInDh::]
- [dailyDh:: 69]
	
Divided into:
	- Fixed Essentials [feDh::] 
	- Variable Essentials [veDh::] 
	- Non-essential consumption [dsDh::] 
	- Personal Development [pdDh::] 
	- Social & Lifestyle [slDh::] 
	- Irregular / Unexpected [iuDh::] 
	- Financial Commitments [fcDh::] 

```dataviewjs
const pages = dv.pages('"00 - Main vault/Notes/Daily Notes"')
  .where(p => p.file.day <= dv.date("<%moment(tp.file.title).format("YYYY-MM-DD")%>"))
  .array(); // 🔑 Convert DataArray -> normal array

// Helper function to safely extract a field value
function getFieldValue(page, fieldName) {
  return Number(page[fieldName]) || 0;
}

// Group pages by day
const groupedByDay = pages.reduce((acc, page) => {
  const day = page.file.day.toISODate(); // Convert to ISO date string for grouping
  if (!acc[day]) acc[day] = [];
  acc[day].push(page);
  return acc;
}, {});

// Calculate `dh` and `e` for each day
const dailyValues = Object.entries(groupedByDay).map(([day, dayPages]) => {
  const dh = dayPages.reduce(
    (sum, p) => sum + getFieldValue(p, "vCIH") + getFieldValue(p, "vBBM") + getFieldValue(p, "vCache"),
    0
  );
  const e = dayPages.reduce((sum, p) => sum + getFieldValue(p, "vBNP"), 0);
  return { day, dh, e };
});

// Find the most recent day where both `dh` and `e` are available
const mostRecent = dailyValues
  .filter(({ dh }) => dh !== null) // Ensure `dh` exists (can be 0, positive, or negative)
  .sort((a, b) => new Date(b.day) - new Date(a.day))[0]; // Sort by date descending

// Extract `dh` and `e` for the most recent day
const dh = mostRecent ? mostRecent.dh : 0;
const e = mostRecent ? mostRecent.e : 0;

// Check for Zero
const EPS = 1e-2;
function isZero(x) {
  return Math.abs(x) < EPS;
}

// Perform calculations
const sumBank2Bank = pages
  .map(p => getFieldValue(p, "vCjBank2Bank"))
  .reduce((a, b) => a + b, 0);

const sumMoneyInDh = pages
  .map(p => getFieldValue(p, "moneyInDh"))
  .reduce((a, b) => a + b, 0);

const sumCDBalance = pages
  .map(p => getFieldValue(p, "vCDBalance"))
  .reduce((a, b) => a + b, 0);

const TH = dh + e * 11; // Total holdings
const TT = sumCDBalance + TH; // Total expected value
const missingValues = TH - sumMoneyInDh - sumBank2Bank;

// Display results
dv.paragraph(`📌 Pending transaction: **${(isZero(sumBank2Bank)?0:sumBank2Bank).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}** Dh`);
dv.paragraph(`⚖️ Credit/Debit balance: **${(isZero(sumCDBalance)?0:sumCDBalance).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}** Dh`);
dv.paragraph(`🏦 Currently in my banks vault: **${(isZero(sumMoneyInDh)?0:sumMoneyInDh).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}** Dh`);
if (!isZero(sumBank2Bank) || !isZero(sumCDBalance)) {
  dv.paragraph(`💸 Normally it should be: **${(sumMoneyInDh + sumBank2Bank + sumCDBalance).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}** Dh`);
}
if(!isZero(TH-sumMoneyInDh) && !isZero(TH)){
	dv.span(`<br>⚠️ Real values = **${TT.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}** Dh`);
	dv.span(`<br>⚠️ To money: **${(TH - sumMoneyInDh).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}** Dh`);
	dv.span(`<br>⚠️ To CjBank: **${(-sumBank2Bank).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}** Dh`);
	dv.span(`<br>⚠️ Missing values: **${missingValues.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}** Dh`);
	dv.span(`<br>⚠️ Expected value: **${TH.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}** Dh`);
};
```

#### 🧑‍🤝‍🧑 Social media stats:
- Facebook [friendsFb::] [RequestsFb::]
- Instagram [followingInsta::] [followersInsta::]
- Github [followingGH::] [followersGH::]
- YouTube [subsIGX::] [subsIG0::]
- ResearchGate [followingRG::] [followersRG::]
- LinkedIn [ConnectionLI::] [followersLI::]
- Contacts [NbrContacts::]

#### 💤 Personal Space
How many hours for me to sleep & relax (in min) and other stats: 
	- [meTime::]
	- [gTime::]
	- [bTime::]
	- [wokedAt::]
	- [sleptAt::]

***
### Links
=> [[00 - Main vault/Notes/Daily Notes/<%moment(tp.file.title,"YYYY-MM-DD").subtract(1,'day').format("YYYY")%>/<%moment(tp.file.title,"YYYY-MM-DD").subtract(1,'day').format("MM")%>/<%moment(tp.file.title,"YYYY-MM-DD").subtract(1,'day').format("YYYY-MM-DD")%>|View previous day]]
=> [[00 - Main vault/Notes/Weekly reports/<%moment(tp.file.title,"YYYY-MM-DD").format("YYYY")%>/<%moment(tp.file.title).format("GGGG-[W]WW")%>|View the weekly report]]

---
### Additional variables (from DBs)
[fillData::false]