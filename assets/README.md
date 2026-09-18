# Nocrew — /assets

Drop your real files in here. Paths below match exactly what `index.html`
references. Nothing else needs editing to swap media — filenames are the contract.

Everything ships as placeholders right now:
- The three films you gave me (Nothing Ear, Nothing Phone, Superyou) are already
  in place as real `.mp4`s.
- The other three tiles and the hero use generated `.svg` poster placeholders and
  reference `.mp4` paths that don't exist yet — the tiles will show the poster and
  simply won't play until you add the video.

--------------------------------------------------------------------------------
## Folder structure
--------------------------------------------------------------------------------

assets/
├─ logo/
│  ├─ nocrew-logo.png         Full square lockup (NC monogram + "NO CREW")
│  ├─ nocrew-mark.png         NC monogram only — used in the nav + footer
│  └─ favicon-64.png          Browser-tab icon
├─ hero/
│  ├─ hero-poster.svg         Placeholder poster shown before/without the showreel
│  └─ showreel.mp4            ← YOU ADD. Hero background film.
├─ work/                      (all tiles are 9:16 · poster = real 1st frame for
│  │                           delivered films, .svg placeholder otherwise)
│  ├─ nothing-ear.mp4  + .jpg poster    ✓ in place, plays
│  ├─ nothing-phone.mp4 + .jpg poster   ✓ in place, plays
│  ├─ rayban-meta.mp4  + .jpg poster    ✓ in place, plays (from Meta.mov)
│  ├─ redbull.mp4      + .jpg poster    ✓ in place, plays
│  ├─ superyou.mp4     + .jpg poster    ✓ in place, plays
│  ├─ starbucks.svg    (placeholder)    starbucks.mp4   ← YOU ADD (9:16)
│  └─ comet-uno.svg    (placeholder)    comet-uno.mp4   ← YOU ADD (9:16)
└─ og/
   └─ og-image.svg            Placeholder social-share image (see note on PNG)

--------------------------------------------------------------------------------
## What to add and at what dimensions
--------------------------------------------------------------------------------

### Hero showreel — assets/hero/showreel.mp4
- 1920×1080 (16:9), H.264 MP4, muted, seamless loop.
- Keep it short (10–20s) and light (aim < 6 MB). It autoplays on mobile data.
- OPTIONAL but recommended: export a real still and replace hero-poster.svg with
  hero-poster.jpg (1920×1080), then update the `poster=` attr in index.html.

### Work films — assets/work/<slug>.mp4  (ALL 9:16 portrait now)
The grid is a uniform wall of 9:16 tiles. Each tile shows a poster + a play button;
clicking plays the film inline WITH sound, using native controls. Only one plays at
a time; scrolling a playing tile offscreen pauses it.

| Tile          | File              | Status                              |
|---------------|-------------------|-------------------------------------|
| Nothing Ear   | nothing-ear.mp4   | ✓ in place                          |
| Nothing Phone | nothing-phone.mp4 | ✓ in place                          |
| Ray-Ban Meta  | rayban-meta.mp4   | ✓ in place (copied from Meta.mov)   |
| Red Bull      | redbull.mp4       | ✓ in place                          |
| Superyou      | superyou.mp4      | ✓ in place                          |
| Starbucks     | starbucks.mp4     | ← YOU ADD, 9:16 (1080×1920)         |
| Comet Uno     | comet-uno.mp4     | ← YOU ADD, 9:16 (1080×1920)         |

- MP4 / H.264 + AAC, 9:16. To add a film: drop `<slug>.mp4` in, then in `CONFIG.work`
  flip that entry's `hasVideo` to `true`. Keep clips reasonably light where you can.
- To ADD A NEW BRAND: add an object to `CONFIG.work` with brand/format/hasVideo/
  poster/src and drop the matching files in — the tile renders automatically.

### Poster frames
Delivered films use a real first-frame `.jpg` (auto-extracted). When you add a new
film, generate its poster with one command (no extra tools needed):

    qlmanage -t -s 1080 -o . yourfilm.mp4 && sips -s format jpeg yourfilm.mp4.png --out yourfilm.jpg && rm yourfilm.mp4.png

then point that entry's `poster:` at `assets/work/yourfilm.jpg`. Placeholder tiles
keep their branded `.svg` until you do.

### Social share image — assets/og/og-image.png
- Export a 1200×630 PNG and save as og/og-image.png (the meta tags already point at
  `.png`). The `.svg` here is only a design reference — most social scrapers won't
  render an SVG OG image, so a PNG/JPG is required for link previews to work.

--------------------------------------------------------------------------------
## Note on the logo
--------------------------------------------------------------------------------
Your NC monogram is now the wordmark in the nav (30px) and footer (40px), and the
favicon. The source art is white-on-black, so the markup uses `mix-blend-mode:
screen` to drop the black — only the white NC shows, cleanly over the dark nav or
bright hero footage. `nocrew-mark.png` was cropped from the full lockup; swap in a
transparent-background version any time and it'll still look right.
