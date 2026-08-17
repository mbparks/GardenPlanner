# Garden Planner

A square foot garden planner that runs from one HTML file. No build step, no
server, no account. Double click it and it works, on disk, offline, forever.

Version 2.5.0 :: GPL-3.0

## What it does

**Plot.** Arrange beds on a grid you control. Add rows and columns, drop beds
into any slot, name and size them, move them by drag or by keyboard, and leave
slots open for paths and compost. It opens on a six bed L around an open center,
which is a starting point and not a rule.

**Three ways to read the map.** Today is the live garden. One day is any date you
scrub to. Whole season drops the date entirely: every square shows its first crop
of the year with a count for what follows, and warnings cover anything that
overlaps at any point in the year. Give a layout a future year and the app treats
it as a plan, so This week becomes the season ahead in order and nothing in it is
ever late. That is the mode for laying out next year in February.

**Season.** A square is not a slot holding one plant forever. It holds a sequence
of plantings with dates, so the same foot of ground is radishes in April and
beans in June. A scrubber sets the day, and everything the planner says is said
about that day. Click any square with nothing selected and it tells you what has
held it, and what still fits before the frost, including later sowings than the
book's date where the gap allows one. Containers work the same way.

**Zone.** Zones 3a to 11b, or your own frost dates, which matter more, or the
frost dates read straight off a weather log you already have: a CSV of dates and
daily minimums, worked out on your machine, averaged or taken from the hardest
year. Any planting also takes a variety name and the days to maturity from the
packet, which sets its window instead of the library figure. The plant
library holds researched Zone 7a timing and every other zone is that timing
re-projected onto your dates, each endpoint moving with whichever frost it sits
closer to. Spring sowing follows the last frost, autumn sowing and late harvest
follow the first.

**Checks.** Companions and conflicts read both ways, with neighbours flagged
harder than bed mates. Footprints, so a squash holds four squares. Shade, since
north is up and a tall crop shades what is behind it. Rotation across years by
plant family. Season fit, so a window squeezed to a sliver gets said out loud. Shade
from the bed to the south as well as inside a bed.
Soil volume in cubic feet of Mel's Mix, split in thirds.

**This week.** What is due, read off the plantings you already made: start these
indoors Saturday, sow radish in NW row 3, picking opens on the peas. Anything
behind is called out separately, and a button writes the date straight into the
journal so recording work takes one tap with dirt on your hands.

**Seeds.** Squares times plants per square, divided by how likely the packet is
to come up, minus what is already in the box. Tell it what you have and the year
you bought it and it asks you to buy only the difference. Garlic is ordered as
cloves, potatoes as seed potatoes, strawberries as crowns.

**Bed by bed.** A strip per square across the year, so the gaps a succession
sowing should fill are visible at a glance instead of one square at a time.
Click any square to open it in the planner.

**Harvest load.** Pounds ripening each week against what the household eats
fresh. Thirty-two tomato plants arriving in the same three weeks gets flagged in
February, and so does an August with nothing in it.

**Roll a year forward.** Copies the open layout into next year and moves each
bed's crops to whichever bed of the same size has gone longest without that
family. The rotation checker does the work instead of only complaining.

**Record.** The Journal holds what actually happened against what was planned:
sown, up, planted out, first pick, last pick, yield, outcome, a photo reference,
and why you think so. Beds and pots both. Export the season as CSV.

**Farm.** One farm, one plant library, one set of frost dates, any number of
layouts. Use them for separate sites, for this year against next, or for two ways
of arranging the same ground.

## Files and data

Nothing leaves the browser. Save writes the whole farm to a JSON file named after
it, Load reads it back, and where the browser supports it Save writes back to the
same file. A working copy is kept in the browser as a convenience and is never
load bearing. Imported files are checked field by field, unknown plant ids are
dropped and reported, and every string is rendered as text.

Files from v1.0 through v1.2 load and migrate: beds become one layout, plain
squares become plantings holding their normal window.

## Keyboard

Tab to a square, arrows to move within a bed, Enter or Space to plant, Delete to
lift, Escape to stop painting or close the inspector. Ctrl+Z undo, Ctrl+Shift+Z
redo, Ctrl+S save. Square brackets step the day, shift with them steps a week.
Drag across squares to paint a run. Nothing needs a mouse.

## Bench checks

The About tab runs 73 assertions on demand, covering the plant data, the season
model, footprints, shade, rotation, the zone projection, import validation and
the migration paths. Run it after any edit.

## Known limitations

- One planting at a time per square. Interplanting two crops in one square on one
  day is not modelled, though a plant covering several squares is.
- Custom plants carry no companion data and are never flagged.
- Timing is Zone 7a research shifted onto your frost dates. It knows nothing
  about your day length, soil temperature, or which varieties you grow.
- Zone frost dates are averages across a wide band of country. Set your own.
- Perennial hardiness is not checked, so it will let you plant rosemary in Zone 4
  without comment.
- Shade is judged inside a bed and from the bed directly to its south. No fence,
  no walnut tree, no garage.
- Days to maturity are the packet's number, taken at face value. Nothing adjusts
  them for a cold spring.
- A weather log is read for freezing days only. It does not become a growing
  degree day model.
- Journal photos are references, not copies. Move or rename the picture and the
  reference goes stale.
- Rotation only sees layouts you gave a year to, and only matches on bed id, so
  renaming a bed loses its history.
- Rolling forward only swaps beds of identical size. A bed with no twin stays
  put and says so.
- Yields are ballpark pounds per square foot and seed viability is the usual rule
  of thumb for how long each kind keeps. Neither is a measurement.
- Companion pairings are mostly tradition. The ones measured in trials are marked
  documented and can be filtered down to.
- No service worker, because a browser will not register one from a file on disk.
  The manifest is there, so it installs to a home screen when served, and it works
  offline either way by being one file you already have.

## Plant marks

Every plant is drawn here as inline SVG, tinted with its own colour, from a small
vocabulary of forms: leaf, sprig, head, taproot, round root, bulb, round fruit,
long fruit, gourd, pod, stalk, disc flower, spike flower, berry, tuber, stalks.
Original work, about 4 kB of markup, no external files.

This replaced emoji because emoji could not do the job. Unicode has no pumpkin or
squash character at all, only U+1F383 JACK-O-LANTERN, which every platform draws
with a carved face. Pea, radish and beet were coloured circles. Oregano was a
jar, zucchini a potted plant, borage and lavender were hearts. The emoji set is
still there behind a switch on the Farm tab, which shows both sets side by side
so you can see what you are choosing between.

## Contrast

All three themes are checked against WCAG AA: 4.5 to 1 for text, 3 to 1 for the
borders of anything you operate. Decorative dividers and operable borders use
separate tokens so the second can be strong without making the page heavy.

## Still open

Interplanting two crops in one square on one day. Growing degree days from the
weather log rather than freeze dates alone. Per variety timing held in the
library instead of on each planting. A cold frame or tunnel as a property of a
bed, which is the honest way to extend the season rather than fudging the frost
dates.

Make. Hack. Learn. Share. Repeat.
