# Fresh Pasta Delights theme refresh

## Branch and safety

- Locked live-theme baseline: `a1bcb9c`
- Development branch: `feature/matthew-theme-refresh-2026-07`
- Store: `pasta-delights.myshopify.com`
- Live theme at the time of the baseline sync: `FPD | LIVE (11/07/2025)` (`151320461469`)
- This branch must be previewed on a development or unpublished theme. It must not be pushed to the live theme without Collin's explicit approval.

## Design direction

The refresh extends the strongest part of the existing store—the custom product and collection experience—across the legacy header, navigation, page background, value banner, and footer.

- Warm cream, low-contrast Italian plaster background
- Tomato red and Italian green from the Fresh Pasta Delights identity
- Warm gold used as a restrained accent
- Dark brown typography with WCAG-compliant contrast
- Lora headings and Montserrat body/navigation copy
- Larger, bolder navigation for the store's older-skewing audience
- Distinct current-page states and a desktop sticky navigation
- Clear shipping and Dallas pickup messages with relevant icons
- Food-specific value icons instead of generic stars
- A new built-in fork-and-pasta favicon

The default palette's tested contrast ratios are:

| Pair | Ratio |
| --- | ---: |
| Body text on cream | 7.61:1 |
| Headings on cream | 13.26:1 |
| Green on light surface | 6.52:1 |
| Red on light surface | 5.79:1 |
| Light text on green | 6.52:1 |
| White text on red | 5.88:1 |

## Theme Editor map

### Theme settings → FPD design system

This is Matthew's primary global design panel.

- Tomato red, Italian green, and warm gold
- Card/panel background and border colors
- Smooth, Italian paper, or soft plaster page texture
- Texture strength
- Card and button corner radius
- Card shadow strength
- Maximum content width
- Keyboard focus-ring width

### Theme settings → Colors

These remain available for legacy Symmetry components.

- Body text, links, and headings
- Buttons
- Header and navigation surfaces
- Shipping/pickup message band
- Product overlays and quick-buy
- Footer

The branch updates the current values to the new Italian palette, removing the old blue/navy presentation.

### Theme settings → Typography

The existing font selectors now also control the custom product and collection layouts. The branch starts with:

- Base: Montserrat
- Headings and store title: Lora
- Navigation and buttons: Montserrat

### Header section

- Menu selection
- Sticky desktop navigation toggle
- Desktop menu size, weight, spacing, and current-page treatment
- Logo image
- Separate desktop and mobile logo widths
- Shipping/pickup messages as editable blocks
- Delivery, storefront, location, or no icon per message
- Existing account, social, newsletter, and mobile notice controls

### Cross-page promos section

- Page visibility
- Open/divided, card, or minimal layout
- Background, text, accent, icon-circle, and icon colors
- Icon size, heading size, and section spacing
- Image or icon blocks
- Pasta fork, ravioli, wheat, chef hat, and legacy utility icons
- Editable heading, supporting copy, and destination link per block

### Collection template section

- Products per page
- Show/hide category navigation
- Accessible navigation label
- Optional Shopify navigation menu

For a fully editable category structure, select a Shopify menu whose top-level items are category-group headings and whose nested items link to collections. If no menu is selected, the existing pasta category list remains as a fallback.

## Implementation notes

- Global brand tokens are emitted once and consumed by the legacy theme plus the custom product and collection templates.
- The product and collection layouts no longer import or hard-code their own brand fonts and core palette.
- The current product purchase layout and add-to-cart placement were intentionally preserved.
- The current shipping/pickup placement was preserved but made clearer and visible on mobile.
- Navigation uses a lightweight desktop-only fixed-state controller so it remains visible beyond the header's containing section. The mobile drawer behavior remains unchanged.
- Current navigation links expose `aria-current="page"`.
- The document language, skip-to-content link, keyboard focus treatment, reduced-motion behavior, and primary content landmark were improved.
- The legacy favicon's image-orientation ambiguity is avoided by the new theme-owned SVG favicon. Matthew can disable it and upload a custom square image.

## Validation

- `config/settings_schema.json`: valid JSON
- `config/settings_data.json`: valid JSON after its Shopify-generated comment
- `git diff --check`: clean
- Shopify Theme Check executes successfully against the theme.

The baseline is Symmetry 3.1.0 and already contains substantial legacy Theme Check debt: parser-blocking scripts, deprecated Liquid tags/filters, missing image dimensions in untouched components, and a syntax false-positive in `assets/theme.js.liquid`. Those issues predate this branch. This refresh does not change dependency ordering or attempt a risky framework migration.

## Official Shopify references

- [Theme editor architecture](https://shopify.dev/docs/storefronts/themes/tools/online-editor)
- [Theme settings schema](https://shopify.dev/docs/storefronts/themes/architecture/config/settings-schema-json)
- [Input settings](https://shopify.dev/docs/storefronts/themes/architecture/settings/input-settings)
- [Color-system guidance](https://shopify.dev/docs/storefronts/themes/best-practices/design/color-system)
- [Theme accessibility guidance](https://shopify.dev/docs/storefronts/themes/best-practices/accessibility)
- [Shopify CLI theme development](https://shopify.dev/docs/api/shopify-cli/theme/theme-dev)
- [Theme Check](https://shopify.dev/docs/storefronts/themes/tools/theme-check)

## Laptop preview workflow

From the laptop's existing clone:

```bash
git fetch origin
git switch feature/matthew-theme-refresh-2026-07
git pull --ff-only origin feature/matthew-theme-refresh-2026-07
shopify theme dev --store pasta-delights.myshopify.com
```

For a shareable unpublished copy, use Shopify CLI's preview/share workflow from this branch after confirming the local preview:

```bash
shopify theme share --store pasta-delights.myshopify.com
```

Do not use `shopify theme push --live` and do not select the live theme as a push target.
