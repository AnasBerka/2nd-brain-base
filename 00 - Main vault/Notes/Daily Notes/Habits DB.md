---

database-plugin: basic

---

```yaml:dbfolder
name: Habits DB
description: A data base to track my habit
columns:
  isCompleted:
    input: checkbox
    accessorKey: isCompleted
    label: isCompleted
    key: isCompleted
    id: isCompleted
    position: 2
    skipPersist: false
    isHidden: false
    sortIndex: -1
    width: 71
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: false
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  salatOnTime:
    input: number
    accessorKey: salatOnTime
    label: salatOnTime
    key: salatOnTime
    id: salatOnTime
    position: 3
    skipPersist: false
    isHidden: false
    sortIndex: -1
    width: 119
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  salatFajer:
    input: checkbox
    accessorKey: salatFajer
    label: salatFajer
    key: salatFajer
    id: salatFajer
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
  salatDohr:
    input: checkbox
    accessorKey: salatDohr
    label: salatDohr
    key: salatDohr
    id: salatDohr
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
  salatAaser:
    input: checkbox
    accessorKey: salatAaser
    label: salatAaser
    key: salatAaser
    id: salatAaser
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
  salatMeghrb:
    input: checkbox
    accessorKey: salatMeghrb
    label: salatMeghrb
    key: salatMeghrb
    id: salatMeghrb
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
  salatIshae:
    input: checkbox
    accessorKey: salatIshae
    label: salatIshae
    key: salatIshae
    id: salatIshae
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
  hWork:
    input: number
    accessorKey: hWork
    label: hWork
    key: hWork
    id: hWork
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
  oWork:
    input: number
    accessorKey: oWork
    label: oWork
    key: oWork
    id: oWork
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
  startOWorkAt:
    input: text
    accessorKey: startOWorkAt
    label: startOWorkAt
    key: startOWorkAt
    id: startOWorkAt
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
  finishOWorkAt:
    input: text
    accessorKey: finishOWorkAt
    label: finishOWorkAt
    key: finishOWorkAt
    id: finishOWorkAt
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
  rWork:
    input: number
    accessorKey: rWork
    label: rWork
    key: rWork
    id: rWork
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
  myWeight:
    input: number
    accessorKey: myWeight
    label: myWeight
    key: myWeight
    id: myWeight
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
  myHeight:
    input: number
    accessorKey: myHeight
    label: myHeight
    key: myHeight
    id: myHeight
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
  pushBarMaxKg:
    input: number
    accessorKey: pushBarMaxKg
    label: pushBarMaxKg
    key: pushBarMaxKg
    id: pushBarMaxKg
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
  pushBarMaxRep:
    input: number
    accessorKey: pushBarMaxRep
    label: pushBarMaxRep
    key: pushBarMaxRep
    id: pushBarMaxRep
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
  pullBarMaxKg:
    input: number
    accessorKey: pullBarMaxKg
    label: pullBarMaxKg
    key: pullBarMaxKg
    id: pullBarMaxKg
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
  pullBarMaxRep:
    input: number
    accessorKey: pullBarMaxRep
    label: pullBarMaxRep
    key: pullBarMaxRep
    id: pullBarMaxRep
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
  squadBarMaxKg:
    input: number
    accessorKey: squadBarMaxKg
    label: squadBarMaxKg
    key: squadBarMaxKg
    id: squadBarMaxKg
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
  squadBarMaxRep:
    input: number
    accessorKey: squadBarMaxRep
    label: squadBarMaxRep
    key: squadBarMaxRep
    id: squadBarMaxRep
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
  curlDumpMaxKg:
    input: number
    accessorKey: curlDumpMaxKg
    label: curlDumpMaxKg
    key: curlDumpMaxKg
    id: curlDumpMaxKg
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
  curlDumpMaxRep:
    input: number
    accessorKey: curlDumpMaxRep
    label: curlDumpMaxRep
    key: curlDumpMaxRep
    id: curlDumpMaxRep
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
  springMaxSpeed:
    input: number
    accessorKey: springMaxSpeed
    label: springMaxSpeed
    key: springMaxSpeed
    id: springMaxSpeed
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
  springMaxSS:
    input: number
    accessorKey: springMaxSS
    label: springMaxSS
    key: springMaxSS
    id: springMaxSS
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
  typingTraining:
    input: number
    accessorKey: typingTraining
    label: typingTraining
    key: typingTraining
    id: typingTraining
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
  typingSpeed:
    input: number
    accessorKey: typingSpeed
    label: typingSpeed
    key: typingSpeed
    id: typingSpeed
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
  gymKg:
    input: number
    accessorKey: gymKg
    label: gymKg
    key: gymKg
    id: gymKg
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
  gymMin:
    input: number
    accessorKey: gymMin
    label: gymMin
    key: gymMin
    id: gymMin
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
  pushUpReps:
    input: number
    accessorKey: pushUpReps
    label: pushUpReps
    key: pushUpReps
    id: pushUpReps
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
  setUpReps:
    input: number
    accessorKey: setUpReps
    label: setUpReps
    key: setUpReps
    id: setUpReps
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
  squadReps:
    input: number
    accessorKey: squadReps
    label: squadReps
    key: squadReps
    id: squadReps
    position: 34
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
  runingKm:
    input: number
    accessorKey: runingKm
    label: runingKm
    key: runingKm
    id: runingKm
    position: 35
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
  animeEp:
    input: number
    accessorKey: animeEp
    label: animeEp
    key: animeEp
    id: animeEp
    position: 36
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
  movieMin:
    input: number
    accessorKey: movieMin
    label: movieMin
    key: movieMin
    id: movieMin
    position: 37
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
  RManga:
    input: number
    accessorKey: RManga
    label: RManga
    key: RManga
    id: RManga
    position: 38
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
  LWRead:
    input: number
    accessorKey: LWRead
    label: LWRead
    key: LWRead
    id: LWRead
    position: 39
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
  BRead:
    input: number
    accessorKey: BRead
    label: BRead
    key: BRead
    id: BRead
    position: 40
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
  gamingPCMin:
    input: number
    accessorKey: gamingPCMin
    label: gamingPCMin
    key: gamingPCMin
    id: gamingPCMin
    position: 41
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
  gamingMobileMin:
    input: number
    accessorKey: gamingMobileMin
    label: gamingMobileMin
    key: gamingMobileMin
    id: gamingMobileMin
    position: 42
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
  smMin:
    input: number
    accessorKey: smMin
    label: smMin
    key: smMin
    id: smMin
    position: 43
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
  moneyInDh:
    input: number
    accessorKey: moneyInDh
    label: moneyInDh
    key: moneyInDh
    id: moneyInDh
    position: 44
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
  meTime:
    input: number
    accessorKey: meTime
    label: meTime
    key: meTime
    id: meTime
    position: 46
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
  gTime:
    input: checkbox
    accessorKey: gTime
    label: gTime
    key: gTime
    id: gTime
    position: 47
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
  bTime:
    input: number
    accessorKey: bTime
    label: bTime
    key: bTime
    id: bTime
    position: 48
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
  sleptAt:
    input: text
    accessorKey: sleptAt
    label: sleptAt
    key: sleptAt
    id: sleptAt
    position: 49
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
  wokedAt:
    input: text
    accessorKey: wokedAt
    label: wokedAt
    key: wokedAt
    id: wokedAt
    position: 50
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
  runingMin:
    input: number
    accessorKey: runingMin
    label: runingMin
    key: runingMin
    id: runingMin
    position: 51
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
  runingAS:
    input: number
    accessorKey: runingAS
    label: runingAS
    key: runingAS
    id: runingAS
    position: 52
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
  LWReadMin:
    input: number
    accessorKey: LWReadMin
    label: LWReadMin
    key: LWReadMin
    id: LWReadMin
    position: 53
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
  Fb:
    input: number
    accessorKey: Fb
    label: Fb
    key: Fb
    id: Fb
    position: 54
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
  Insta:
    input: number
    accessorKey: Insta
    label: Insta
    key: Insta
    id: Insta
    position: 55
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
  UnlockNbr:
    input: number
    accessorKey: UnlockNbr
    label: UnlockNbr
    key: UnlockNbr
    id: UnlockNbr
    position: 56
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
  ScreenTime:
    input: number
    accessorKey: ScreenTime
    label: ScreenTime
    key: ScreenTime
    id: ScreenTime
    position: 57
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
  tags:
    input: text
    accessorKey: tags
    label: tags
    key: tags
    id: tags
    position: 62
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
  quran-7izb:
    input: number
    accessorKey: quran-7izb
    label: quran-7izb
    key: quran-7izb
    id: quran-7izb
    position: 58
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
  pWork:
    input: number
    accessorKey: pWork
    key: pWork
    id: pWork
    label: pWork
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
  travelingDist:
    input: number
    accessorKey: travelingDist
    key: travelingDist
    id: travelingDist
    label: travelingDist
    position: 59
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
  Steps:
    input: number
    accessorKey: Steps
    key: Steps
    id: Steps
    label: Steps
    position: 60
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
  quranReading:
    input: number
    accessorKey: quranReading
    key: quranReading
    id: quranReading
    label: quranReading
    position: 61
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
  pWorkDh:
    input: number
    accessorKey: pWorkDh
    key: pWorkDh
    id: pWorkDh
    label: pWorkDh
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
  dailyDh:
    input: number
    accessorKey: dailyDh
    key: dailyDh
    id: dailyDh
    label: dailyDh
    position: 45
    skipPersist: false
    isHidden: false
    sortIndex: -1
    width: 134
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  vWiamElOuaham:
    input: number
    accessorKey: vWiamElOuaham
    key: vWiamElOuaham
    id: vWiamElOuaham
    label: vWiamElOuaham
    position: 63
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
  vAnasBerka:
    input: number
    accessorKey: vAnasBerka
    key: vAnasBerka
    id: vAnasBerka
    label: vAnasBerka
    position: 64
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
  vChaimaaHakim:
    input: number
    accessorKey: vChaimaaHakim
    key: vChaimaaHakim
    id: vChaimaaHakim
    label: vChaimaaHakim
    position: 100
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
  Quran/7izb:
    input: number
    accessorKey: Quran/7izb
    key: Quran/7izb
    id: Quran/7izb
    label: Quran/7izb
    position: 100
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
  remove_field_when_delete_column: false
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
  pagination_size: 25
  font_size: 10
  enable_js_formulas: true
  formula_folder_path: /
  inline_default: true
  inline_new_position: last_field
  date_format: yyyy-MM-dd
  datetime_format: "yyyy-MM-dd hh:mm A"
  metadata_date_format: "yyyy-MM-dd hh:mm A"
  enable_footer: false
  implementation: default
filters:
  enabled: false
  conditions:
```