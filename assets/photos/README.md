# Photos

This folder holds image assets referenced by `index.html`.

Until Andrew exports and renames specific shots, the site renders styled placeholder rectangles in each photo slot. The slots and their expected aspect ratios:

| Window | Slot | Aspect | Suggested content |
|---|---|---|---|
| About | portrait | 3:4 | Andrew, head-and-shoulders or candid |
| Homestead | landscape | 4:3 | the property, animals, family |
| The Bus | wide | 16:9 | the converted school bus |

To wire a real photo, replace the corresponding `<div class="photo …" role="img" …>` with an `<img>`:

```html
<img class="photo--portrait" src="assets/photos/andrew-portrait.jpg" alt="Andrew, …" loading="lazy">
```

Keep file sizes modest. JPG for photos, web-sized (around 1200px on the long edge is plenty). HEIC files in this directory are originals and should be converted before wiring.
