---
tags: 
  - newIdea
Creation date: 2026-01-18 17:11
banner: "[[DeathNoteBanner.jpg]]"
banner_x: 0
banner_y: 0.906
cssclasses:
  - daily
  - sNote
---
# 🎓 Research Index:

## Our publications:
Papers:
- [@berka_CactiViTImagebasedSmartphone_2023] 
- [@berka_EnhancingDeepLabV3Aerial_2024] 
- [@berka_EnhancingDeepLabV3Fuse_2025]  
- [@elhajji_ArchitectureIntelligentTutoring_2025] 

Thesis:
-  [@berka_SmartFarmingSysteme_2024] 

## Citation metrics
```dataviewjs
/******************************************************************
 * CONFIGURATION
 ******************************************************************/
const ROOT      = '"00 - Main vault/Notes/Daily Notes"';
const METRICS = {
    "AB/CitationsGY": "G-Scholar Citation",
    "AB/CitationsRY": "On Reaserch-Gate",
    "AB/CitationsSY": "On Scopus",
    "AB/CitationsWY": "On Web Of Sciences",
};

/******************************************************************
 * HELPERS
 ******************************************************************/
const yearOf = p => {
    const m = p.file.name.match(/^(\d{4})-\d{2}-\d{2}$/);
    return m ? Number(m[1]) : null;
};

const val = (p, k) =>
    typeof p[k] === "number" ? p[k] : 0;

/******************************************************************
 * DATA COLLECTION
 ******************************************************************/
const pages = dv.pages(ROOT)
    .where(p => yearOf(p) !== null);

const allYears = [...new Set(pages.map(p => yearOf(p)))].sort();

/******************************************************************
 * AGGREGATION
 ******************************************************************/
const sums = {};
for (const k of Object.keys(METRICS)) {
    sums[k] = Object.fromEntries(allYears.map(y => [y, 0]));
}

for (const p of pages) {
    const y = yearOf(p);
    for (const k of Object.keys(METRICS)) {
        sums[k][y] += val(p, k);
    }
}

/******************************************************************
 * FILTER EMPTY YEARS
 ******************************************************************/
const years = allYears.filter(y =>
    Object.keys(METRICS)
        .reduce((acc, k) => acc + sums[k][y], 0) !== 0
);

/******************************************************************
 * RENDER
 ******************************************************************/
dv.table(
    ["Metric", ...years.map(String), "Total"],
    Object.entries(METRICS).map(([k, label]) => {
        const row = years.map(y => sums[k][y]);
        const total = row.reduce((a, b) => a + b, 0);

        return [
            label,
            ...row.map(v => v===0 ? "":
                v.toLocaleString("fr-FR", {
                    minimumFractionDigits: 0,
                    maximumFractionDigits: 0
                })
            ),
            total.toLocaleString("fr-FR", {
                minimumFractionDigits: 0,
                maximumFractionDigits: 0
            })
        ];
    })
);
```
## Detailed information 
```dataviewjs
/******************************************************************
 * CONFIGURATION
 ******************************************************************/
const ROOT = '"00 - Main vault/Notes/Daily Notes"';

const METRICS = {
    "@berka_CactiViTImagebasedSmartphone_2023|CactiVit": {
        "AB/CactiVit/GS": "G-Scholar",
        "AB/CactiVit/RG": "ReaserchGate",
        "AB/CactiVit/S": "Scopus",
        "AB/CactiVit/WOF": "WOS"
    },
    "@berka_EnhancingDeepLabV3Aerial_2024|EDLV3": {
        "AB/EDLV3/GS": "G-Scholar",
        "AB/EDLV3/RG": "ReaserchGate",
        "AB/EDLV3/S": "Scopus",
        "AB/EDLV3/WOF": "WOS"
    },
    "@berka_SmartFarmingSysteme_2024|My thesis": {
        "AB/myThesis/GS": "G-Scholar",
        "AB/myThesis/RG": "ReaserchGate",
        "AB/myThesis/S": "Scopus",
        "AB/myThesis/WOF": "WOS"
    },
    "@berka_EnhancingDeepLabV3Fuse_2025|DIFD": {
        "AB/DIFD/GS": "G-Scholar",
        "AB/DIFD/RG": "ReaserchGate",
        "AB/DIFD/S": "Scopus",
        "AB/DIFD/WOF": "WOS"
    },
    "@elhajji_ArchitectureIntelligentTutoring_2025|AITVR": {
        "AB/AITVR/GS": "G-Scholar",
        "AB/AITVR/RG": "ReaserchGate",
        "AB/AITVR/S": "Scopus",
        "AB/AITVR/WOF": "WOS"
    }
};

/******************************************************************
 * HELPERS
 ******************************************************************/
const yearOf = p => {
    const m = p.file.name.match(/^(\d{4})-\d{2}-\d{2}$/);
    return m ? Number(m[1]) : null;
};

const val = (p, k) =>
    typeof p[k] === "number" ? p[k] : 0;

const fmt = v => v === 0 ? "" :
    v.toLocaleString("fr-FR", { minimumFractionDigits: 0, maximumFractionDigits: 0 });

/******************************************************************
 * DATA COLLECTION
 ******************************************************************/
const pages = dv.pages(ROOT).where(p => yearOf(p) !== null);
const allYears = [...new Set(pages.map(p => yearOf(p)))].sort();

/******************************************************************
 * AGGREGATION
 ******************************************************************/
const sums = {};
for (const g of Object.values(METRICS)) {
    for (const k of Object.keys(g)) {
        sums[k] = Object.fromEntries(allYears.map(y => [y, 0]));
    }
}

for (const p of pages) {
    const y = yearOf(p);
    for (const g of Object.values(METRICS)) {
        for (const k of Object.keys(g)) {
            sums[k][y] += val(p, k);
        }
    }
}

/******************************************************************
 * FILTER EMPTY YEARS (column-level)
 ******************************************************************/
const years = allYears.filter(y =>
    Object.keys(sums).reduce((acc, k) => acc + sums[k][y], 0) !== 0
);

/******************************************************************
 * BUILD TABLE ROWS
 ******************************************************************/
let tableRows = [];

// Keep track of total sums for the final "Total" group
let metricTotals = {}; // key = metric label, value = array of yearly sums

Object.entries(METRICS).forEach(([group, metrics]) => {
    Object.entries(metrics).forEach(([k, label], idx) => {
        const rowValues = years.map(y => sums[k][y]);
        const total = rowValues.reduce((a, b) => a + b, 0);

        // accumulate for final total
        if (!metricTotals[label]) metricTotals[label] = rowValues.map(v => v);
        else rowValues.forEach((v, i) => metricTotals[label][i] += v);

        tableRows.push([
            idx === 0 ? `[[${group}]]` : "",  // wikilink only on first row of group
            label,
            ...rowValues.map(v => v === 0 ? "" : fmt(v)),
            fmt(total)
        ]);
    });
});

// Build main table without totals
dv.table(
    ["Work", "Indexation", ...years.map(String), "Total"],
    tableRows
);
dv.paragraph(`<h4> </h4>`);
// Build totals table separately
let totalRows = [];
Object.entries(metricTotals).forEach(([label, rowValues], idx) => {
    const total = rowValues.reduce((a, b) => a + b, 0);
    totalRows.push([
        idx === 0 ? "All works" : "",
        label,
        ...rowValues.map(v => v === 0 ? "" : fmt(v)),
        fmt(total)
    ]);
});

dv.table(
    ["Total", "Indexation", ...years.map(String), "Total"],
    totalRows
);

```
## Growth in research 
```tracker
searchType: dvField
searchTarget: AB/hGIndex, AB/hRIndex, AB/gGIndex, AB/gRIndex, AB/i10GIndex, AB/i10RIndex
datasetName: hGIndex,hRIndex,gGIndex,gRIndex,i10GIndex,i10RIndex
startDate: 2023-07-13
accum: false
fitPanelWidth: true
aspectRatio: 20:9
line:
    title: Main index
    yAxisLabel: Google Scholar, Researchgate  
    showPoint: false
    yAxisLocation: left, right, left, right, left, right
    yAxisColor: '#E69F00, #56B4E9' 
    yAxisLabelColor: '#E69F00, #56B4E9' 
    lineColor: '#E69F00, #56B4E9, #F0E442, #009E73, #D55E00, #0072B2'
    showLegend: true
    yMin: 0, 0
    fillGap: true
```
```tracker
searchType: dvField
searchTarget: AB/PapersS, AB/PapersP, AB/PScore
datasetName: Submitted, Published, PScore
startDate: 2023-07-13
accum: false
fitPanelWidth: true
aspectRatio: 20:9
line:
    title: Publications
    yAxisLabel: Score, Papers count   
    showPoint: false
    yAxisLocation: right,right,left 
    yAxisColor: '#009E73, #56B4E9' 
    yAxisLabelColor: '#009E73, #56B4E9' 
    lineColor: '#E69F00, #56B4E9, #009E73'
    showLegend: true
    yMin: 0, 0
    fillGap: true
```
```tracker
searchType: dvField
searchTarget: AB/CPPGScore, AB/CPPRScore, AB/GCiteScore, AB/RCiteScore
datasetName: CPPGScore,CPPRScore,GCiteScore,RCiteScore
startDate: 2023-07-13
accum: false
fitPanelWidth: true
aspectRatio: 20:9
line:
    title: Citation index
    yAxisLabel: Google Scholar, Researchgate  
    showPoint: false
    yAxisLocation: left, right, left, right
    yAxisColor: '#E69F00, #56B4E9' 
    yAxisLabelColor: '#E69F00, #56B4E9' 
    lineColor: '#E69F00, #56B4E9, #F0E442, #009E73'
    showLegend: true
    yMin: 0, 0
    fillGap: true
```
```tracker
searchType: dvField
searchTarget: AB/hGScore, AB/hRScore, AB/gGScore, AB/gRScore
datasetName: hGScore,hRScore,gGScore,gRScore
startDate: 2023-07-13
accum: false
fitPanelWidth: true
aspectRatio: 20:9
line:
    title: My preferred index
    yAxisLabel: Google Scholar, Researchgate  
    showPoint: false
    yAxisLocation: left, right, left, right
    yAxisColor: '#E69F00, #56B4E9' 
    yAxisLabelColor: '#E69F00, #56B4E9' 
    lineColor: '#E69F00, #56B4E9, #F0E442, #009E73'
    showLegend: true
    yMin: 0, 0
    fillGap: true
```
```tracker
searchType: dvField
searchTarget: AB/GCitations, AB/RCitations
datasetName: Citations GS,Citations R
startDate: 2023-07-13
accum: false
fitPanelWidth: true
aspectRatio: 20:9
line:
    title: Citations growth 
    yAxisLabel: Google Scholar, Researchgate  
    showPoint: false
    yAxisLocation: left, right
    yAxisColor: '#E69F00, #56B4E9' 
    yAxisLabelColor: '#E69F00, #56B4E9' 
    lineColor: '#E69F00, #56B4E9'
    showLegend: true
    yMin: 0, 0
    fillGap: true
```
