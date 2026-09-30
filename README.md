# DigitalSigns

Artwork and schedule for the XIAO 7.5" ePaper door sign. The sign fetches these
files straight from `raw.githubusercontent.com/ThaDewey/DigitalSigns/main/`, so
pushing a change here is all it takes. The board never needs re-flashing.

This repo is public on purpose: raw links only work without a token on a public
repo. Anyone with the URL can see the images and the schedule.

The firmware lives in the private repo `DigitalSignage_ePaperPanel_XIAO-7-5-`,
which includes this repo as its `sign/` submodule.

## Files

| File | Purpose |
|---|---|
| `schedule.txt` | Which image shows when. Re-read on every wake |
| `door-sign-*.bmp` | The images the sign can show |
| `door-sign-design-sheet.png` | Design reference only. The sign never loads it |
| `gone-for-day.bmp` | Older placeholder image |
| `schedule.starter.txt`, `schedule.dropbox.example.txt` | Examples. The sign ignores them |

Files must sit at the **root** of the repo, not in a subfolder.

## Changing an image

Replace the `.bmp` with one of the **same filename** and push. The URL stays the
same, so `schedule.txt` needs no edit. Press Reset on the sign to see it
straight away, or wait for its next wake.

Images must be **800×480, 1-bit, uncompressed BMP** (about 48 KB). In Photoshop:
Grayscale, then Bitmap (50% Threshold for type, Diffusion Dither for photos),
then Save As BMP with **Windows** format, **1 bit**, and **Compress (RLE)
unticked**. Anything else is rejected on the panel.

## Changing the schedule

One rule per line: `DAYS START-END filename.bmp`

```
MON,WED 12:00-15:00  door-sign-office-hours.bmp
MON,WED 15:00-18:00  door-sign-teaching-class.bmp
ALL     00:00-24:00  door-sign-default.bmp
```

- `DAYS`: `MON`..`SUN`, a comma list, or `WEEKDAY` / `WEEKEND` / `ALL`
- Times are 24-hour, in the sign's local time. `00:00-24:00` is the whole day,
  and a range may wrap midnight (`17:00-08:00`)
- The **first matching line wins**, so put specific rules first
- Keep an `ALL 00:00-24:00` line **last** so there is never a gap
- `#` starts a comment

To add a new design, add the `.bmp` and a `schedule.txt` line that uses its bare
filename, then push both.

## After pushing

If you pushed from inside `sign/` in the firmware repo, you can also run
`git add sign && git commit` in the outer repo to update its recorded submodule
commit. The sign works either way.
