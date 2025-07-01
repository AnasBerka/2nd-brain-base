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
Creation date: 
Last modification: {{now_str}}
banner: "[[FriendsBanner.jpg]]"
banner_x: 0
banner_y: 0.546
cssclasses:
  - daily
  - sNote
---

# {{full_name}}
## contact

> _Imported from Google Contacts_
***
### Important events
#### Birthday on {{bday}}

- [ ] 🍰 [[{{full_name}}]]’s #BDay let’s party !! ⏬ 🔁 every year ⏳ {{bdayday}}

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
tags do not include #BDay
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
---
### Transactional relationship 💸


```dataviewjs
const pages = dv.pages('"00 - Main vault/Notes/Daily Notes"').filter(p => p.{{vname}}).sort(p => p.file.name, 'asc');
let vRise = 0, minDhS = -6e9, maxDhS = 0, minDhR = 6e9, maxDhR = 0, totalS=0, totalR=0;
// Display totals in the note
dv.paragraph(`**History of transactions:**<br>`);
for (let p of pages) {
    let vDh = Number(String(p.{{vname}}).match(/-?\d+(\.\d+)?/)[0]|| 0);
    if (vDh === 0) {continue;}
    vRise += vDh;
    if (vDh>0){dv.paragraph('💰 I recieved **'+vDh+'** Dh on [['+p.file.name+']] <br>');
    if(vDh>maxDhR){maxDhR=vDh;}
    if(vDh<minDhR){minDhR=vDh;}
    totalR+=vDh;
    }
else{dv.paragraph('💸 I sent **'+vDh+'** Dh on [['+p.file.name+']] <br>');
	if(vDh<maxDhS){maxDhS=vDh;}
    if(vDh>minDhS){minDhS=vDh;}
    totalS+=vDh;
}
}
if(minDhR === 6e9){minDhR = 0;}
if(minDhS === -6e9){minDhS = 0;}

// Display totals in the note
dv.paragraph(`<br><br>**Total:**<br>`);
if (vRise>=0){dv.paragraph(`<li> 💰 I am borrowing <b><i>${vRise}</i></b> Dh</li>`);}
else{dv.paragraph(`<li> 💸 I am lending <b><i>${vRise}</i></b> Dh</li>`);}
dv.paragraph(`<li> 💸💰 Lending money (Total of ${totalS} Dh):&nbsp;&nbsp;&nbsp;&nbsp; minimum <b><i>${minDhS}</i></b> Dh & maximum <b><i>${maxDhS}</i></b> Dh</li>`);
dv.paragraph(`<li> 💰💸 Borrowing money (Total of ${totalR} Dh):&nbsp;&nbsp;&nbsp;&nbsp; minimum <b><i>${minDhR}</i></b> Dh & maximum <b><i>${maxDhR}</i></b> Dh</li>`);
```
