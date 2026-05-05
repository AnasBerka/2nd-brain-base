---
aliases: 
{{alias_block}}
tags:
{{tag_block}}
Phone number:
{{phone_block}}
E-mail:
{{email_block}} 
Full address:
{{address_block}}
City: 
Country:
{{country_block}}
Organization: "{{organization}}"
Title: "{{jobTitle}}"
Notes: "{{notes}}"
Birthday: "{{bday}}"
Close relations: 
Last modification: "{{now_str}}" 
banner: "[[FriendsBanner.jpg]]"
banner_x: 0
banner_y: 0.546
cssclasses:
  - daily
  - cyber
---

# {{full_name}}
## contact

> _Imported from Google Contacts_
***
### Important events
#### Birthday 
on {{bday}}.

***
### Important notes
#### 

***
### Tasks
#### In progress ⏳
```tasks
not done
description includes [[{{full_name}}
sort by priority
sort by due date 
sort by description ASC
```

#### Done ✔️
```tasks
status.type is done
tags do not include #Logging/SDay/BDay
description includes [[{{full_name}}
sort by priority
sort by due date 
sort by description ASC
```

#### Cancelled ❌
```tasks
status.type is cancelled
description includes [[{{full_name}}
sort by priority
sort by due date 
sort by description ASC
```
#### Birthdays 🍰
```tasks
done
tags include #Logging/SDay/BDay
description includes [[{{full_name}}
sort by priority
sort by due date 
sort by description ASC
```
---
### Transactional relationship 💸


```dataviewjs
const pages = dv.pages('"00 - Main vault/Notes/Daily Notes"').filter(p => p.{{vname}}).sort(p => p.file.name, 'asc');
let vRise = 0, minDhS = -6e9, maxDhS = 0, minDhR = 6e9, maxDhR = 0, totalS=0, totalR=0;

dv.paragraph(`**History of transactions:**<br>`);
let rows = [];
for (let p of pages) {
    let rawValues = Array.isArray(p.{{vname}}) ? p.{{vname}} : [p.{{vname}}];
    for (let val of rawValues) {
      let vDh = Number(String(p.{{vname}}).match(/-?\d+(\.\d+)?/)[0] || 0);
      if (vDh === 0) continue;

      let newValDh = vRise + vDh;
      // let newValP = (vRise * vDh > 0) ? vDh : newValDh;
      // dv.paragraph('    NEW:'+newValDh+'   vDh:'+vDh+'    vRise:'+vRise);
      let action = "";
      // let value = "";
      
      if (vDh > 0) {
          if (newValDh > 0) {
              action = `💰 <strong>I owe</strong>`;
              // value = newValP.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + " Dh";
              if (newValDh > maxDhR) maxDhR = newValDh;
              if (newValDh < minDhR) minDhR = newValDh;
              totalR += newValDh;
          } else {
              action = `💰 <strong>I received back</strong>`;
              // value = vDh.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + " Dh";
          }
      } else {
          if (newValDh < 0) {
              action = `💸 <strong>I lent</strong>`;
              // value = newValP.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + " Dh";
              if (newValDh < maxDhS) maxDhS = newValDh;
              if (newValDh > minDhS) minDhS = newValDh;
              totalS += newValDh;
          } else {
              action = `💸 <strong>I sent back</strong>`;
              // value = vDh.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + " Dh";
          }
      }

      vRise += vDh;
      
      rows.push([
          `[[${p.file.name}]]`,
          action,
          vDh.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + " Dh",
          vRise.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 }) + " Dh"
      ]);
    }
}


// Final display
dv.table(["Transaction date", "Transaction type : 💰 / 💸", "Value", "Accumulated"], rows);

if(minDhR === 6e9){minDhR = 0;}
if(minDhS === -6e9){minDhS = 0;}

// --- TOTAL SUMMARY ---
dv.paragraph(`<h4><strong>🏦 Total Summary:</strong></h4>`);
dv.paragraph(`
  <ul>
    <li>💰💸 <strong>Borrowing money</strong>
      <ul>
        <li><strong>Total:</strong> ${Math.abs(totalR).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })} Dh</li>
        <li><strong>Minimum:</strong> <i>${Math.abs(minDhR).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}</i> Dh</li>
        <li><strong>Maximum:</strong> <i>${Math.abs(maxDhR).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}</i> Dh</li>
      </ul>
    </li>
    <li>💸💰 <strong>Lending money</strong>
      <ul>
        <li><strong>Total:</strong> ${Math.abs(totalS).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })} Dh</li>
        <li><strong>Minimum:</strong> <i>${Math.abs(minDhS).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}</i> Dh</li>
        <li><strong>Maximum:</strong> <i>${Math.abs(maxDhS).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}</i> Dh</li>
      </ul>
    </li>
    <li>👛 <strong>Current balance</strong>
      <ul>
        ${
          vRise > 0
            ? `<li><strong>Status:</strong> Borrowing <i>${vRise.toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}</i> Dh</li>`
            : vRise < 0
              ? `<li><strong>Status:</strong> Lending <i>${Math.abs(vRise).toLocaleString("fr-FR", { minimumFractionDigits: 2, maximumFractionDigits: 2 })}</i> Dh</li>`
              : `<li><strong>Status:</strong> No pending transactions</li>`
        }
      </ul>
    </li>
  </ul>
`);
```
