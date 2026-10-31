# SVG Paint Order Lab

A small reproducible fixture for reviewing SVG export code. Use the two deliberately broken files as regression examples when document order is accidentally replaced by color sorting.

An offline exercise for designers and developers: a two-color illustration can require three ordered passes. Merging identical colors changes which shapes cover which others.

## Run it

Download this repository, open **lab.html** in a current browser, and click **Compare rendered pixels**. No install, account, network access or product subscription is required. The lab does not accept arbitrary SVG uploads.

The four original SVG files in `examples/` can also be opened directly in a browser or vector editor. The lab contains these examples itself, so the HTML file works on its own.

| Example | Shape order | What to look for |
|---|---|---|
| Original | White background → teal tag → white detail | Small white circle visible on the tag |
| White first | White background → white detail → teal tag | Detail disappears |
| White last | Teal tag → white background → white detail | Tag disappears |
| Ordered passes | Three groups in the original sequence | Original appearance retained |

The compare button decodes all four SVGs, renders each at 300 × 180 pixels using the current browser, and counts differing RGBA pixels. RGB is ignored where alpha is zero in both renderings. Results describe that renderer and size; they do not establish universal vector equivalence, print readiness or cutter safety.

## A useful handoff checklist

1. Preserve the original viewBox, dimensions and origin.
2. Distinguish white paint from transparent space; this example uses white paint.
3. Keep document order when splitting consecutive groups.
4. Reassemble passes in order on the original canvas.
5. Compare the rendered result before handing it to another application.

There is no rule that every repeated color always needs a separate pass: non-overlapping shapes can sometimes be combined safely. That requires checking geometry and intervening artwork. This lab deliberately does not implement such optimization, arbitrary SVG parsing, gradients, clipping or manufacturing output.

## Why this works

For these ordinary shapes, later elements paint over earlier elements. See the [W3C SVG rendering-order model](https://www.w3.org/TR/SVG2/render.html#RenderingOrder). Moving both white shapes to one side of the teal shape cannot preserve this fixture's appearance.

## Optional practical tool and disclosure

For supported simple solid-fill artwork, [Pic2SVG's Split SVG by Color](https://pic2svg.com/split-svg-by-color/) exports consecutive color passes while retaining the canvas. It is a separate service with its own limits. This repository was prepared on behalf of Pic2SVG. The link is optional; the complete exercise works without visiting that site.

## License

The original tutorial, HTML and SVG examples here are MIT licensed. This does not license Pic2SVG's service, third-party artwork or outputs from that service. There is no telemetry or external script dependency. The external references are ordinary links and are opened only if you choose them.
