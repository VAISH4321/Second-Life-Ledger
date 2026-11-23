## Inspiration

When a fridge, laptop or air conditioner breaks, the usual advice is "just buy a new, efficient one." But manufacturing a new device already releases a large amount of CO₂ before it is ever switched on. A typical refrigerator carries roughly 400 kg of embodied carbon. We wondered: is replacing really greener, and if so, when does a new appliance actually repay that carbon debt? People make these decisions every day with no way to see the answer, so we built a tool that shows it.

## What it does

Second Life Ledger is a repair-or-replace calculator that compares carbon over a device's lifetime.

- The user picks a device (refrigerator, air conditioner, washing machine, TV, laptop, smartphone or ceiling fan).
- They enter the repair quote, the price of a new device, how many extra years the repair buys, and their electricity grid (India, US, EU, France or a coal-heavy grid).
- The app plots two cumulative-emissions curves: **repair now and replace later** versus **replace now**.
- It marks the **break-even point** where replacing starts to win, if there is one, and gives a clear verdict: *Repair it* or *Replace it*.
- It reports the kg of CO₂ avoided by following the verdict and the money difference between the two paths.
- A personal **ledger** keeps a running total of CO₂ avoided across all logged decisions.

The tool doesn't just say "always repair." On a clean grid or for small devices, repair wins. For an old, power-hungry appliance on a coal-heavy grid, replacing can win, and the app says so.

**Intended users:** households, students and small repair shops deciding what to do with a failing appliance.

## How we built it

- A single self-contained HTML, CSS and JavaScript file with no dependencies, so it runs offline in any browser.
- **Carbon model:** each device has an embodied carbon value, an annual energy use for the old and a new model, and a typical lifespan. Operational carbon is annual kWh × grid intensity (kg CO₂/kWh).
  - *Replace now* = embodied carbon of the new device + new-device operational carbon × years.
  - *Repair* = small embodied carbon of repair parts (assumed 8% of a new device) + old-device operational carbon for the extra years the repair buys, then the new device's carbon, with its embodied carbon spread over its lifetime.
- Both paths are compared over one new-device lifetime, and the verdict is whichever ends lower.
- The chart is hand-drawn inline SVG that redraws live as sliders move.
- The ledger is stored in the browser's local storage.
- Fonts: Bricolage Grotesque via Google Fonts. The page supports light and dark mode.

## Challenges we ran into

- **Making the comparison fair.** Repairing and replacing give different lifespans, so we had to compare them over the same period and spread the replacement's embodied carbon sensibly.
- **Data quality.** Embodied carbon and power figures vary widely between models and studies. We used rounded typical values, labelled them as estimates, and made them easy to replace with sourced data.
- **Keeping it honest.** It was tempting to make the app always favour repair, since that is the "green" story. We chose to let the numbers decide, so the verdict can flip.
- **Making the chart readable** on small phone screens while still showing the crossing point clearly.

## Accomplishments that we're proud of

- A working prototype that turns an abstract idea (embodied vs operational carbon) into one clear chart and verdict.
- A tool that gives different answers for different devices and grids, instead of a one-size-fits-all message.
- It runs entirely in the browser with no sign-up, no server and no data collection.
- It shows both the carbon and the money impact, which is what actually drives household decisions.

## What we learned

- For small devices such as phones and laptops, embodied carbon dominates, so repair almost always wins.
- For large, power-hungry appliances, the electricity grid matters as much as the device: the same AC can be a "repair" on a clean grid and a "replace" on a coal-heavy one.
- Even simple models become more convincing when their assumptions and limitations are stated openly.
- Sustainability tools work best when they help people choose between real options, not just raise awareness.

## What's next for Second Life Ledger

- Replace our rounded figures with sourced, model-specific lifecycle data, and cite the sources.
- Pull real efficiency data from energy-label databases such as the BEE star rating.
- Add a local repair-shop and repair-café finder.
- Add a shared community or campus dashboard of CO₂ avoided.
- Include recycling credits and end-of-life impacts of the discarded device.
- Model changing grid intensity over time as grids get cleaner.
- Estimate impact at scale: *if 1,000 households followed the verdicts, about X tonnes of CO₂ would be avoided* (to be filled in with a calculation we can defend).

### Built with

HTML, CSS, JavaScript, SVG, Google Fonts

### Limitations

Figures are typical averages, not model-specific. The model assumes constant grid intensity and usage, assumes repair parts carry 8% of a new device's embodied carbon, uses a flat ₹8/kWh electricity cost, and does not include recycling credits.
