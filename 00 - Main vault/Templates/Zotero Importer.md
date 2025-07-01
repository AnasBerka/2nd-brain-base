---
tags:
- Reading/{{itemType}}/{% if publicationTitle %}{{publicationTitle | replace(' ', '-')}}{% elif repository %}{{ repository | replace(' ', '-')}}{% elif publisher %}{{ publisher }}{% else %}Unknown{% endif %}
{% for tag in tags %} 
- Reading/Tags/{{ tag.tag | replace(' ', '-') }}
{% endfor %}
- "{{date | format("YYYY")}}"
authors: 
{% for author in authors.split(',') %}
- "[[{{ author | trim }}]]"
{% endfor %}
year: {{date | format("YYYY")}}
publisher: 
{% if publicationTitle %}
publisher: "[[{{publicationTitle}}]]"
{% elif repository %}
publisher: "[[{{ repository }}]]"
{% elif publisher %}
publisher: "[[{{ publisher }}]]"
{% else %}
publisher: Unknown
{% endif %}
itemType : {{itemType}}
citekey: {{citekey}}
keywords: [{{allTags}}]
cssclasses:
  - daily
  - sNote
banner: "[[CircuitBanner.jpg]]"
banner_x: 0
banner_y: 0.644
isRead: false
---

# Title: {{title}}
Authors: {{authors}}
---
Zotero link: {{pdfZoteroLink}}
---

## Metadata
> [!meta]- Metadata
> abstract:: {{abstractNote}}
> year: {{date | format("YYYY")}}
> zotero_link:: {{pdfZoteroLink}}
> url:: {{url}}
> doi:: {{DOI}}
> keywords: {{allTags}}
> itemType : {{itemType}}
> Related:: {% for relation in relations -%} {%- if relation.citekey -%} [[{{relation.citekey}}]], {% endif -%} {%- endfor%}
> bibliography:: {{bibliography}}
> Keywords:: {{allTags}}

---
## Self Notes
{% persist "notes" %}


{% endpersist %}

---

## Reading notes
{% persist "annotations" %}

---

{%-
    set zoteroColors = {
        "#2ea8e5": "blue",
        "#5fb236": "green",
        "#a28ae5": "purple",
        "#ff6666": "red",
        "#ffd400": "yellow",
        "#f19837": "orange",
        "#aaaaaa": "grey",
        "#e56eee": "magenta"
    }
-%}

{%-
   set colorHeading = {
		"yellow": "🗝️ Important Quotes & Key Findings", 
		"red": "⚠️ Critical Points & Controversies", 
		"green": "📊 Evidence & Supporting Data", 
		"blue": "📘 Key Concepts & Definitions", 
		"purple": "🛠️ Methodology & Techniques", 
		"magenta": "📌 To-Do & Follow-Up",
		"orange": "💡 Personal Insights & Ideas", 
		"grey": "📂 Background Information"
   }
-%}

{%- macro calloutHeader(type) -%}
    {%- switch type -%}
        {%- case "highlight" -%}
        Highlight
        {%- case "image" -%}
        Image
        {%- default -%}
        Note
    {%- endswitch -%}
{%- endmacro %}

{%- set newAnnot = [] -%}
{%- set newAnnotations = [] -%}
{%- set annotations = annotations | filterby("date", "dateafter", lastImportDate) %}

{% if annotations.length > 0 %}
*Imported: {{importDate | format("YYYY-MM-DD HH:mm")}}*

{%- for annot in annotations -%}
    {%- if annot.color in zoteroColors -%}
        {%- set customColor = zoteroColors[annot.color] -%}
    {%- elif annot.colorCategory|lower in colorHeading -%}
    	{%- set customColor = annot.colorCategory|lower -%}
    {%- else -%}
	    {%- set customColor = "other" -%}
    {%- endif -%}
    {%- set newAnnotations = (newAnnotations.push({"annotation": annot, "customColor": customColor}), newAnnotations) -%}
{%- endfor -%}

{%- for color, heading in colorHeading -%}
{%- for entry in newAnnotations | filterby ("customColor", "startswith", color) -%}
{%- set annot = entry.annotation -%}

{%- if entry and loop.first %}
#### {{colorHeading[color]}}
{%- endif %}

> [!quote{{"|" + color if color != "other"}}]+ {{calloutHeader(annot.type)}} ([page. {{annot.pageLabel}}](zotero://open-pdf/library/items/{{annot.attachment.itemKey}}?page={{annot.pageLabel}}&annotation={{annot.id}}))

{%- if annot.annotatedText %}
> {{annot.annotatedText|nl2br}} {% if annot.hashTags %}{{annot.hashTags}}{% endif -%}
{%- endif %}

{%- if annot.imageRelativePath %}
> ![[{{annot.imageRelativePath}}]]
{%- endif %}

{%- if annot.ocrText %}
> {{annot.ocrText}}
{%- endif %}

{%- if annot.comment %}
> - **{{annot.comment}}**
{%- endif -%}

{%- endfor -%}
{%- endfor -%}

{% endif %}
{% endpersist %}