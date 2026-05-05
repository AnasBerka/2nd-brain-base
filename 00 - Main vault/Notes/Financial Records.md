---
excalidraw-plugin: parsed
tags:
  - excalidraw
cssclasses:
  - daily
  - cosmos
---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠== You can decompress Drawing data with the command palette: 'Decompress current Excalidraw file'. For more info check in plugin settings under 'Saving'
***
#  Transactional relationship  for [[OwnerFirstName OwnerLastName|Lord Cj]] 💸
```dataviewjs
/***** Single-pass, semantics-preserving rewrite *****/

/* ---- helpers (unchanged) ---- */
function toCamelCase(str) {
  return 'v' + str
    .replace(/[^a-zA-Z0-9]+/g, ' ')
    .split(' ')
    .map((word, index) => word.charAt(0).toUpperCase() + word.slice(1).toLowerCase())
    .join('');
}

const FAMILY_TAGS = new Set([
"vBrother","vSister","vMother","vFather","vMyFamily","vMyCommunity","vMyFriends","vMyProfessionalCircle"
]);

//new Set([
//"vRogStrixG152022","vSamsungA22s2021"
//]);

/* ---- headings (unchanged) ---- */
dv.paragraph(`<h2><strong>🤝 My financial relationship :</strong></h2>`);

/* ---- 0) Load sources ONCE (order identical to your code) ---- */
const PEOPLE = dv.pages('"00 - Main vault/Notes/Relationships"').sort(p => p.file.name, 'asc');
const DAILY  = dv.pages('"00 - Main vault/Notes/Daily Notes"').sort(p => p.file.name, 'asc'); // NOTE: no sort here on purpose to preserve original ordering behavior

/* Build the allowlist of v* variable names from People (excluding vOwnerfirstnameOwnerlastname) */
const allow = new Set();
for (const person of PEOPLE) {
  const vName = toCamelCase(person.file.name);
  if (vName !== "vOwnerfirstnameOwnerlastname") allow.add(vName);
}

const MACHINES_TAGS = new Set();
const MACHINES = dv.pages('"00 - Main vault/Notes/Relationships/Machines"').sort(p => p.file.name, 'asc');
for (const machine of MACHINES) {
  const vName = toCamelCase(machine.file.name);
  MACHINES_TAGS.add(vName);
}

const Diverses_TAGS = new Set();
const Diverses = dv.pages('"00 - Main vault/Notes/Relationships/Diverses"').sort(p => p.file.name, 'asc');
for (const diverse of Diverses) {
  const vName = toCamelCase(diverse.file.name);
  Diverses_TAGS.add(vName);
}

/* ---- 1) First section accumulators (exact sentinels & logic) ---- */
let totalValue = 0, fam = 0, machines = 0, diverses = 0;
let totalS = 0, totalR = 0;

let minDhS = -6e9, maxDhS = 0, minDhR = 6e9, maxDhR = 0;
let DminDhS = '', DmaxDhS = '', DminDhR = '', DmaxDhR = '';

/* per-person running value (like your per-person inner loop’s `value`) */
const acc = new Map(); // vName -> { value: number }

// Map vName -> People note title (with spaces), e.g. vJohnDoe -> "John Doe"
const vNameToTitle = Object.fromEntries(
  PEOPLE.map(p => [toCamelCase(p.file.name), p.file.name])
);

// Treat anything smaller than 0.01 Dh (two decimals) as zero for display
const EPS = 0.005; // half-cent rounding guard
const isZero = (n) => Math.abs(Number(n) || 0) < EPS;

/* single pass over Daily Notes; update all persons present in this note */
for (const note of DAILY) {
  // iterate only keys that match our allowlist; avoids O(P) checks per note
  for (const [k, raw] of Object.entries(note)) {
    if (!allow.has(k)) continue;
    const rawValues = Array.isArray(raw) ? raw : [raw];
    for (const val of rawValues) {
    const m = String(val).match(/-?\d+(\.\d+)?/);
    if (!m) continue;
    const newV = Number(m[0]);
    if (!newV) continue;
    if (isZero(newV)) continue;

    let a = acc.get(k);
    if (!a) { a = { value: 0 }; acc.set(k, a); }

    const newValDh = isZero(a.value + newV)?0:a.value + newV;
    if (MACHINES_TAGS.has(k) | Diverses_TAGS.has(k)){//Skip machines...
	    a.value = newValDh;
	    continue;
    }
    const newValP  = (a.value * newV > 0) ? newV : newValDh; // preserved (not displayed)

	//dv.paragraph('    NEW:'+note.file.name+" "+newValDh+'   vDh:'+newV+'    vRise:'+a.value);
    //if (newV > 0) {
      if (newValDh > 0) {
        if (newValDh > maxDhR) { 
          maxDhR = newValDh; 
          DmaxDhR = vNameToTitle[k] ?? k.slice(1);  // <— use title with spaces
        }
        if (newValDh < minDhR) { 
          minDhR = newValDh; 
          DminDhR = vNameToTitle[k] ?? k.slice(1);
        }
        if (!FAMILY_TAGS.has(k)) totalR += newValDh; // preserve the exact branch and amount
	    }
    //} else { // newV < 0
      else if (newValDh < 0) {
        if (newValDh < maxDhS) { 
          maxDhS = newValDh; 
          DmaxDhS = vNameToTitle[k] ?? k.slice(1);
        }
        if (newValDh > minDhS) { 
          minDhS = newValDh; 
          DminDhS = vNameToTitle[k] ?? k.slice(1);
        }
        if (!FAMILY_TAGS.has(k)) totalS += newValDh;
      }
    //}

    a.value = newValDh;
    }
  }
}




/* Rows construction (unchanged rules, same special names/aliases) */
let rows1 = [], rows2 = [], rows3 = [], rows4 = [], rows5 = [];

//helpers
const formatMoneyE = (money) => {
 return `<div class="cell-right">${(money).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })} Dh</div>`;
};


for (const page of PEOPLE) {
  const vName = toCamelCase(page.file.name);
  if (vName === "vOwnerfirstnameOwnerlastname") continue;
  const a = acc.get(vName);
  const value = Number(a ? a.value : 0);
  if (isZero(value)) continue;   // hide final-zero counterparties

  // family members with aliases
  if (vName === "vBrother") {
    fam += value;
    rows1.push([`[[${page.file.name}]]`, (value >= 0 ? `💸 I owe` : `💰 I lent`), formatMoneyE(Math.abs(value))]);
    continue;
  } else if (vName === "vSister") {
    fam += value;
    rows1.push([`[[${page.file.name}]]`, (value >= 0 ? `💸 I owe` : `💰 I lent`),
      formatMoneyE(Math.abs(value))]);
    continue;
  } else if (vName === "vMother") {
    fam += value;
    rows1.push([`[[${page.file.name}]]`, (value >= 0 ? `💸 I owe` : `💰 I lent`),
      formatMoneyE(Math.abs(value))]);
    continue;
  } else if (vName === "vFather") {
    fam += value;
    rows1.push([`[[${page.file.name}]]`, (value >= 0 ? `💸 I owe` : `💰 I lent`),
      formatMoneyE(Math.abs(value))]);
    continue;
  } else if (vName === "vMyFamily" || vName === "vMyCommunity" || vName === "vMyFriends" || vName === "vMyProfessionalCircle") {
    rows3.push([`[[${page.file.name}]]`, (value >= 0 ? `💸 I received` : `💰 I sent`),
      formatMoneyE(Math.abs(value))]);
    continue;
  } else if (MACHINES_TAGS.has(vName)){//Skip machines...
	    machines += value;
	    rows4.push([`[[${page.file.name}]]`, (value >= 0 ? `💸 I gained` : `💰 I spent`),
      formatMoneyE(value)]);
	    continue;
    } else if (Diverses_TAGS.has(vName)){//Skip diverses...
	    diverses += value;
	    rows5.push([`[[${page.file.name}]]`, (value >= 0 ? `💸 I gained` : `💰 I spent`),
      formatMoneyE(value)]);
	    continue;
    }

  // everyone else
  rows2.push([`[[${page.file.name}]]`, (value >= 0 ? `💸 I owe` : `💰 I lent`),
    formatMoneyE(value)]);

  totalValue += value;
}

/* totals (unchanged) */
// rows1.push([
//   "**TOTAL**",
//   (totalValue >= 0 ? `💰💸 <strong>Borrowing</strong>` : `💸💰 <strong>Loaning</strong>`),formatMoneyE(totalValue)]);
// rows1.push([
//   "**From my family:**",
//   (totalValue >= 0 ? `💰💸 <strong>Borrowing</strong>` : `💸💰 <strong>Loaning</strong>`),
//   (fam > 0 ? formatMoneyE(fam) : ``)
// ]);

/* tables (one per group) */
const _groups = [
  { rows: rows2, title: "👥 People",    col: "Full name" },
  { rows: rows3, title: "🏘️ Groups",    col: "Groups" },
  { rows: rows4, title: "🖥️ Machines",  col: "Machines" },
  { rows: rows5, title: "📦 Diverses",  col: "Item" },
  { rows: rows1, title: "👨‍👩‍👦 Family", col: "Member" },
];
for (const g of _groups) {
  if (!g.rows.length) continue;
  dv.paragraph(`<h4>${g.title}</h4>`);
  dv.table([g.col, "💰 / 💸", "Value"], g.rows);
}

/* ---- 2) “Official payments and taxes” (single pass across DAILY) ---- */
dv.paragraph(`<h2><strong>💲My official payments and taxes 💲</strong>:</h2>`);
const list = dv.el("ul", "");

let minDhdS = -6e9, maxDhdS = 0, minDhdR = 6e9, maxDhdR = 0, totaldS = 0, totaldR = 0;
let minDhPS = -6e9, maxDhPS = 0, minDhPR = 6e9, maxDhPR = 0, totalPS = 0, totalPR = 0;

let vRise = 0;
let pTime=0, sTime=0, rTime=0, oTime=0, hTime=0;
let pTimeDh=0, sTimeDh=0, rTimeDh=0, oTimeDh=0, hTimeDh=0;

let DminDhdS='', DmaxDhdS='', DminDhdR='', DmaxDhdR='';
let DminDhPS='',  DmaxDhPS='',  DminDhPR='',  DmaxDhPR='';

for (const p of DAILY.filter(p => p.vOwnerfirstnameOwnerlastname || p.hWork || p.oWork || p.rWork || p.sWork || p.pWork || p.moneyInDh).sort(x => x.file.name, 'asc')) {
  // moneyInDh
  const rawMoneyInDh = Array.isArray(p.moneyInDh) ? p.moneyInDh : [p.moneyInDh || 0];
  for (const mVal of rawMoneyInDh) {
  const dDh = Number(String(mVal).match(/-?\d+(\.\d+)?/)?.[0] || 0);
  vRise += dDh;
  if (dDh !== 0) {
    if (dDh > 0) {
      if (dDh > maxDhdR) { maxDhdR = dDh; DmaxDhdR = p.file.name; }
      if (dDh < minDhdR) { minDhdR = dDh; DminDhdR = p.file.name; }
      totaldR += dDh;
    } else {
      if (dDh < maxDhdS) { maxDhdS = dDh; DmaxDhdS = p.file.name; }
      if (dDh > minDhdS) { minDhdS = dDh; DminDhdS = p.file.name; }
      totaldS += dDh;
    }
  }
  }

  // times & rates (per note)
  const pushTime = (minVar, rateVar, accTimeName, accDhName) => {
    const mins = Number(p[minVar] || 0);
    if (!mins) return;
    const rate = Number(p[rateVar] || 0);
    const tempPay = mins * (rate > 0 ? rate : 0) / 60;
    switch (accTimeName) {
      case 'p': pTime += mins; pTimeDh += tempPay; break;
      case 's': sTime += mins; sTimeDh += tempPay; break;
      case 'r': rTime += mins; rTimeDh += tempPay; break;
      case 'o': oTime += mins; oTimeDh += tempPay; break;
      case 'h': hTime += mins; hTimeDh += tempPay; break;
    }
  };
  pushTime('pWork','pWorkDh','p','p');
  pushTime('hWork','hWorkDh','h','h');
  pushTime('sWork','sWorkDh','s','s');
  pushTime('rWork','rWorkDh','r','r');
  pushTime('oWork','oWorkDh','o','o');

  // vOwnerfirstnameOwnerlastname: official paid/donated list and totals
  const rawAnasBerka = Array.isArray(p.vOwnerfirstnameOwnerlastname) ? p.vOwnerfirstnameOwnerlastname : [p.vOwnerfirstnameOwnerlastname || 0];
  for (const aVal of rawAnasBerka) {
  const vDh = Number(String(aVal).match(/-?\d+(\.\d+)?/)?.[0] || 0);
  if (vDh !== 0) {
    dv.el("li",
      `[[${p.file.name}]] : ` +
      (vDh > 0
        ? `💰 I officially received ${vDh.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })} Dh`
        : `💸 I officially donated ${Math.abs(vDh).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })} Dh`)
    );
    if (vDh > 0) {
      if (vDh > maxDhPR) { maxDhPR = vDh; DmaxDhPR = p.file.name; }
      if (vDh < minDhPR) { minDhPR = vDh; DminDhPR = p.file.name; }
      totalPR += vDh;
    } else {
      if (vDh < maxDhPS) { maxDhPS = vDh; DmaxDhPS = p.file.name; }
      if (vDh > minDhPS) { minDhPS = vDh; DminDhPS = p.file.name; }
      totalPS += vDh;
    }
  }
  }
}

/* add Calendar pages (unchanged second pass) */
const cal = dv.pages('"00 - Main vault/Notes/Calenders"').filter(p => p.hWork || p.oWork || p.rWork || p.sWork || p.pWork).sort(p => p.file.name, 'asc');
for (const p of cal) {
  const add = (mins, rate, toTime, toDh) => {
    const m = Number(p[mins] || 0); if (!m) return;
    const pay = m / 60 * Number(p[rate] || 0);
    switch (toTime) {
      case 'h': hTime += m; hTimeDh += pay; break;
      case 'p': pTime += m; pTimeDh += pay; break;
      case 's': sTime += m; sTimeDh += pay; break;
      case 'r': rTime += m; rTimeDh += pay; break;
      case 'o': oTime += m; oTimeDh += pay; break;
    }
  };
  add('hWork','hWorkDh','h','h');
  add('pWork','pWorkDh','p','p');
  add('sWork','sWorkDh','s','s');
  add('rWork','rWorkDh','r','r');
  add('oWork','oWorkDh','o','o');
}

/* Normalize edge cases (unchanged) */
if (minDhR === 6e9) minDhR = 0;
if (minDhS === -6e9) minDhS = 0;
if (minDhPR === 6e9) minDhPR = 0;
if (minDhPS === -6e9) minDhPS = 0;

/* ---- 3) Total Summary table (unchanged) ---- */
let rowsTS = [];
dv.paragraph(`<h2><strong>🏦 Total Summary:</strong></h2>`);

const moneyOwner = (money, owner) => {
  const file  = encodeURIComponent(owner);   // The note name

  return `<div class="cell-stack"><div class="stack-top"> ${Math.abs(money).toLocaleString("fr-FR", {
          minimumFractionDigits: 2, maximumFractionDigits: 2
        })} Dh </div>
      <div class="stack-bottom">(<a href="obsidian://open?vault=Notes&file=${file}">${owner}</a>)</div></div>`;
};



rowsTS.push([`💸💰 <strong>Donations</strong>`,
  moneyOwner(minDhPS,DminDhPS),
  moneyOwner(maxDhPS,DmaxDhPS),
  formatMoneyE(totalPS)]);

rowsTS.push([`📉📉 <strong>Overall borrowing</strong>`,
  moneyOwner(minDhR,DminDhR),
  moneyOwner(maxDhR,DmaxDhR),
  formatMoneyE(totalR)]);

rowsTS.push([`📈📈 <strong>Overall loaning`,
  moneyOwner(minDhS,DminDhS),
  moneyOwner(maxDhS,DmaxDhS),
  formatMoneyE(totalS)]);

rowsTS.push([`💲💲 <strong>Amount actually paid</strong> `,
  moneyOwner(minDhPR,DminDhPR),
  moneyOwner(maxDhPR,DmaxDhPR),
  formatMoneyE(totalPR)]);

rowsTS.push(["---", "---", "---", "---"]);

rowsTS.push([`👨‍🏫💰 <strong>Amount due to be paid</strong>`, "--", "--",
  formatMoneyE(pTimeDh + rTimeDh + sTimeDh + hTimeDh + oTimeDh)]);

rowsTS.push([`👨‍💼💰 <strong>Money I have spent</strong> (in a 24H)`,
  moneyOwner(minDhdS,DminDhdS),
  moneyOwner(maxDhdS,DmaxDhdS),
  `--`]);

rowsTS.push([`💰👨‍💼 <strong>Money I have conserved</strong> (in a 24H)`,
	moneyOwner(minDhdR,DminDhdR),
	moneyOwner(maxDhdR,DmaxDhdR),
  `--`]);

dv.table(["Transactions type", "Min (ref)", "Max (ref)", "Total"], rowsTS);

/* ---- 4) Current status (unchanged) ---- */
dv.paragraph(`<h2><strong>📌 Current situation:</strong></h2>`);
dv.paragraph(`
  <ul>
    <li>
      ${totalValue >= 0 
        ? `💰💸 <strong>Borrowing ${totalValue.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })} Dh</strong> `+(fam>0 ? `(${fam.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })} Dh stored for family 👨‍👩‍👦)`:``)
        : `💸💰 Loaning ${Math.abs(totalValue).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })} Dh `+(fam>0 ? `(${fam.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })} Dh stored for family 👨‍👩‍👦)`:``)
      }
    </li>
    <li><strong> 💲💲 Payment I got so far: </strong><i>${totalPR.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}</i> Dh 
    ${(pTimeDh+rTimeDh+sTimeDh+hTimeDh+oTimeDh-totalPR)>0 ?
    `<ul><li>=> Expecting additional ${(pTimeDh+rTimeDh+sTimeDh+hTimeDh+oTimeDh-totalPR).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })} Dh
    </li></ul>`:``
    }
    </li>
    <li><strong> 🏦🏦 Balance currently: </strong><i>${vRise.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}</i> Dh</li>
  </ul>
