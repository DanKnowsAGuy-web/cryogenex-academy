# PRODUCT.md — Academy Sports + Outdoors proposal page

## Version 4 (September 2026): three inputs, solar thermal, no price on the page
Per Dan's direction, the ledger takes three inputs instead of one, and the treatment is
paired with a solar thermal add-on held at a 30 percent floor. No cost, price, or tax
credit figure appears anywhere on the page; the output is savings only.

**Controls, in order:** age of the rooftop units (0 to 25 years, default 12); store size
(50,000 to 100,000 sq ft, step 1,000, default 70,000 — Academy's stores run 55,000 to a
130,000 sq ft flagship, clustering at 70,000), which also derives and displays rooftop
tonnage (`sqft / 400`, rounded to the nearest 5 tons); electricity rate (6.0 to 16.0 cents
per kWh, step 0.5, default `RATE_DEFAULT = 10.1`); then the existing one-store/all-322-
stores toggle.

**Electricity rate source.** `RATE_DEFAULT` is set from EIA commercial electricity rates
weighted by Academy's own store count per state, not a simple average:

| Source | Figure |
|---|---|
| EIA Table 4 (2024), commercial rate by state | range 8.6 cents to 13.6 cents |
| Academy 10-K, store count by state | weights applied to the EIA range above |
| Simple average across Academy's states | 10.9 cents |
| **Store-count-weighted average (used as `RATE_DEFAULT`)** | **10.1 cents** |

The page's fine print states the weighted range (8.6 to 13.6 cents) but does not name
individual states, per the standing hard rule against state or region references (see
"Hard rules this page follows," below); the coordinator's original draft of that sentence
named two states specifically, and was edited to drop the names while keeping the range.

**Engine.** `compute()` was replaced with the version 4 engine given verbatim: per-square-
foot constants (`KWH_PER_SQFT = 14.3`, `PEAK_W_PER_SQFT = 6.4`, `MAINT_PER_SQFT`,
`ROOF_COST_PER_SQFT`) replace the fixed per-store figures from version 2 to 3, so the
ledger scales with the size slider. The rooftop units' share of energy and peak
(`HVAC_KWH_SHARE = 0.40`, `HVAC_PEAK_SHARE = 0.55`) and the treatment's peak recovery
(`DEMAND_MAX = 0.125`) are unchanged from version 3. A new `SOLAR = 0.30` constant applies
solar thermal to whatever energy and peak the treatment alone does not recover, at a
30 percent floor. `LOSS` is unchanged.

**Verified in node** at the current defaults (age 12, 70,000 sq ft, 10.1 cents/kWh):
- One store: `hvacKwh` 400,400; `hvacKw` 246.4; `energyToday` $75,922; `treatRec` $13,869;
  `solarRec` $18,616; `demandRec` $13,672; `energyRec` $32,485; `maintRec` $5,364; `lifeRec`
  $3,302; `totalToday` $119,422; `totalAfter` $78,271; `totalRec` $41,151.
- Fleet of 322: `energyToday` $24.4M; `energyRec` about $10.5M; `maintRec` about $1.73M;
  `lifeRec` about $1.06M; `totalToday` $38.5M; `totalAfter` $25.2M; `totalRec` about
  $13.25M; `deferred` $77.28M.

At the original 10.0 cent placeholder rate the code returned: one store `treatRec` $13,775,
`solarRec` $18,524, `energyRec` $32,299, `totalRec` $40,965; fleet `totalRec` about $13.19M.
The coordinator's original spec supplied approximate expected figures at 10.0 cents
(treatRec about $13,760, solarRec about $18,520, energyRec about $32,280, totalRec about
$40,950) that were close to, but not identical to, the code's output; the differences are
consistent with rounding in the spec's own arithmetic, not a code error, so the verbatim
engine was kept as given rather than adjusted to match the approximation.

