# PharmD Plus Brand Guide

This file records the colors and typography used by the PharmD Plus storefront PoC.

## Brand colors

| Name | Hex | RGB | Usage |
|---|---|---|---|
| PharmD Green | `#3DC95B` | `61, 201, 91` | Primary brand accent, LINE-style actions, success states |
| PharmD Blue | `#2196E5` | `33, 150, 229` | Product actions, links, and hero gradient |
| PharmD Navy | `#153F90` | `21, 63, 144` | Primary buttons, dark sections, and strong emphasis |
| PharmD Pink | `#FF008A` | `255, 0, 138` | Small highlights, notifications, and badges |
| Ink | `#272B30` | `39, 43, 48` | Headings and high-emphasis content |

`#3DC95B` is taken from the public PharmD Plus website. The site uses `#1C1C1C`, but the storefront uses the softer `#272B30` for high-emphasis text. The blue, navy, and pink supporting colors are matched to the official logo asset.

## Interface colors

| Name | Hex | Usage |
|---|---|---|
| Page background | `#F7FBFF` | Main application background |
| Card | `#FFFFFF` | Product cards, dialogs, and admin panels |
| Muted text | `#62676C` | Supporting copy and metadata |
| Light green | `#DFF8E4` | Pills, tags, and subtle green backgrounds |
| Border | `#DCE6EE` | Dividers, fields, and card borders |
| Danger | `#C53C49` | Destructive admin actions and errors |
| Light blue | `#E7F4FD` | Product artwork background |
| Light pink | `#FCE5F2` | Product artwork background |

## CSS variables

```css
:root {
  --ink: #272b30;
  --muted: #62676c;
  --cream: #f7fbff;
  --card: #ffffff;
  --green: #3dc95b;
  --lime: #dff8e4;
  --blue: #2196e5;
  --navy: #153f90;
  --pink: #ff008a;
  --line: #dce6ee;
  --danger: #c53c49;
}
```

## Typography

### Primary typeface

Use **Noto Sans Thai** throughout the PharmD Plus application. It supports both Thai and Latin content and is available through Google Fonts.

```css
font-family: "Noto Sans Thai", ui-sans-serif, system-ui, sans-serif;
```

Load the required weights with:

```html
<link
  href="https://fonts.googleapis.com/css2?family=Noto+Sans+Thai:wght@400;500;600;700;800&display=swap"
  rel="stylesheet"
/>
```

Use weight `400` for body copy, `500–600` for interface controls, and `700–800` for headings and strong emphasis. Avoid introducing additional typefaces without updating this guide.

## Logo

The official transparent logo is stored at:

```text
assets/pharmdplus-logo.png
```

Keep its aspect ratio, do not recolor it, and leave clear space around the mark. Use a white or very light background whenever possible.
