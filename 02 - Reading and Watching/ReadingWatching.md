---
excalidraw-plugin: parsed
tags:
  - excalidraw
cssclasses:
  - daily
  - reflection
Owner(s):
  - "[[OwnerFirstName OwnerLastName|Dr. Anas BERKA]]"
---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠== You can decompress Drawing data with the command palette: 'Decompress current Excalidraw file'. For more info check in plugin settings under 'Saving'

# My Library 
- [ ] 💁‍♂️ I need to update my lib asap 🔼 ⏳ 2026-02-07 📅 2026-04-30

 
Most of the arts starts as ideas, published as [[Web Novels]] promoted to [[Light Novels]] (or a [[Books|book]])then either [[Manga]] or [[Manhwa]] would be serialized and finally an [[Anime]] adaptation or a [[Movie]].
### 📓 Items I’m enjoying
```dataviewjs
/********************************************************************
 * AUTO TABLES + WISHLIST — curated headlines for known folders
 *******************************************************************/

// --- CONFIG ---
const ROOT = dv.current().file.folder;
const DAILY_NOTES = "00 - Main vault/Notes/Daily Notes";
const IGNORE = new Set(["Zotero Notes"]);
const SPECIAL_QURAN_NAME = "_Quran Kareem";
const RESERVED = new Set(["Anime", "Books", "Light Novels", "Manga", "Manhwa", "Movie", "Web Novels"].map(s => s.toLowerCase()));// notes to hide completely

// Curated headlines for folders you showed in the screenshot
const HEADLINE = {
  [SPECIAL_QURAN_NAME]: "🕋 Quran Kareem — Reading",
  "Animes": "🍥 Anime — Watching Log",
  "Books": "📚 Books — Reading Log",
  "Light Novels": "📓✨ Light Novels — Reading Log",
  "Manga": "🗯️ Manga — Reading Log",
  "Manhwa": "🗯️ Manhwa — Reading Log",
  "Movies": "🎬🍿 Films — Watching Log",
  "Web Novels": "🌐📖 Web Novels — Reading Log"
};

// Abbreviations per folder (used to compose variable keys)
const ABBR = {
  [SPECIAL_QURAN_NAME]: "Quran",
  "Books": "BK",
  "Light Novels": "LN",
  "Web Novels": "WN",
  "Animes": "AN",
  "Manga": "MG",
  "Manhwa": "MH",
  "Movies": "MV"
};

// --- HELPERS ---
// strip any trailing parenthetical qualifiers, e.g., "Note (2024) (DC)" → "Note"
const stripParenSuffix = s => s.replace(/\s*(\([^()]*\)\s*)+$/, '');

const toCamel = s =>
  stripParenSuffix(s)                  // ⟵ NEW: ignore "(…)" at end
    .replace(/\.[^/.]+$/, "")
    .split(/[^A-Za-z0-9]+/g).filter(Boolean)
    .map(w => w.charAt(0).toUpperCase() + w.slice(1))
    .join("");

const isReservedTitle = (title) => {
  const base = stripParenSuffix(title); // ⟵ NEW: evaluate reservedness on stripped title
  const low = base.toLowerCase();
  const camelLow = toCamel(base).toLowerCase();
  return RESERVED.has(low) || RESERVED.has(camelLow);
};

const abbrev = name =>
  ABBR[name] ?? name.replace(/^_+/, "")
                    .split(/\s+/).filter(Boolean)
                    .map(w => w[0]).join("").toUpperCase();


// immediate child folders
const rootFolder = app.vault.getAbstractFileByPath(ROOT);
const childFolders = (rootFolder?.children ?? [])
  .filter(x => "children" in x)
  .filter(f => !IGNORE.has(f.name));

// daily notes (newest first)
const daily = dv.pages(`"${DAILY_NOTES}"`).sort(p => p.file.name, 'desc');

// wishlist accumulator
const wishlist = [];
const pushWishlist = (item, folder, note) => wishlist.push({ item, folder, note });

// per-folder rendering
for (const sf of childFolders) {
  const sfName = sf.name;
  const sfAbbr = abbrev(sfName);

  let vars = [];
  let rrMap = {};
  let origin = {};

  if (sfName === SPECIAL_QURAN_NAME) {
    vars = ["Quran/7izb", "Quran/7izbO", "Quran/7izbE"];
    rrMap = Object.fromEntries(vars.map(v => [v, v==="Quran/7izb" ? 1 : 0]));
    //in this u better search for when reading attended 60 how many times
    origin = Object.fromEntries(vars.map(v => [v, { folder: sfName, note: "(fixed)", reserved: false }]));
  } else {
    const files = sf.children
      .filter(x => "extension" in x && x.extension === "md")
      .filter(f => !isReservedTitle(f.name.replace(/\.md$/i, "")));

    for (const f of files) {
      const title = f.name.replace(/\.md$/i, "");
      const camel = toCamel(title);          // "Movie Title (2024)" → "MovieTitle"
      const key = `${sfAbbr}/${camel}`;
      vars.push(key);
      const meta = dv.page(f.path);
      rrMap[key] = (meta?.reRead ?? meta?.reread ?? 0) || 0;
      origin[key] = { folder: sfName, note: title, reserved: false };
    }
    vars.sort((a, b) => a.localeCompare(b));
  }

  // scan daily notes
  const results = Object.fromEntries(vars.map(v => [v, null]));
  outer:
  for (const p of daily) {
    for (const v of vars) {
      if (results[v] === null) {
        const val = p[v];
        if (val !== null && val !== undefined && val !== 0 && val !== "0") {
          results[v] = { value: val, date: p.file.link };
        }
      }
    }
    if (Object.values(results).every(x => x !== null)) break outer;
  }

  // visible rows; missing -> wishlist (unless reserved)
  const rows = [];
  for (const v of vars) {
    const r = results[v];
    if (r) {
      rows.push([v, r.value, r.date, rrMap[v] ?? 0]);
    } else {
      const o = origin[v] ?? { folder: sfName, note: "(unknown)", reserved: false };
      if (!o.reserved) pushWishlist(v, o.folder, o.note);
    }
  }

  // curated headline
  const headline = HEADLINE[sfName] ?? `${sfName} — Reading/Watching Log`;
  dv.header(4, headline);
  dv.table(["Items", "Last Value", "Date Found", "Complete reread"], rows);
  dv.el("hr", "");
}

// --- Wishlist ---
if (wishlist.length) {
  const uniq = Array.from(new Map(wishlist.map(w => [`${w.item}@@${w.folder}`, w])).values())
                    .sort((a, b) => a.folder.localeCompare(b.folder) || a.item.localeCompare(b.item));
  dv.header(3, "🧺 Wishlist 🧺");
  dv.table(
    ["Item", "Folder", "Source note"],
    uniq.map(w => [w.item, w.folder, `[[${w.note}]]`]) // ← simple wikilink
  );
}

```

