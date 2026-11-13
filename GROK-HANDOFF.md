# Handoff for Grok: TBG Formulation screens into Figma (WBA)

You are taking over a job from Claude. The goal: build the 56 TBG Formulation screens into
Figma as real WBA screens, made from **instances of the published WBA Design System library**.
Nothing gets hand-drawn if the library has a component for it.

Read this whole file before you touch Figma. The rules are strict because the last attempt to
do this without them (the TBG 2nd-tier Declaration board, 10/Nov/2026) came out looking
nothing like WBA: Inter type, 16px padding, typed "ICW", text glyphs as icons, zero instances.

---

## 0. Inputs

| What | Where |
| --- | --- |
| The screens (content, copy, flow) | Static site: `https://marconip2026.github.io/bg-formulation-screens/` (index lists all 56 pages; every page is a plain HTML snapshot) |
| Site source | GitHub repo `marconip2026/bg-formulation-screens` |
| Original canvas | Claude Design canvas "TBG Formulation Screens" (Marco has the link) |
| Target Figma file | **TBG Ethical & SQA** · `HUpqECP1pJFN3GXZcMJgRH` — new page `TBG Formulation` (ask Marco if he wants another file) |
| Component library | **WBA Design System** · `a3aZGdGwAnlYkxdkTwrrZ6` |
| WBA library key (for `search_design_system` → `includeLibraryKeys`) | `lk-497894441e5ffd200879dd6937854d8991f118d0c5c51cce3e28857c68997fbc38f684bcc487240f084afd7689e454a52aeea76fad29f8822b40d29d61584dee` |
| Gold frames to clone chrome from | SVSI · `aJIs39okLTRsQMwk96NWrC` — [Buyer / Invoice · 01 Pending Payment](https://www.figma.com/design/aJIs39okLTRsQMwk96NWrC/SVSI?node-id=850-19241), [Buyer / Application · 00 Waiting for supplier (empty)](https://www.figma.com/design/aJIs39okLTRsQMwk96NWrC/SVSI?node-id=8025-31778) |
| Real icw logo | TBG Ethical & SQA: colour `7624:1045`, white `567:12769`. Also in the repo: `assets/icw-logo-white.png`, `assets/icw-logo.png` |

**The site is content, not design.** Take copy, fields, states and order from it. Take every
visual decision from this file and the library. The site was already partly corrected (navy
buttons, real logo), but it still carries off-grid spacing, odd font sizes and hand-made chips
— see section 7. Do not copy those into Figma.

**Never** capture the HTML straight into Figma (html-to-design, `send_code_to_figma`, browser
capture) for a final screen. Capture keeps the source's look, which is the defect. A capture is
allowed only as a throwaway reference frame named `ref · …`, deleted before hand-off.

---

## 1. Library gate (hard stop, before anything else)

1. Open a session on the target file and list its libraries.
2. **WBA Design System must be enabled in the file.** If it is not: stop, tell Marco to enable
   it (Assets → Libraries), build nothing. Never fall back to drawing frames "for now".
3. Other libraries (QMAS / Ant Design, Design System Workshop, RH, i-Source) may be on too.
   **Ignore them.** Every search passes `includeLibraryKeys` = the WBA key. Never import a
   QMAS / Ant / Material Kit key, even if it looks closer.
4. Write the result at the top of your report: `Library gate: WBA ✓ (QMAS present, ignored)`.

---

## 2. Instance, never draw

```js
const c = await figma.importComponentByKeyAsync(KEY);   // single component
// or for a set: const set = await figma.importComponentSetByKeyAsync(KEY); set.defaultVariant
const inst = c.createInstance();
inst.setProperties({ 'Label#6:0': 'SAVE', 'Variant': 'Contained', 'Color': 'Primary 1', 'Size': 'M' });
```

Hand-building a button, chip, field, table cell, tab, app bar, stepper, dialog, menu or snackbar
is a defect. Author raw nodes only for page-specific data rows and layout frames. If a key fails
to import, the library has not been published since that component was made: **say so and
stop** — do not silently hand-draw a replacement.

### Component keys (read from the library 11/Nov/2026; `#nn:n` = real property names)

| Component | Key | Properties |
| --- | --- | --- |
| `NavigationBar` (46) | `7ca371f198f01fce476fc1a00fc7240df32a5cc0` | boolean `Create action#151:0`; six `nav item` frames, active = item 3. No label prop: overwrite texts |
| `Header` (90) | `d11858252d39726c0a9bf64e88f71653cc452447` | two texts: title, meta line |
| `Tab` | `7f21dddafdc1c5bd8182a7e67ddcd1324d301347` | `Label#18:0` · `State` Default/Active |
| `RegularTab` | `ca9825d184bc2f29ed1e117a4acf9ad7870b5108` | run of Tabs + 1px divider |
| `Stepper` (76) | `15481888217d8eff1cce9a609951b131fc84f466` | `Progress` 25/50/75/100 |
| `TaskStep` | `e0ee6dbf94ad2762dfdff250f51590191466cd4b` | `State` Done/Current/Upcoming · `Label` |
| `Button` | `181499dbf0c2da872d6a1ed0ab8fa01c5df71e66` | `Label#6:0` · `Caret#188:0` · `Variant` Contained/Outlined/Text · `Color` Primary 1/Primary 2/Disabled/Danger · `Size` M/S |
| `IconButton` | `0ee17c087eac16e14b7add230846e44f642c7fd7` | `Variant` · `Size` M/S/XS |
| `URLButton` | `76a7141f8c707691740502fdaaec58bcf971b25f` | `Label#56:3` · `State` Primary 1/Primary 2/Disabled |
| `LongButton` | `c999f3f8fa9ac5a7dabbb823ef863eb217cfe69a` | `Label#11:0` · `Color` · `State` |
| `Chip` | `9c23c2f6061a35ce971d783bb10b6d31f280ad6d` | `Label#7:0` · `Style` Filled/Outlined · `Tone` Neutral/Info/Success/Warning/Error · `Size` M/S |
| `StatusTag` | `26b88750150db8d3b3bce00cf74d8c6aac804baf` | `Label#54:0` |
| `TrafficLight` | `4749f7352aa98965b13eba638f9c188529c0d67b` | `Label#8:0` · `Tone` Success/Warning/Error/Info/Neutral |
| `TierChip` | `7793efeba2c10d4b1bae30cae5eef39a9d88babf` | `Tier` Not Rated/Bronze/Silver/Gold/Out of Scope |
| `SelectionChip` | `eb346bd4222343e7d9e8e8d78243885c25952117` | `Label#11:5` · `State` · `Size` — set HUG after the label |
| `Badge` | `adeeab5c5e8d40d9fdffbbb775f29af7cc85a9be` | `Count#7:28` · `Tone` · `Size` |
| `TextField` | `d133819964aebf8c689c3b648fc6603708bc168f` | `Label#12:0` · `Value#12:6` · `Helper#12:12` · `State` Default/Filled/Focus/Typing/Dropdown/With Icon/Multi-Line/Error/Disabled/Date |
| `Radio` | `f25314bf4afe990a90c5cd6ee1255e98480899b4` | `Label#13:8` · `State` Unselected/Selected/Disabled |
| `Checkbox` | `ae0f34cc797ed290de1580b50290ce18b944b394` | `Label#13:3` · `State` Unchecked/Checked/Indeterminate/Disabled |
| `TableCell` | `b32913906e2d19cab7f849238c4a2d485684655c` | `Value#16:0` · `Type` Header/Body/Link/Numeric |
| `KVRow` | `5a6db5208df1b98fcf5001a8b9b02edddea157bb` | `Key#225:4` · `Value#225:7` · `Divider` On/Off (key cell 200) |
| `KVGrid` | `b76b6a90eb95eef71d030106babf0c54980a6088` | 3 × KVRow in a table outline |
| `FileRow` | `d4c64cd9537a40e2df0df88c165d27e5350eae16` | `FileName#225:10` · `Deletable#225:11` |
| `DocumentRow` | `ea158a7da6153c82a0252af25d83837e27f19d3c` | `Type` Header/Row · `Divider` · Version/File/Date/By |
| `DocumentTable` | `057df45f7fab8e494938f4f3cf5b915bd8b7d5fc` | header + rows |
| `Alert` | `5bb414920874eabec3330269ef1c13b63c204729` | `Message#201:0` · `Tone` Success/Info/Warning/Error |
| `Snackbar` | `71396fdbe7117f0c55f2f9476cb1efec95783e8d` | `Message#57:0` · `Action#130:0` · `Tone` (always Default) · `Lines` |
| `Dialog` | `bf0f8ef1962d69e6fded32361fb64d4238ee29ae` | `Size` Small 286 / Big 560 |
| `PopUpTitle` | `1527d11e88aa915c5073c02a0ab967979fe515dd` | dialog title row |
| `DataTooltip` | `be07fba6f4f20350071ca595ceacaed2c3d4f325` | long-name hover |
| `Tooltip` | `d00a79273ed4c8374b2cc4da081455c3fc0af7a9` | |
| `Scrollbar` | `cc07b4cded9e32b85aabecf594679ba282f7f8e6` | `Thumb` · `Position` |
| `Card` | `7895b40cfef34087572db2175508bf5c2fef687e` | `Width` 1200/770/585/400 — **no content slot** (see below) |
| `IconBack` | `329ffe742b5fbd4315d7155939fb0ad42f4982bc` | back glyph, 54% black |
| `IcClose` | `6911996e0ef171a143e2894fda36c317a9188e30` | close glyph, 54% black |
| `Paging` | `435dcb2afda088539ef5167becfebfe242d0206c` | **do not use** — still draws `‹ ›` as text; build pagination from icons |

**Library gaps** (author these as frames, styled from tokens): section cards (`Card` has no slot →
frame with `surface/card` fill, radius 4, `Elevation/Card` effect, 30 padding), Role switch,
Factory/Item detail header (79), Sub Tabs, Cycle Rail, Task Card, Section header.

### Text styles (bind with `setTextStyleIdAsync` after `importStyleByKeyAsync`)

`Para/12 Regular` `e59545d284f10a344e6d7f798fb1f20663b59743` · `Caption/12 Regular` `6dcbec625a53381c0cef876085e05f3cf5f8fdc2` ·
`Body Small/12 Medium` `40031f5c9be4d1ab4a3c53d0e4236a8a2b02f7e8` · `Body/14 Medium` `d7e7498a94e4a935ac6a02655d0e0a15a6cf255c` ·
`Subtitle/16 Bold` `d5d9a64f6a9e3aab67ee10b0762c6b1eba96aa12` · `Title/20 Bold` `8ce2c5473194f124332b7fbbe7aecdf7978ed666` ·
`Headline/24 Medium` `c41ee6ac0fa69a81eac0dd84e0ce3be49800d6f9` · `Display/36 Bold` `d92096a97659fbf2ce9391dd0b5aae13a5866393` ·
`Button/14 Medium Upper` `d6141fff709d7339caf8a62210ab606e77d654ef` · `Chip/10 Medium` `b3cd644d44eef12c49494fb025fab0e7a55f1055`.
Effect: `Elevation/Card` `8332d8b67c8791bbd28c7b2c1a8c34a5b49f56e2`.

Never set `fontSize` / `fontName` / `letterSpacing` after binding a style — that detaches it.

### Colour variables (`importVariableByKeyAsync`, then `setBoundVariableForPaint`)

`text/body` `8fdef1b37915df14563be2b7ebba9b7e19d1d4a7` · `text/primary` `a05060ebf7630b2d92428d366ba3504e54193c55` ·
`text/secondary` `afffcc4be42e9a7f9a482ab47589ee7c7728eca3` · `text/muted` `bfc86c8168738279fce88491ff70a89112b94e18` ·
`text/link` `afa2ce7f2a4b8522607416ffee6fc7ebe7a6e72c` · `text/error` `d5a61062fc8d755aea2fc747e85134569c58bee0` ·
`surface/app` `c668a1dd65392519aa699a049028f5a39a7978b1` · `surface/card` `23567d7be5bc9ec9116b8fe23029ee5ae19e1b4c` ·
`border/table` `e4ca55862486bbe2c66afefa9be55b6906d616d3` · `border/divider` `71936918e9fb97e2a076244c4d2250f10be65c5e` ·
`state/info` `b6b8c3ec97200d0b557276cc2bb51f8fca24fcd3` · `state/success` `9e682d8d18b03a4ad4cdef1eb1bd0e3ff7073ec7` ·
`state/error` `178cc7c222fbba5cba171d038c95b54fb34c8393` · `state/warning` `947a607f5697849e9ee7f0f1c3a1a3509eae8562`.

If you need an opacity on a bound paint, put `opacity` in the paint **before** binding.

---

## 3. Icons are components too

Never a hand-drawn vector, never a text glyph (`→ ← › ▾ ☑ ● ✓ ×`, emoji). Import the **WBA** key
(the Design System Workshop copies look identical but are not ours). Size with `rescale()`,
never `resize()`. Recolour through the `BOOLEAN_OPERATION` fill, not every vector.

```js
const i = (await figma.importComponentByKeyAsync(KEY)).createInstance();
i.rescale(20 / 24);
for (const s of i.findAll(n => n.type === 'BOOLEAN_OPERATION')) s.fills = [boundPaint('text/muted')];
```

| Icon | WBA key | Use |
| --- | --- | --- |
| `Content/ic_filter_list` | `c0d35519f24d7c15cd58bd4919d3d2fe5fe75111` | column filter |
| `Content/ic_sort` | `255f99c626f72614069624316496654aa30b59bd` | sortable column |
| `Content/ic_create` | `8e3de5867457bf36e1642a4f4d6e4d196e0f580f` | edit |
| `Content/ic_clear` | `c28b9e792106ca80c33380af00d9a3de68887241` | clear / cancel |
| `Content/ic_add` | `83117a157e81def23581b5d0f96bccf8d34e0930` | add |
| `Action/ic_search` | `d6ac2d91a7cf49e70ebbf9239ad9e2450ecb26a0` | search |
| `Action/ic_today` | `9d0f0ef59d6ba382f037eabc07107eb7f509aaad` | date field |
| `Action/ic_date_range` | `2dfb74a3d1a0680bdc2a982b24f6852c1d29a2bb` | date range |
| `Action/ic_event` | `acb2b2cb52ee21617474542c745f887f6f0fff9e` | scheduled date |
| `Action/ic_done` | `d2a27ad10747ab632d07adb78a9ef25d7a0d61e6` | confirm / done step |
| `Action/ic_delete` | `93b4ccf53d04ecea0fec4a792dfe98696e312452` | remove |
| `Action/ic_visibility` | `0e00e44517c1be5bb9210ff717291a310a66749d` | preview |
| `Action/ic_info` | `d1a22a09c1fc7dfaf5a18b0cdddb3fbd0589f5d9` | hint |
| `Hardware/ic_keyboard_arrow_down` | `7284d3f47b159dbda68dfce850bc5fbef324aa9f` | select caret, expand |
| `Hardware/ic_keyboard_arrow_up` | `947a70b48f97f5ffe60e499786d55f55d1e0c9ea` | collapse |
| `Hardware/ic_keyboard_arrow_left` | `eb1739f76ec636c1f28a0d64aa3febb4bb77e505` | back |
| `Hardware/ic_keyboard_arrow_right` | `0f13599ba9d3207097d6baa5f3203416886cf9d3` | drill in, breadcrumb separator |
| `Navigation/ic_chevron_left` | `b09205a5704c6ebdd11c4bd75cc18ba39d87b371` | previous page |
| `Navigation/ic_chevron_right` | `7be7c6b7cad4731c09150768774cfdeb64068d31` | next page |
| `Navigation/ic_arrow_drop_down` | `70a12a0fd57e4243d35c36c591d2e64429eb4c24` | inline dropdown |
| `AV/ic_skip_previous` | `ac1e2c28eeb28c33d95e11b8a34f909c30b01f1c` | first page |
| `AV/ic_skip_next` | `e46fc4f8d143966947fe5b9f433198dfb9e97a83` | last page |
| `File/ic_file_download` | `55b352c27b7258efb8e2c26ab3b5c7d85695f4a2` | download |

Not in the set (do not draw them): `ic_close`, `ic_check`, `ic_first_page`, `ic_last_page`,
`File/ic_file_upload`, `ic_attachment`. Use the substitutes above.

---

## 4. Translate each site element into WBA

| Site element | WBA in Figma |
| --- | --- |
| Blue top bar with "icw" + menu | `NavigationBar` 46 + white icw logo (41×24, 20 from left). Overwrite the placeholder labels; active item = copy item 3's fill + 3px lime bottom stroke |
| Item / formulation detail header (back, crumb, title, meta line, ACTIONS) | Clone the Factory Header chrome from the SVSI gold frame (79 high, padding 18/24); `ACTIONS` = `Button` Contained, Caret on |
| Page title + right buttons on list pages | toolbar row: title `Headline/24 Medium` · `TextField` search · spacer · `Button`s |
| White section box | authored card frame (surface/card, radius 4, Elevation/Card, padding 30) — no coloured left bar |
| Blue-left-bar / tinted info box | `Alert` (Info / Warning / Error) |
| Inputs, selects | `TextField` (State Filled / Default / Dropdown / Error / Disabled / Date) |
| Yes/No, option cards | `Radio` |
| Checkbox lists | `Checkbox` |
| Status pills (Approved, Pending, Pass, Fail, In review…) | `TrafficLight` (status phrase + dot) or `Chip` with the right `Tone`; supplier tiers → `TierChip` |
| Market badges EU / GB / US / AU | `Chip` Size S, Tone Success (OK) / Warning (restricted) / Error (prohibited) |
| Filter pills above a table (`All (5)`, `Testing (2)`) | `SelectionChip` row |
| Key : value lists | `KVRow` / `KVGrid` |
| File links / documents | `FileRow` / `DocumentTable` |
| Data tables | `TableCell` instances in a fully ruled grid (0.5px `border/table` on every side, header row 40, body row 60, never zebra) |
| Tabs (`Task (5)`, `Detail`, `Approvals`) | `Tab` instances |
| 4-step create wizard | `Stepper` (76) |
| Workflow step row (Supplier input → … → Live) | `TaskStep` row, itemSpacing 0, each FILL |
| Journey bar (1 Concept brief … 12 Life-cycle) | board furniture or `TaskStep` row — ask Marco if it stays in the product |
| Dialog over scrim | `Dialog` Big 560 + `PopUpTitle`, 25% black scrim frame underneath |
| Full-width bottom CTA | `LongButton` |
| Pagination text `1–10 of 318` | build: `Rows per page: 20` + caret · `1 - 10 of 318` · `Page: 1` + caret · skip/chevron icons |
| "Placeholder", "roadmap", "Prototype: mark all done", journey notes | yellow `Note` frame beside the screen, never inside it |

### Copy pass (apply while mapping)

- Buttons UPPERCASE (`Add substance` → `ADD SUBSTANCE`). Everything else sentence case.
- Remove `› → ← ▾ ☑ ● •` and emoji from copy. Breadcrumb/approval chains use the
  `ic_keyboard_arrow_right` icon at 14px between text runs, or plain commas.
- Tabs naming a collection: plural, space before count — `Claims (214)`, `Task (5)`.
- Filter chips / queue counts: count in the label, `All(877)`.
- Dates: `DD/MMM/YYYY` in detail views, `DD/MM/YYYY` in list tables.
- Empty values by meaning: `/` = a later step fills it · `N/A` = does not apply · `—` = empty
  read-only table cell. Never blank, `TBD`, `-` or `unknown`.
- Statuses: two-word Title Case + dot (`In Progress`, `To Do`, `Signed Off`).
- Say Supplier (not Vendor), Buyer (not QT/QA), TBG (not "client").
- No exclamation marks, no marketing adjectives.

---

## 5. Grid, type and layout

- Every padding and gap is a multiple of **10** (`10 20 30 40 50 60 80 100 120`). **5** is the
  only half-step, and only inside table cells, chip internals, icon-to-number gaps.
  No 4, 8, 12, 14, 16, 18, 22, 24, 26, 28.
- Control heights stay as the library defines them: button 36 (28 in table toolbars), field 40,
  chip 24/20, table header 40, body row 60, app bar 46, stepper 76.
- Type: Roboto only, via the text styles above. Sizes 10 / 12 / 14 / 16 / 20 / 24 / 36. The
  site's 13, 12.5, 13.5, 11.5, 15, 18, 22px map to the nearest style (13→12 or 14, 18→16, 22→20 or 24).
- Radius 2 on controls (buttons, chips, search), 4 on surfaces (cards, dialogs, fields, menus),
  square on table cells and the app bar.
- Shadows: only the library effects. No blur, no glow.
- Page frame 1440 wide, fill `surface/app`. Content max 1200 centred, or the SVSI detail layout
  (rail 378 + task card) for item / formulation detail pages.
- Everything authored is auto-layout. Flexible = FILL, fixed columns = FIXED, labels = HUG.
  Set `layoutSizing*` AFTER `resize()` (resize resets sizing to FIXED).

---

## 6. Board layout in Figma

- One page `TBG Formulation`. One red-outlined group section per heading in section 8 (A, B,
  B2, C, D, 00 … 11, Shared), in that order, top to bottom.
- Frames in a row step by 1640 (1440 + 200). Every frame named exactly as in section 8.
- Caption above each frame: Roboto Bold 60, fixed width = frame width, `textAutoResize =
  'HEIGHT'`, bottom 30px above the frame, node name `caption:<frameId>`. Short Title Case,
  max two lines.
- State variants of one screen sit side by side in the same section. A screen with a dialog or
  popover = a separate frame with the screen under a scrim.

---

## 7. Known problems in the site — fix them, don't copy them

Claude audited the canvas on 13/Nov/2026. The site snapshot has these deviations from WBA;
the Figma build must not inherit them:

| In the site | Do in Figma |
| --- | --- |
| ~1,700 raw hex colours | bind every fill/stroke to a WBA variable |
| ~1,000 off-grid paddings/gaps (12/14/16/18/22/24/26/28) | 10pt grid, 5 half-step |
| font sizes 13, 12.5, 13.5, 11.5, 15, 18, 22 | WBA text styles only |
| 103 hand-made buttons (`a.nb`, `.btn`) | `Button` / `LongButton` instances |
| custom EU/GB/US/AU badges | `Chip` Size S |
| tinted boxes with a 3px left bar | `Alert` |
| 27 inline SVG icons, `+` and `›` as icons | WBA icon instances |
| pagination as plain text | built pagination (section 4) |
| TopNav labels CONCEPT BRIEF · ITEM LIST · FORMULATION · SUBSTANCE LIBRARY · MATERIAL LIBRARY · CLAIMS, role pill | **ask Marco** whether these stay for the TBG module or revert to `HOME · ITEM LIST · SUPPLIER · PO · ANALYTICS · eFiling`; role → `Role switch` (local SVSI component `e1988dcfdd4d5da284a8795eb27a29f34c44505e`) |
| `Claims(214)` tabs | `Claims (214)` |
| statuses like `To do`, `Pending`, `Matches · all substantiated` | two-word Title Case + dot |
| prototype helpers ("Prototype: mark all done", "end of walkthrough", "roadmap") | Note frames, not in the screen |

---

## 8. Screens to build (56)

Build in this order. Do one section, run the lint (section 9), show Marco screenshots, then go on.

### Start here: press Play

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 01 | `Start.html` | `Start · Choose a journey` |
| 02 | `Dashboard.html` | `Reporting dashboard (3)` |

### A Concept brief › formulation › sign-off (formulation screen sits in B2)

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 03 | `ConceptList.html` | `A · Concept brief list` |
| 04 | `ConceptCreate.html` | `A · Create concept brief` |
| 05 | `ConceptBrief.html` | `A · Concept brief workspace` |
| 06 | `ConceptBriefSignoff.html` | `A · Concept brief sign-off (all formulations signed off)` |
| 07 | `ConceptBriefSigned.html` | `A · Concept brief after sign-off` |

### B Item page, PLM tab › one view per workstream

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 08 | `ItemPLM.html` | `B · PLM tab · Formulation` |
| 09 | `ItemPLMUseDetails.html` | `B · PLM tab · Use details` |
| 10 | `ItemPLMBOM.html` | `B · PLM tab · BOM` |
| 11 | `ItemPLMClaims.html` | `B · PLM tab · Claims & pack copy` |
| 12 | `ItemPLMArtwork.html` | `B · PLM tab · Artwork` |
| 13 | `ItemPLMSpec.html` | `B · PLM tab · Specification` |
| 14 | `ItemPLMUsedIn.html` | `B · PLM tab · Used in` |

### B2 PLM workstream screens, aligned under each PLM tab view › formulation › use details › BOM & packaging › claims & pack copy › artwork › specification › used in › packaging component

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 15 | `FormulationTasks.html` | `B2 · Formulation (tasks and sign-off)` |
| 16 | `ProductUse.html` | `B2 · Use details` |
| 17 | `ProductBOM.html` | `B2 · BOM & packaging` |
| 18 | `ProductClaims.html` | `B2 · Claims & pack copy` |
| 19 | `Artwork.html` | `B2 · Artwork review` |
| 20 | `Specification.html` | `B2 · Specification (1.5)` |
| 21 | `GiftBOM.html` | `B2 · Used in: gift set BOM` |
| 22 | `PackagingComponent.html` | `B2 · BOM sub-flow: packaging component` |

### C Sealing › product information file › notification › shipment

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 23 | `Sealing.html` | `C · Seal sample approval` |
| 24 | `ProductDossier.html` | `C · Product information file and DoC (1.7)` |
| 25 | `Notification.html` | `C · CPNP and SCPN notification` |
| 26 | `ShipmentRelease.html` | `C · Shipment release` |

### D Life-cycle changes

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 27 | `ChangeRequest.html` | `D · Life-cycle change request` |

### 00 Substance library

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 28 | `Main.html` | `00 · Substance library list` |
| 29 | `SubstanceDetail.html` | `00 · Substance record, market rules` |
| 30 | `SubstanceAdd.html` | `00 · Add substance, market rules` |
| 31 | `SubstanceImport.html` | `00 · Bulk import, check rows` |

### 01 Formulation library

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 32 | `FormulationLibrary.html` | `01 · Formulation library` |
| 33 | `FormulationRecord.html` | `01 · Formulation record` |
| 34 | `RecipeCMO.html` | `01 · Manufacturing recipe and CMO transfer (1.4)` |

### 02 Build a formulation

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 35 | `CreateBasics.html` | `02 · Step 1, basic information` |
| 36 | `CreateComposition.html` | `02 · Step 2, build composition` |
| 37 | `AddSubstanceDialog.html` | `02 · Add from substance library` |

### 03 Compliance check & submit

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 38 | `ComplianceCheck.html` | `03 · Step 3, compliance check` |
| 39 | `PreviewSubmit.html` | `03 · Step 4, preview & submit` |

### 04 Apply formulation to products

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 40 | `LinkProducts.html` | `04 · Set formulation for products` |

### 05 Supplier-developed formulation

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 41 | `SupplierRequest.html` | `05 · Request formulation from supplier` |
| 42 | `SupplierFill.html` | `05 · Supplier fills formulation details` |
| 43 | `NewSubstanceRequest.html` | `05 · New substance request` |
| 44 | `SupplierESG.html` | `05 · Supplier certificates, ESG and EUDR (1.10)` |

### 06 TBG review & approval

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 45 | `RegulatoryReview.html` | `06 · Review formulation` |
| 46 | `RestrictionDetails.html` | `06 · Restriction details` |

### 07 Supplier costing

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 47 | `CostEntry.html` | `07 · Supplier fills price request (cost breakdown)` |

### 08 Revisions & impact

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 48 | `Revisions.html` | `08 · Revisions & compare` |
| 49 | `WhereUsed.html` | `08 · Where used after a rule change` |

### 09 Material library

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 50 | `MaterialLibrary.html` | `09 · Material library` |
| 51 | `MaterialRecord.html` | `09 · Material record` |

### 11 Claims & wording

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 52 | `ClaimsLibrary.html` | `11 · Claims and wording library` |

### Shared parts

| # | Page (site) | Figma frame name |
| --- | --- | --- |
| 53 | `TopNav.html` | `Shared · Top navigation` |
| 54 | `JourneyBar.html` | `Shared · End-to-end stage bar` |
| 55 | `ItemHeader.html` | `Shared · Item page header (Task / PLM tabs and sub-navigation)` |
| 56 | `RestrictionPopup.html` | `Shared · Restriction details pop-up` |

`Shared` parts (TopNav, ItemHeader, JourneyBar, RestrictionPopup) are reference only: build
them once as the chrome inside the screens, not as separate deliverables, unless Marco asks.

---

## 9. QA lint — run it, paste the numbers, don't hand off until it passes

```js
const FRAME_IDS = [/* your new frames */];
const GLYPHS = /[→←↑↓▾▸▶◀☑☐●○•✓✕×›]|\p{Extended_Pictographic}/u;
const CONTROL_NAMES = /button|btn|input|field|chip|tag|badge|radio|checkbox|tab|nav|select|dropdown/i;
const r = { instances:0, localInstances:0, keys:{}, nonRoboto:0, glyphText:0,
            unboundFill:0, unstyledText:0, rawControls:[], offGrid:[] };
for (const id of FRAME_IDS) {
  const root = await figma.getNodeByIdAsync(id);
  const all = [];
  (function walk(n){ all.push(n); if (n.type !== 'INSTANCE' && 'children' in n) n.children.forEach(walk); })(root);
  for (const n of all) {
    if (n.type === 'INSTANCE') {
      r.instances++;
      const mc = await n.getMainComponentAsync();
      if (!mc || !mc.remote) { r.localInstances++; continue; }
      const owner = mc.parent && mc.parent.type === 'COMPONENT_SET' ? mc.parent : mc;
      r.keys[owner.name] = owner.key;
      continue;
    }
    if (n.type === 'TEXT') {
      if (n.fontName !== figma.mixed && n.fontName.family !== 'Roboto') r.nonRoboto++;
      if (GLYPHS.test(n.characters)) r.glyphText++;
      if (!n.textStyleId) r.unstyledText++;
    }
    if ('fills' in n && Array.isArray(n.fills))
      for (const f of n.fills) if (f.type==='SOLID' && f.visible!==false && !f.boundVariables?.color) r.unboundFill++;
    if (n.type === 'FRAME' && n.id !== root.id && CONTROL_NAMES.test(n.name) && !n.findOne(x => x.type === 'INSTANCE')) r.rawControls.push(n.name);
    if (n.type === 'FRAME' && n.layoutMode !== 'NONE')
      for (const p of [n.paddingTop,n.paddingRight,n.paddingBottom,n.paddingLeft,n.itemSpacing])
        if (p && p % 5 !== 0) { r.offGrid.push(`${n.name}:${p}`); break; }
  }
}
return r;
```

| Check | Must be |
| --- | --- |
| `instances` | > 0, and every control is one |
| `localInstances` | 0 (the SVSI Role switch is the one allowed exception) |
| `keys` | every key appears in section 2 or 3 |
| `rawControls` | empty |
| `nonRoboto`, `glyphText` | 0 |
| `unboundFill`, `unstyledText` (authored content) | 0 |
| `offGrid` | empty — except chrome cloned from SVSI gold frames (list it separately) |

Then screenshot every new frame at readable zoom and check: chips still 20/24 high, labels not
overflowing, no `#000000` fallback where a bound colour should show.

---

## 10. Figma API traps that already bit this project

- **One error rolls back the whole script run.** Fix the line and re-run all of it; never write
  recovery code that assumes partial application.
- Node proxies go stale after other writes — capture ids into plain data before remove loops.
- You cannot `appendChild` into an instance. Hide the original, add a sibling.
- `resize()` resets sizing modes to FIXED → set `FILL`/`HUG` after it.
- `query()` selectors break on names with spaces → use `children.find(c => c.name === '…')`.
- SECTION children use section-relative coordinates.
- Never run a full-file `findAll` on the library file — it crashes the connection.
- `TierChip` collapsed 20 → 12 after a bulk clone once: after cloning, histogram the heights.

---

## 11. Report back to Marco (in Cantonese, short)

1. `Library gate: …` line.
2. Table: frame name (as a clickable Figma link, `?node-id=` with `:` → `-`) · section · status.
3. Components instanced (name → count).
4. Lint result table from section 9.
5. Screenshots.
6. Deviations you made on purpose, and open questions (nav labels, journey bar).

Every frame you mention must be a clickable Figma link, never a bare node id.