`);

```
#### Global statistique
```tracker
searchType: dvField
folder: "00 - Main vault/Notes/Daily Notes"
searchTarget: feDh,veDh,dsDh,pdDh,slDh,iuDh,fcDh,vOwnerfirstnameOwnerlastname
datasetName: feDh,veDh,dsDh,pdDh,slDh,iuDh,fcDh,vOwnerfirstnameOwnerlastname
fitPanelWidth: true
aspectRatio: 1

pie:
	title: My spending 
    label: '{{sum(dataset(0))}} Dh,{{sum(dataset(1))}} Dh,{{sum(dataset(2))}} Dh,{{sum(dataset(3))}} Dh,{{sum(dataset(4))}} Dh,{{sum(dataset(5))}} Dh,{{sum(dataset(7))-(sum(dataset(6))+sum(dataset(5))+sum(dataset(4))+sum(dataset(3))+sum(dataset(2))+sum(dataset(1))+sum(dataset(0)))}} Dh'
    data: '{{sum(dataset(0))}},{{sum(dataset(1))}},{{sum(dataset(2))}},{{sum(dataset(3))}},{{sum(dataset(4))}},{{sum(dataset(5))}},{{sum(dataset(7))-(sum(dataset(6))+sum(dataset(5))+sum(dataset(4))+sum(dataset(3))+sum(dataset(2))+sum(dataset(1))+sum(dataset(0)))}}'
    extLabel: '{{sum(dataset(0))}} Dh,{{sum(dataset(1))}} Dh,{{sum(dataset(2))}} Dh,{{sum(dataset(3))}} Dh,{{sum(dataset(4))}} Dh,{{sum(dataset(5))}} Dh,{{sum(dataset(7))-(sum(dataset(6))+sum(dataset(5))+sum(dataset(4))+sum(dataset(3))+sum(dataset(2))+sum(dataset(1))+sum(dataset(0)))}} Dh'
	showExtLabelOnlyIfNoLabel: true
	showLegend: true
	dataColor: '#E69F00, #56B4E9, #009E73, #F0E442, #0072B2, #D55E00, blue'
	ratioInnerRadius: 0.6
	dataName: Fixed Essentials,Variable Essentials,Discretionary Spending,Personal Development,Social & Lifestyle,Irregular / Unexpected,Financial Commitments
    legendPosition: right
    legendOrientation: vertical	
```
![[Work _ Stat#Global statistiques]]

#### 💸 Money Log 💰
- [ ] 💰 I need Logs of BBM for the start and for months : **2020-, 2021-,2022-(-12),2023-,2024-(1+2+3+4+5+6+7)** ⏫ 📅 2026-07-31

![[OwnerFirstName OwnerLastName#💸 Money Log]]

***
# Excalidraw Data

## Text Elements
CIH ^ucDHO5av

BBM ^wQXNc2If

BP ^DuahAUF6

3Dh ^DHNYbrZW

22Dh ^IPwf36qx

7€ ^dz1GlPWK

80Dh ^jITqP4PS

(67.62Dh/day) ^fUtbfzqj

(xxxxxx-xxxxx*6)Dh ^JHpQVcvu

365.25days ^UqEsJyQh

=  6.01Dh ^t5aezLT6

10.6261 ^oQv25AOY

%%
## Drawing
```compressed-json
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
```
%%