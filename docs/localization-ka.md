# Georgian interface

> **Last reviewed:** 2026-10-13 · **Last updated:** 2026-10-13 · **Change:** minor (Georgian interface table, ka-GE regional format, terminology) · **Target:** GridCraft 0.6.1

Choose **View › Interface language › ქართული** or **File › Options › Interface language ›
ქართული**, or follow a Georgian system display language (`ka`, `ka-GE`, `ka_GE.UTF-8`; the web
app reads `navigator.language`). The language code is `ka`: `app.language.set` with
`{"language": "ka"}` selects it explicitly, and the choice is saved as `"language": "ka"` in
`ui.json` with the other interface settings. Workbook contents, function names, command ids,
CLI/MCP/control responses and file paths do not change.

Numbers, dates and times follow the separate **File › Options › Regional format › ქართული
(საქართველო)** (`app.region` with `{"region": "ka-GE"}`), which a Georgian system selects on first
run: decimal comma, no-break-space digit groups, `dd.mm.yyyy` short date, `dddd, d mmmm, yyyy` long
date, 24-hour time, Georgian month and weekday names (typed month names are read too), and the lari
after the amount (`1 234,50 ₾`). Number format codes and files stay en-US.

`crates/ui-egui/src/i18n/ka.rs` translates all 382 keys of the interface table in
`crates/ui-egui/src/i18n.rs`: the ribbon, sheet tabs, status bar modes, number-format names,
Backstage (File) pages, header and footer tools and Options. Like every other language on `main`,
dialogs, context menus, task panes, tooltips, messages and function help are still English
literals. Function names, `TRUE`/`FALSE` and error values (`#DIV/0!`) stay English, as for
Japanese, Chinese and Korean: formulas mix Georgian text with Latin cell references, so one keyboard
layout serves the whole formula. The built-in samples (File › New) are written in Georgian when the
interface is Georgian, with amounts in lari. The translations are written from the meaning of the
English labels; no proprietary translation resources were consulted.

## Georgian script

- **No case.** Mkhedruli has no capital letters; Mtavruli is an all-caps style only. Labels are
  written in lower case, and `PROPER` and Flash Fill's proper case leave Georgian letters alone
  (`gridcraft_core::capitalizes`), while `UPPER` still gives Mtavruli as Unicode defines it.
- **Counts.** A noun after a number stays singular, so count labels are written count-neutral
  (`სიტყვა: {n}`); the table has no plural forms and doesn't need them.
- **Fonts.** Nothing is bundled. `crates/ui-egui/src/theme.rs` appends a system Georgian face to
  every family (Sylfaen on Windows, SF Georgian or Arial Unicode on macOS, Noto Sans Georgian or
  DejaVu Sans on Linux) and a currency face for `₾`. `storytold/craft-fonts` has no Georgian face
  yet, so the web build shows Georgian only where the browser supplies a font.

## Terminology

Follow these when adding strings; they come from the Craft apps' shared Georgian glossary and the
native speaker's review.

| English | ქართული |
|---|---|
| File / Home / Insert / Draw | ფაილი / მთავარი / ჩასმა / ხატვა |
| Page Layout / Formulas / Data / Review / View | გვერდის განლაგება / ფორმულები / მონაცემები / განხილვა / ჩვენება |
| Paste / Paste Special… | ჩასმა / სპეციალური ჩასმა… |
| Cut / Copy | ამოჭრა / კოპირება |
| Bold / Italic / Underline | მუქი / დახრილი / ხაზგასმული |
| Wrap Text / Merge & Center | ტექსტის გადატანა / შერწყმა და ცენტრირება |
| Conditional Formatting | პირობითი ფორმატირება |
| Format Cells… | უჯრების ფორმატირება… |
| Insert Sheet Rows / Columns | ფურცლის სტრიქონების ჩასმა / ფურცლის სვეტების ჩასმა |
| Hide Rows / Unhide Rows | სტრიქონების დამალვა / სტრიქონების გამოჩენა |
| AutoSum / Flash Fill | ავტოჯამი / მყისიერი შევსება |
| PivotTable / Table | კრებსითი ცხრილი / ცხრილი |
| Sparklines | მინიდიაგრამები |
| Header / Footer | ზედა კოლონტიტული / ქვედა კოლონტიტული |
| Name Manager | სახელების მართვა |
| Trace Precedents / Trace Dependents | გავლენის მქონე უჯრების მიდევნება / დამოკიდებული უჯრების მიდევნება |
| Evaluate Formula | ფორმულის ნაბიჯ-ნაბიჯ გამოთვლა |
| Calculation Options / Manual | გამოთვლის პარამეტრები / ხელით |
| Sort & Filter | სორტირება და ფილტრი |
| Data Validation | მონაცემთა შემოწმება |
| What-If Analysis / Goal Seek… | ანალიზი „რა მოხდება, თუ“ / მიზნის ძიება… |
| Freeze Panes | არეების დაფიქსირება |
| Page Break Preview | გვერდის გამყოფის გადახედვა |
| Formula Bar / Gridlines / Headings | ფორმულათა ზოლი / ბადე / სათაურები |
| Comment / Note | კომენტარი / შენიშვნა |
| Currency / Accounting / Percentage | ფულადი / საბუღალტრო / პროცენტული |
| Lookup & Reference | ძებნა და ცნობარები |
| Blank workbook / Save As | ცარიელი სამუშაო წიგნი / შენახვა როგორც |
| Options / Regional format | პარამეტრები / რეგიონული ფორმატი |

Commands are verbal nouns (masdar: შენახვა, წაშლა), not imperatives; `…` stays on labels that open
a dialog; product and format names (`Excel`, `CSV`, `PDF`) stay as they are.

## Maintenance

A new interface string is a new `("English", "…")` row in `i18n.rs`'s `JAPANESE` table plus one
`"English" => "ქართული",` line in `i18n/ka.rs` (and in the other languages' files). Keep `\n` in
ribbon labels at a natural word boundary, and keep `{page}`-style placeholders, shortcuts in
parentheses (`(⌘X)`) and `…` exactly. A `context|label` key (`Page Layout|Orientation`)
translates the label in that context. `cargo test -p gridcraft-ui-egui --lib i18n` fails when a key
has no Georgian translation (`missing Georgian: …`) and checks the `ka`/`ka-GE` tags; regions are
checked by `cargo test -p gridcraft-core region` and `cargo test -p gridcraft-numfmt`; the
Georgian face by `theme::tests::fallback_covers_its_script`.

## Revision history

| Date | Change | Summary |
|---|---|---|
| 2026-10-13 | minor | Created: Georgian interface table (382 keys), ka-GE regional format, font fallback, casing, Georgian samples, terminology |