**Ledger display.** The Electricity row's subtitle changed to "treatment and solar
thermal"; its "how sure" text now reads "Treatment measured elsewhere. Solar thermal at
its floor. Both measured in the pilot." Three fine-print lines under the table now read
"Treatment $X", "Solar thermal $X", and "Of which demand $X" (the former "Kilowatt hours
$X" line was dropped since kWh recovery is now split across the treatment and solar
lines). The closing fine print now credits the rate and size the reader chose, states that
the default rate is the store-count-weighted average across Academy's states (8.6 to 13.6
cents, no states named), notes the per-square-foot electricity source, and states that
solar thermal is held at its measured floor.

**Copy.** Two sentences were added, both supplied verbatim: one at the end of bill one's
second paragraph ("Solar thermal on a restored unit takes the rest of the way: at least
30 percent more.") and one at the end of the mechanism paragraph in the "why" section
("Solar thermal adds heat on the compressor's discharge side, so a restored unit does the
same work with less electricity."). No other copy changed.

**CSS.** `.controls .range-row` (previously `.controls > div:first-child`) now applies the
260px flex-basis to all three sliders, not just the first, so the new size and rate rows
size consistently with the age row on desktop and reset to full width identically on
phones. `assets/brand.css` bumped to `?v=20260924c`.

## Version 3 (September 2026)
Three changes from Dan on top of version 2, all copy-and-type, no structural change:
1. **Type sized for readers 65 and up.** Body text is 1.3rem/1.55, the lead is 1.5rem, labels
   and fine print never drop below 1rem, ledger numerals run 1.5rem on desktop and 1.35rem on
   phone, buttons and the scope toggle are 56px minimum height with 1.15rem text, and the
   range slider has a 32px thumb on a 6px track. `--ink-2` is capped at `#3f4850` so no text
   on the page renders lighter than that. All of it lives in `assets/brand.css`; see DESIGN.md.
2. **The word "cooling" is banned.** This is pitched as an energy play, not an HVAC play.
   Every sentence that referenced cooling, cooling's share, or cooling energy was rewritten to
   talk about electricity, the demand charge, and kilowatt hours directly. `grep -i cooling
   index.html` returns zero hits.
3. **Apple-level concision.** Every sentence on the page was replaced with the shorter version
   Dan supplied verbatim. Visible body text runs to 691 words end to end (header through
   footer), under the 700-word target.

The interactive ledger, its compute() engine, the seven-beat structure, brand.css isolation,
and every hard rule from version 2 (no dashes, no product names, no Texas terms, noindex,
same-origin only) are unchanged.

## Version 2 (September 2026)
Rebuilt around one idea, per Dan's decision: every Academy store pays three bills for
cooling (energy, led by the demand charge; maintenance; the equipment replacement cycle),
and one treatment moves all three. The page is one interactive exhibit, the roof ledger,
plus three short bill sections, a mechanism section, and the pilot ask. Version 1's
five-lever list, sales equation, spread chart, standalone calculator, and three-audience
accordion are gone; their content folded into the ledger and the three bill sections.

## Purpose
A single-file, Energy Plus branded proposal landing page for Academy Sports + Outdoors. The
reader is an Academy VP who opens this on a phone, then forwards it to facilities and finance.
Cryogenex brought the introduction and is credited as the partner; Energy Plus leads the
engineering, the measurement, and the incentive filing.

## Hard rules this page follows
- No em dashes or en dashes anywhere in copy. Ranges use "to".
- No product or vendor names in body copy (no CryoGenX4, HVAC Optimizer, Airco, Tri-S,
  Frontier). "Cryogenex" appears only in the header partner line, the CTA copy, and the
  footer.
- No Texas, Houston, Katy, ERCOT, 4CP, or "113" anywhere. Savings are framed as an average
  store's electric, maintenance, and replacement bills, then multiplied by the 322-store fleet.
- The word "cooling" does not appear anywhere in the page (version 3, per Dan: this is an
  energy play, not an HVAC play). Copy talks about electricity, the demand charge, kilowatt
  hours, and the rooftop units directly instead.
- No stock photos of Academy stores, no Academy logo, no federal agency logos. The only
  photos on the page are Cliff Suljak (grayscale) and the film cover.
- `<meta name="robots" content="noindex, nofollow">` plus a matching robots.txt.
- No third-party scripts. The only external calls are the Google Fonts stylesheet link and,
  on click only, the Wistia iframe for the film. Everything else is same-origin
  (`assets/brand.css`, the inline script).
- Mobile first, no horizontal scroll at 375px. Respects `prefers-reduced-motion`.
- Numbers are not invented: the roof ledger uses the compute() engine given in each version's
  build spec verbatim. As of version 4 that engine takes age, store size, and electricity
  rate as inputs, with LOSS, STORES, KWH_PER_SQFT, HVAC_KWH_SHARE, PEAK_W_PER_SQFT,
  HVAC_PEAK_SHARE, DEMAND_RATE, DEMAND_MAX, SOLAR, MAINT_PER_SQFT, MAINT_MAX,
  ROOF_COST_PER_SQFT, LIFE_YEARS, and EXT_MAX as its only constants. All narrative figures
  (Simon Property Group case, the 94 percent purchased-electricity note, the twelve-units-
  a-roof estimate) cite the spec's own sourcing.

## The roof ledger and DEMAND_MAX
The ledger's JavaScript is the compute() function from the build spec, copied verbatim,
with `DEMAND_MAX = 0.125`: at full fouling, up to 12.5 percent of cooling's share of the
peak kW is recoverable, scaling down with the fouling fraction (10 to 15 percent of
cooling's peak share is the working range described in the spec). The constant stands at
0.125. An earlier draft of this note flagged a mismatch against the spec's narrative
"expected" figures; that narrative arithmetic was in error, not the code, so it has been
corrected rather than the constant. At age 12, one store: $13,785 energy recovered a year,
$5,364 maintenance recovered a year, $3,302 equipment life recovered a year, $22,450 total
recovered a year. At the 322-store fleet scope: about $7.2M total recovered a year, and
$77.3M of replacement capital deferred (at the 3.9 year extension the age-12 fouling
fraction implies).

## Open decisions
- **Brand.** The real Energy Plus visual identity is not resolved. This version ships on a
  placeholder skin (see DESIGN.md); reskinning is a single-file swap of `assets/brand.css`.
- **Product naming.** Still white-labeled; no product name appears anywhere on the page.
- **VP identity.** Unknown. The page is written to work for facilities, finance, or ESG,
  since each owns one of the three bills, rather than addressing a named title.
- Whose calendar the "Book the 15 minute fit call" button should point to once a specific
  Academy contact is engaged (currently Dan's own booking link).

## Fleet wide, not Texas specific
This page pitches Academy as a big box fleet story, not a Texas story: it covers all 322
stores, not a regional subset. There is no reference anywhere in the page to Texas, Houston,
Katy, ERCOT, "4CP," or "113"; the demand charge is described generically ("the highest
fifteen minutes of the month"), and the pilot is "five stores." The ledger's fleet toggle
covers all 322 stores by default off (one store is the default view).

## Customer-specific strings and where they live
All of the following are specific to Academy Sports + Outdoors and should be revisited if
this page is ever reused as a template for another retailer:
- Header: "Prepared for Academy Sports + Outdoors"
- Hero label, H1, and lead copy (store count, twelve rooftop units per store)
- The roof ledger: `STORES` (322), `KWH_STORE`, `PEAK_KW`, `MAINT_TODAY`, `ROOF_COST`, and
  the fine print citing "Academy's public filings and industry norms for a 70,000 square
  foot big box"
- Bill one's mono note citing Academy's 2021 GHG supplement (94 percent purchased
  electricity)
- Offer section: five-store pilot structure, bottom-quartile (about eighty stores) rollout,
  Academy's twenty to twenty five store a year build-and-remodel cadence
- CTA band: Daniel Gutierrez contact details, booking link with `?f=academy` query param
- Footer: "prepared for Academy Sports + Outdoors"
