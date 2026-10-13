# VisiPack — visual data pack editor

VisiPack is a node-based visual scripting editor for **Minecraft Java Edition 26.3+** data packs (pack format 121.0). Build logic by connecting nodes, check the generated `.mcfunction` code live, and export a `.zip` that goes straight into your world's `datapacks` folder.

Everything runs in the browser, in a single `index.html` with no build step and no server, and it can be installed as an app that works offline.

## Features

- **Events**: on load, every tick, every N ticks, player joins, player dies, right-click with item, advancement triggers, `/trigger` commands, callable functions with macro parameters.
- **Flow**: execute as/at/positioned/rotated/in/on, branches with AND/OR/NOT conditions, loops, raycasts, delays, function calls.
- **Commands**: chat, titles, boss bars, dialogs, summon (with RealisticSize / FrameEditor options), effects, attributes, items, blocks, particles, sounds, game rules, NBT data, scoreboard variables.
- **Recipes** with a crafting-grid editor, **extra files** (predicates, loot tables, tags) with templates.
- Live code panel with line → node mapping, a problems list, undo/redo, comment frames, minimap, light and dark themes.
- Interface in English; node descriptions, field help and tooltips can also be shown in Italian (⋯ menu or Pack settings).

## Publishing on GitHub Pages

1. Put the contents of this folder (`index.html`, `.nojekyll`, `manifest.webmanifest`, `sw.js`, `icons/`) at the root of the repository, or in a `docs/` folder.
2. On GitHub: **Settings → Pages → Build and deployment → Deploy from a branch**, then choose your branch and `/ (root)` or `/docs`.
3. After a minute the editor is live at `https://<user>.github.io/<repository>/`.

## Installing it as an app

The GitHub Pages folder is a Progressive Web App: `manifest.webmanifest`, `sw.js` and `icons/` make it installable and usable offline.

1. Upload **all** these files to the same folder of the repository: `index.html`, `manifest.webmanifest`, `sw.js`, `.nojekyll`, `icons/`.
2. Open the site (it must be the `https://` GitHub Pages address, not a local file).
3. Install it:
   - **Chrome / Edge (desktop and Android)**: the install icon in the address bar, or **⋯ → Install as app** inside VisiPack.
   - **Safari on iPhone / iPad**: Share → **Add to Home Screen**.
   - **Safari on Mac**: File → **Add to Dock**.

The icons in `icons/` are generated from `Logo.png`; the app does not load `Logo.png` itself, so you can keep it in the repository or remove it.

After the first visit the editor also works offline. When you upload a new `index.html`, the app picks it up the next time it is opened online; if you change the icons or the manifest, also raise `VERSION` at the top of `sw.js` (e.g. `visipack-v2`).

Installed app and browser tab share the same saved projects only on Chrome/Edge; on iOS the home-screen app has its own storage, so move projects with **Export project .json**.

## Saving your work

- Projects are saved automatically in the browser you use (local storage). Another browser or device starts empty.
- Use **Projects → Export project .json** for backups or to move a project, and **Import .json** to open it again.
- **Export .zip** creates the data pack: drop the `.zip` into `saves/<world>/datapacks/` (no need to unzip it) and run `/reload`.

## Notes for 26.3

- `pack.mcmeta` uses `min_format` / `max_format` (no `pack_format`).
- Loot conditions and predicates use `"type"` instead of `"condition"`; entity predicate fields are namespaced (`minecraft:entity_type`, `minecraft:flags`…); `block_state_property` was removed.
- Summoned item frames need `block_pos`: VisiPack adds it automatically through a small macro function.
- Game rules use snake_case names (`keep_inventory`, `advance_time`…).