# Excalidraw Data

## Text Elements
## Embedded Files
e30b38b5d74e3f5d93b41b6759a640af7f877f2c: [[animes_wp.jpg]]

%%
## Drawing
```compressed-json
N4KAkARALgngDgUwgLgAQQQDwMYEMA2AlgCYBOuA7hADTgQBuCpAzoQPYB2KqATLZMzYBXUtiRoIACyhQ4zZAHoFAc0JRJQgEYA6bGwC2CgF7N6hbEcK4OCtptbErHALRY8RMpWdx8Q1TdIEfARcZgRmBShcZQUebR44gAYaOiCEfQQOKGZuAG1wMFAwYogSbggOAAUARgB2AGF6gBEARRTiyFhEcsJ9aKR+EsxuZwBmAE4AVm1JnlHagA5EhYTa

yYnByBgRyerE7XHl0bmeBdrxgDZRs82IChJ1bgAWcbjz8fGz855LhYXbyQIQjKaTcHiLbSJSaJGGjKF1SaLW7WZTBbiJW7MKCkNgAawQ9TY+DYpHK2OszDguECWXaJU0uGwuOUOKEHGIhOJpIk5I4lOpmSgdMgADNCPh8ABlWBoiSSRkaQLCiBYnH4gDqD0k3GqmOxeIQ0pgsvQgg8ytZII44RyaF1BUgbCp2DU2ztMNurPZ1uYttQHCEEsxCAQx

G4s1GT3+DoYTFYnG4owut0YLHYHAAcpwxDrEuN5gt5tdbkI4MRcFBQzrajXXoknhMnh6Y4RmE00pWw2gRQQwrcWcI4ABJYh+3IAXVummE7IAosEMlkx5OY0QOLjuAGg6u2Eyq93ewhbiLyBkR5vA/gAaEACpYKAAGUI6+4PfwfZjYuC54kCDhmmuTRJmIWonj/EVgPzTQnmqTQLjWcZcAuJtcBFWoRS+EUeGwZVmHccRUHyDowHtYjqgdFcOggbA

cTgbgiio4Y0B4J4ZlqC483maEYUSa4+AdLZE0hWoeESWpeOqHhuPBUZNkge5iEeNAC1Y8SJkSC4WI+KZajkqQgRBIVmOqUZpieFjEjmBtQI+XSBIqCsRAITVFO1ZSFibPSOEc8h8AACQM0FjI4h0AF9bmfYgsHKXBkj1Ry/QgRB2WfZQIAKULwEoiBcDgOBpQrAiGOgQEMnKctSA3QYGEIBAKAAIUZZkvQ5IkSXKABiEVup6ulqJEGkoCHSt9GlN

UCTa7l0A66oEFm2a+uwAbBWG9JGqZAc2VarkyXIPkqUGxblqyVb9AAMXFKUZQIlUiTKaqltIQbTrGg0XKU3gHuOoaRte/EjRNW7zS+p6VpGgAlYQrRtHUQeekaAHlnVdXMMQKfrQZOkazs4KAztwfRxTdVBJjhsH0hxrJJUIIwCNEsmsfSO9MCgABBIhlC4CRghFIUGZ+9ICtINmnrYChAVwLt/UvfnTtndlWdF8WQilnKlaOzGBf0RWcQoG94Bu

lqNfhinTwQSGTS3K90bwnEJQADWeKF4i4+CJIsqTqttol8AATXDSYFm0KNRkjXZJiuOpqqMNgDHomN6AIIQ6e0WouNeDLZYhmdiB9RKjeqlkSGp2mwTRkoi+IaUEDotBSfRyuAFk2Ci+XcE0YIpbfD8K9IEhOXatAGMgeqiVV0hlAZAAKHgo94OfZ901B9kmABKZVwYQZRA2pcoJ+nuYMV4OFqGPo+V/XzP0cewa/oQJGoHTP0reqk8CfNzIor7j

g0qHmNMnbp3bg2Jk63GwEQWuqAQFHhjN5MqaBoG3GEFANcBFEExj6JVJgGZ37ANIKAjB1J8SkDbh3fcUD8EICviUOwAArBA2BsiSm8nAZurdvJkK7oeaqjJH6MBvLHfA8cqJdBumEYIjD0zKiWliAw+tuhoBfjuPcXD3wwKoieAwko0iSITAeNRtx8ChDZpI/hgiLwSmoZARwzBAETSyPeRumQhCvm4ejTQkVUqVECCKJgmQcy/g4UA6qrZ6qeJ/

qQoBCDKEhOYI3EgcA2DPigMw3KcBUqRPIeg+kbBMDaIkY/TgbCbp6CyLgZ86UwDhToF+cI9FMqhSAA==
```
%%