---

database-plugin: basic

---

```yaml:dbfolder
name: Research DB
description: Research DB of citations and stuffs
columns:
  __file__:
    key: __file__
    id: __file__
    input: markdown
    label: File
    accessorKey: __file__
    isMetadata: true
    skipPersist: false
    isDragDisabled: false
    csvCandidate: true
    position: 1
    isHidden: false
    sortIndex: 1
    isSorted: true
    isSortedDesc: true
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/Citations:
    input: number
    accessorKey: AB/Citations
    key: AB/Citations
    id: AB/Citations
    label: AB/Citations
    position: 2
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/CiteScore:
    input: number
    accessorKey: AB/CiteScore
    key: AB/CiteScore
    id: AB/CiteScore
    label: AB/CiteScore
    position: 3
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/CoAScore:
    input: number
    accessorKey: AB/CoAScore
    key: AB/CoAScore
    id: AB/CoAScore
    label: AB/CoAScore
    position: 4
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/CPPGScore:
    input: number
    accessorKey: AB/CPPGScore
    key: AB/CPPGScore
    id: AB/CPPGScore
    label: AB/CPPGScore
    position: 5
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/CPPRScore:
    input: number
    accessorKey: AB/CPPRScore
    key: AB/CPPRScore
    id: AB/CPPRScore
    label: AB/CPPRScore
    position: 6
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/CPPScore:
    input: number
    accessorKey: AB/CPPScore
    key: AB/CPPScore
    id: AB/CPPScore
    label: AB/CPPScore
    position: 7
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/GCitations:
    input: number
    accessorKey: AB/GCitations
    key: AB/GCitations
    id: AB/GCitations
    label: AB/GCitations
    position: 29
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/GCiteScore:
    input: number
    accessorKey: AB/GCiteScore
    key: AB/GCiteScore
    id: AB/GCiteScore
    label: AB/GCiteScore
    position: 8
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/gGIndex:
    input: number
    accessorKey: AB/gGIndex
    key: AB/gGIndex
    id: AB/gGIndex
    label: AB/gGIndex
    position: 9
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/gGScore:
    input: number
    accessorKey: AB/gGScore
    key: AB/gGScore
    id: AB/gGScore
    label: AB/gGScore
    position: 10
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/gIndex:
    input: number
    accessorKey: AB/gIndex
    key: AB/gIndex
    id: AB/gIndex
    label: AB/gIndex
    position: 11
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/gRIndex:
    input: number
    accessorKey: AB/gRIndex
    key: AB/gRIndex
    id: AB/gRIndex
    label: AB/gRIndex
    position: 12
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/gRScore:
    input: number
    accessorKey: AB/gRScore
    key: AB/gRScore
    id: AB/gRScore
    label: AB/gRScore
    position: 13
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/gScore:
    input: number
    accessorKey: AB/gScore
    key: AB/gScore
    id: AB/gScore
    label: AB/gScore
    position: 14
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/hGIndex:
    input: number
    accessorKey: AB/hGIndex
    key: AB/hGIndex
    id: AB/hGIndex
    label: AB/hGIndex
    position: 15
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/hGScore:
    input: number
    accessorKey: AB/hGScore
    key: AB/hGScore
    id: AB/hGScore
    label: AB/hGScore
    position: 16
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/hIndex:
    input: number
    accessorKey: AB/hIndex
    key: AB/hIndex
    id: AB/hIndex
    label: AB/hIndex
    position: 17
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/hRIndex:
    input: number
    accessorKey: AB/hRIndex
    key: AB/hRIndex
    id: AB/hRIndex
    label: AB/hRIndex
    position: 18
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/hRScore:
    input: number
    accessorKey: AB/hRScore
    key: AB/hRScore
    id: AB/hRScore
    label: AB/hRScore
    position: 19
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/hScore:
    input: number
    accessorKey: AB/hScore
    key: AB/hScore
    id: AB/hScore
    label: AB/hScore
    position: 20
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/i10GIndex:
    input: number
    accessorKey: AB/i10GIndex
    key: AB/i10GIndex
    id: AB/i10GIndex
    label: AB/i10GIndex
    position: 21
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/i10Index:
    input: number
    accessorKey: AB/i10Index
    key: AB/i10Index
    id: AB/i10Index
    label: AB/i10Index
    position: 22
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/i10RIndex:
    input: number
    accessorKey: AB/i10RIndex
    key: AB/i10RIndex
    id: AB/i10RIndex
    label: AB/i10RIndex
    position: 23
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/OScore:
    input: number
    accessorKey: AB/OScore
    key: AB/OScore
    id: AB/OScore
    label: AB/OScore
    position: 24
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/PapersP:
    input: number
    accessorKey: AB/PapersP
    key: AB/PapersP
    id: AB/PapersP
    label: AB/PapersP
    position: 25
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/PapersS:
    input: number
    accessorKey: AB/PapersS
    key: AB/PapersS
    id: AB/PapersS
    label: AB/PapersS
    position: 26
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/RCiteScore:
    input: number
    accessorKey: AB/RCiteScore
    key: AB/RCiteScore
    id: AB/RCiteScore
    label: AB/RCiteScore
    position: 27
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/RCitations:
    input: number
    accessorKey: AB/RCitations
    key: AB/RCitations
    id: AB/RCitations
    label: AB/RCitations
    position: 31
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/PScore:
    input: number
    accessorKey: AB/PScore
    key: AB/PScore
    id: AB/PScore
    label: AB/PScore
    position: 28
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  fillData:
    input: checkbox
    accessorKey: fillData
    key: fillData
    id: fillData
    label: fillData
    position: 33
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/CitationsGY:
    input: number
    accessorKey: AB/CitationsGY
    key: AB/CitationsGY
    id: AB/CitationsGY
    label: AB/CitationsGY
    position: 30
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  AB/CitationsRY:
    input: number
    accessorKey: AB/CitationsRY
    key: AB/CitationsRY
    id: AB/CitationsRY
    label: AB/CitationsRY
    position: 32
    skipPersist: false
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
config:
  remove_field_when_delete_column: true
  cell_size: compact
  sticky_first_column: true
  group_folder_column: 
  remove_empty_folders: false
  automatically_group_files: false
  hoist_files_with_empty_attributes: true
  show_metadata_created: false
  show_metadata_modified: false
  show_metadata_tasks: false
  show_metadata_inlinks: false
  show_metadata_outlinks: false
  show_metadata_tags: false
  source_data: current_folder
  source_form_result: 
  source_destination_path: /
  row_templates_folder: 00 - Main vault/Templates
  current_row_template: 
  pagination_size: 30
  font_size: 16
  enable_js_formulas: false
  formula_folder_path: /
  inline_default: true
  inline_new_position: last_field
  date_format: yyyy-MM-dd
  datetime_format: "yyyy-MM-dd HH:mm:ss"
  metadata_date_format: "yyyy-MM-dd HH:mm:ss"
  enable_footer: false
  implementation: default
filters:
  enabled: false
  conditions:
```