---
aliases:
  - my
tags:
  - Owned
Serial number: 
Full Technical Name: 
Country: 
Organization: 
Notes: My personal
Birthday: 
Owner(s): 
Last modification: ""
banner: "[[FriendsBanner.jpg]]"
banner_x: 0
banner_y: 0.546
cssclasses:
  - daily
  - sNote
---
# <% tp.file.title %>
## My machines

> _My lovely soldiers_
***
### Important events
#### Added to chart
on 

#### 1st day in my arsenal 
on .

***
### Important notes
#### 

***
### Tasks
#### In progress ⏳
```tasks
not done
description includes [[<% tp.file.title %>
sort by priority
sort by due date 
sort by description ASC
```

#### Done ✔️
```tasks
status.type is done
tags do not include #Logging/SDay/BDay
description includes [[<% tp.file.title %>
sort by priority
sort by due date 
sort by description ASC
```

#### Cancelled ❌
```tasks
status.type is cancelled
description includes [[<% tp.file.title %>
sort by priority
sort by due date 
sort by description ASC
```
#### Birthdays 🍰
```tasks
done
tags include #Logging/SDay/BDay
description includes <% tp.file.title %>
sort by priority
sort by due date 
sort by description ASC
```
---
### Transactional relationship 💸


```dataviewjs
const pages = dv.pages('"00 - Main vault/Notes/Daily Notes"').filter(p => p.<% tp.file.title %>).sort(p => p.file.name, 'asc');
let vRise = 0, minDhS = -6e9, maxDhS = 0, minDhR = 6e9, maxDhR = 0, totalS=0, totalR=0;

dv.paragraph(`**History of transactions:**<br>`);
let rows = [];
for (let p of pages) {
    let vDh = Number(String(p.<% tp.file.title %>).match(/-?\d+(\.\d+)?/)[0] || 0);
    if (vDh === 0) continue;

    let newValDh = vRise + vDh;
    let newValP = (vRise * vDh > 0) ? vDh : newValDh;
    // dv.paragraph('    NEW:'+newValDh+'   vDh:'+vDh+'    vRise:'+vRise);
    let action = "";
    let value = "";
    
    if (vDh > 0) {
        if (newValDh > 0) {
            action = `💰 <strong>I won</strong>`;
            value = newValP.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + " Dh";
            if (newValDh > maxDhR) maxDhR = newValDh;
            if (newValDh < minDhR) minDhR = newValDh;
            totalR += newValDh;
        } else {
            action = `💰 <strong>I received back</strong>`;
            value = vDh.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + " Dh";
        }
    } else {
        if (newValDh < 0) {
            action = `💸 <strong>I spent</strong>`;
            value = newValP.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + " Dh";
            if (newValDh < maxDhS) maxDhS = newValDh;
            if (newValDh > minDhS) minDhS = newValDh;
            totalS += newValDh;
        } else {
            action = `💸 <strong>I paied back</strong>`;
            value = vDh.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + " Dh";
        }
    }

    rows.push([
        `[[${p.file.name}]]`,
        action,
        value
    ]);

    vRise += vDh;
}


// Final display
dv.table(["Transaction date", "Transaction type : 💰 / 💸", "Value"], rows);

if(minDhR === 6e9){minDhR = 0;}
if(minDhS === -6e9){minDhS = 0;}

// --- TOTAL SUMMARY ---
dv.paragraph(`<h4><strong>🏦 Total Summary:</strong></h4>`);
dv.paragraph(`
  <ul>
    <li>💰💸 <strong>Profiting money</strong>
      <ul>
        <li><strong>Total:</strong> ${Math.abs(totalR).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })} Dh</li>
        <li><strong>Minimum:</strong> <i>${Math.abs(minDhR).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}</i> Dh</li>
        <li><strong>Maximum:</strong> <i>${Math.abs(maxDhR).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}</i> Dh</li>
      </ul>
    </li>
    <li>💸💰 <strong>Spending money</strong>
      <ul>
        <li><strong>Total:</strong> ${Math.abs(totalS).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })} Dh</li>
        <li><strong>Minimum:</strong> <i>${Math.abs(minDhS).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}</i> Dh</li>
        <li><strong>Maximum:</strong> <i>${Math.abs(maxDhS).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}</i> Dh</li>
      </ul>
    </li>
    <li>👛 <strong>Current expenses </strong>
      <ul>
        ${
          vRise > 0
            ? `<li><strong>Status:</strong> Winning <i>${vRise.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}</i> Dh</li>`
            : vRise < 0
              ? `<li><strong>Status:</strong> Spending <i>${Math.abs(vRise).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}</i> Dh</li>`
              : `<li><strong>Status:</strong> No pending transactions</li>`
        }
      </ul>
    </li>
  </ul>
`);
```
