# Quest gallery contract

The default guide is an explorable knowledge gallery, not a long article. Adapt `../assets/gallery-guide.html`; retain its interaction and accessibility behavior while replacing sample content. Use the user's language for all labels.

## First screen: quest and cards

- Start with the user's current quest as the main heading and a one-sentence immediate goal. Make the task more prominent than the brand slogan. Include N2T's core phrase once in the footer.
- Group cards by task-specific priority: **Essential now**, **Useful next**, and **Can wait**. Explain each group in one short sentence. Omit empty groups; do not invent topics to fill a grid.
- Each card represents one concept: a meaningful visual cover, title, one-line explanation, and a few useful topic or media labels. Cards are not miniature articles. Do not use unrelated stock imagery.
- Rank by what the user needs to take their next action. Prerequisites precede dependent concepts. Later topics remain visually secondary.
- Use a responsive Notion-like gallery: consistent cover ratios and spacing, restrained borders, readable titles, 3–4 columns on wide screens and fewer as space narrows. Neutral dark surfaces are a suitable default; user preferences take precedence.

## Card detail: modal

Selecting a card opens its detail on the same page:

1. The concept name and why it matters for this quest.
2. A short explanation (usually 2–4 sentences), a concrete example or original diagram, and only the terms or common mistakes needed to understand it.
3. **References for this concept**: images or diagrams, video links, and real websites alongside the explanation. Each reference has a title, source, what to look at, and verification limits where relevant.
4. One small action or decision the user can now make.

Favor visuals, captions, short paragraphs, and a few bullets over extensive prose. Include all useful media types when research supports them. Never fabricate a screenshot, video, URL, or verification status to fill a slot. Remove unused template slots, but do not treat this as permission to skip visual-reference research. When no researched reference image can be displayed, explain the actual reason in the guide and delivery message. Do not move the references into a separate page-long resource list.

## Reference media

- Display reference images inside the modal when reuse and attribution permit, with alt text, caption, and source link. Otherwise link to the source page. Preserve an understandable text fallback if remote images fail.
- A link to a website is not an embedded reference image. Use an actual verified image resource in an `img` element (or permitted inline content), with a source link beside it. Verify `complete && naturalWidth > 0` after opening the modal. A successful page fetch alone is insufficient. Do not claim that link-only references are visible images. If images are unavailable, label the gap rather than substituting generic diagrams without explanation.
- Add `data-reference-image` to embedded reference images to use the template's load-failure handler. Localize the `data-fallback` message. Keep the caption and source link outside the image so they remain visible after a failed load. The handler runs on cloned modal content too.
- Original SVG diagrams can be covers and explanatory images. Label them as illustrations, never real product screenshots.
- Present videos as link cards with creator and a reason to watch. Only use verified thumbnails and timestamps. Do not autoplay or assume embedded players work; retain a usable link.
- Include only confirmed free-to-watch full videos. Omit paid courses, subscription/membership videos, rentals, purchases, trial-only access, and paid-lesson previews. If free access cannot be verified, omit that video; a warning beside a paid link is not a substitute.
- Website cards link to the inspected destination and explain its relevance. Place citations near the claims they support and record the research date where freshness matters.
- Sample template content is fictional layout material, never evidence.

The template's original SVG covers are layout examples, not a complete reference section. Add researched images to the relevant detail articles using the commented image pattern in the template. Replace every placeholder attribute with verified content; do not ship the commented pattern or placeholder URLs as a reference.

## Interaction and portability

- Complete HTML document with language, UTF-8, viewport, semantic headings, and inline CSS/JavaScript. The core UI needs no network.
- Keyboard-accessible cards and a native `dialog.showModal()` with a visible heading as its accessible name. Support a close button, Escape, backdrop dismissal, and focus restoration to the originating card. Lock background scroll while allowing modal content to scroll.
- Readable contrast, visible focus, meaningful link text, touch targets around 44px, reduced-motion support, and priority labels that do not depend solely on color.
- A single column and near-full-width modal on small screens. No horizontal overflow; keep the close control reachable.
- Static detail sections for no-script use and print. Hide them in enhanced gallery mode; do not force all explanations onto the normal interactive page.
- Escape researched text and use safe DOM APIs for dynamic text. Only HTTP(S) external references, local assets, and internal anchors. No remote scripts or event handlers copied from sources. New-tab links need `rel="noopener noreferrer"`.

## Final review

Check quest relevance, priorities, and concept-reference associations. Count researched reference images separately from original illustrations and text links. Open their modals and confirm each image is visible with decoded dimensions, not just present in HTML. A zero-image result needs renewed research or an explicit, supported explanation of why images could not be included. Replace every example and preview notice. Test every card, close button, Escape, backdrop, keyboard activation, and focus restoration. Inspect wide/narrow layouts, long modal content, image failure, no-script fallback, and print readability. Report checks that could not be performed.
