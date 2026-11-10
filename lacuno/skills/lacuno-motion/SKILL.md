---
name: lacuno-motion
description: Add motion to a Lacuno site - entrance animations, scroll-driven animations, parallax, a pinned scroll story, a video that follows the scroll, a reading progress bar or custom keyframes. Use when the user asks for animation, movement, scroll effects, an Apple-style product story or anything that should fade, slide or scale on a Lacuno page.
---

# Motion in Lacuno

Motion is CSS on classes: `style.set` of the custom properties below, with raw values (`{"type":"raw","value":"…"}`). It needs no script.

## Method

1. Call `sites.list` and pass `site` on every later call (a self-hosted, per-site connection has neither). `page.outline` shows the page's elements with their classes.
2. Set the properties on the element's class in one `style.set`, a list of changes, passing the revision you read as `expectedRevision`. An element without a class of its own gets one first (`class.create`, then `node.update`).
3. Check the page as the lacuno-check-your-work skill describes. The canvas and `page.screenshot` show the page at rest; the person presses Preview motion on the canvas to see it move. Say so.

## Entrance and scroll

- `--lc-entrance` plays once when the element scrolls into view; `--lc-scroll` follows the scrollbar. Set one, not both (scroll wins).
- Names: lc-fade, lc-slide-up, lc-slide-down, lc-slide-left, lc-slide-right, lc-scale-up, lc-blur-in (enter or scroll); lc-fade-out, lc-parallax, lc-fade-through, lc-progress (scroll only). Or the id of custom keyframes.
- `--lc-duration` (400ms), `--lc-delay` and `--lc-easing` time entrances and every change a state makes (hover, focus, open…) to opacity, scale, rotate, translate, transform, box-shadow and colours; `--lc-duration` 0s makes those changes instant. Scroll motion is linear.
- `--lc-range`, scroll only: entry (while entering, the default outside a story), cover (while visible), exit (while leaving), or any animation-range value. lc-fade-out wants exit, lc-parallax cover. lc-parallax moves the element up, faster than the page; `--lc-parallax` is its distance each way, 80px by default.
- `--lc-scroll` none on a smaller breakpoint turns it off there.
- The page must read well at rest. Reduced motion and browsers without scroll timelines show every element as styled, and a story flows like any section. Reduced motion also stops a class's own animation. Every name has the element as styled as one of its frames.

## Scroll story

The Apple-style product page: a pinned stage, steps in turn.

- A section with attrs `{"data-lc-story":{"type":"static","value":true}}`. Its first child is the stage: display grid, grid-template-rows minmax(0, max-content) auto, align-content and place-items center. It pins for the story's length.
- In the stage: the pinned image with `--lc-scroll` lc-scale-up, `--lc-range` entry and max-height 100%, then one child per step (a heading and a paragraph) with `--lc-scroll` lc-fade-through and no `--lc-range`. The picture takes the first row, the steps share the second.
- A step is a direct child of the stage with `--lc-scroll` on the base breakpoint and no `--lc-range`; steps take turns in order. Add, remove or move them freely. Anything else in the story that follows the scroll runs while the stage is pinned, unless its `--lc-range` says otherwise, like the picture's entry: a progress line in the stage needs its own `--lc-range`, or it counts as a step.
- Length: `--lc-length` on the section, a number of screens without a unit (steps + 1 by default). No overflow hidden on the section or its ancestors (clip is fine).

## Scroll video

The pinned element of a story is a video, `src` an asset binding, with attrs `{"data-lc-scrub":{"type":"static","value":true}}`. Its time follows the story; it never plays, and is published muted, without controls, autoplay or loop. Outside a story the attr is ignored.

- It needs a keyframe on every frame or it scrubs in jumps. Where the person's machine has ffmpeg, prepare the clip there, then add it with `asset.upload`:
  `ffmpeg -i in.mov -an -vf "scale=1280:-2,fps=24" -c:v libx264 -g 1 -crf 26 -pix_fmt yuv420p -movflags +faststart out.mp4`
- Uploads are at most 10 MB, about 15 to 20 s at 1280 px: shorter is better; raise `-crf` if it is too big.

## Reading progress bar

An empty span with `--lc-scroll` lc-progress, `--lc-timeline` scroll(), `--lc-range` normal, position fixed, inset 0 0 auto 0, height 3px, transform-origin left and a background.

## Custom keyframes

- `keyframes.create` with `{"id":"rise","stops":[{"at":0,"styles":{"opacity":"0","translate":"0 40px"}},{"at":60,"styles":{"translate":"0 -4px"}}]}`, before the `style.set` of `--lc-entrance` or `--lc-scroll` rise.
- Styles are CSS text keyed by kebab-case property; a token is `var(--color-brand)`. Leave out the first or last stop to mean "as styled", so the element as styled stays a frame; a stop left out in between is interpolated.
- Ids are lower-case idents, not lc-* or none, fixed once created. `keyframes.update` replaces the stops; `keyframes.delete` is refused while a style names them.

## Reference

`style.set` and the keyframes tools declare their own fields. The editor's palette has Scroll story, Scroll video and Reading progress for the person to insert by hand. The method and rules above come from this skill.
