# Clinical benchmarking

The front door to the MedLabIQ practice benchmark. A practice picks the markers it orders and sets a low and a high for each patient group it serves, starting from ranges Quest and Labcorp publish. It saves the result as a versioned file, and opens that file again later to amend single markers.

## What's here

| File | What it is |
|---|---|
| `index.html` | The form. One page, no build step |
| `data.json` | Marker names, units, lab-published ranges and codes, and the default ranges, each with the lab text it came from |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are |

## Where the data comes from

`data.json` is built in the MedLabIQ brain and pushed here by its `publish benchmark data` workflow. Don't edit it by hand, because the next push overwrites it. This repo never reads the brain, and the brain's gate refuses to publish a file that carries a rule, a conflict or the brain's own ranges.

Everything in it is public already: marker names and the ranges and codes each lab publishes.

## What the form does

- A row opens on its default: the practice's primary lab's range for that group, or the other lab's where the primary lab has none.
- A high can't be set below its low, and a low can't be set above its high. Either side can be left blank to leave it open.
- Each row also has optional settings: optimal range, severity outside optimal and outside the range, critical values, action on flag, recheck interval and trend alert. The optimal and critical pairs can't cross either, and a critical value inside the range blocks saving.
- Every input is a number, a dropdown, a checkbox or a date. There's no free text.
- Saving downloads a file. Nothing a practice enters is sent anywhere.

## Publishing

In this repo's settings, under Pages, set the source to deploy from the `main` branch, root folder.

For the brain to push data here, add a deploy key with write access in this repo's settings, and put its private half in the brain repo's `BENCHMARK_DEPLOY_KEY` secret.
