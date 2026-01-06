# Responsive Design

## Overview

The website is built with a mobile-first approach and includes three breakpoints to ensure optimal viewing experience across all devices from smartphones to large desktop monitors.

## Breakpoints

### Mobile (Default - up to 600px)
- **Target Devices**: Smartphones in portrait mode
- **Design Focus**: Single column layout, touch-friendly targets
- **Container Width**: Full width with 25px padding
- **Navigation**: Hamburger menu with slide-down animation

### Tablet (601px to 1024px)
- **Target Devices**: Tablets, small laptops, smartphones in landscape
- **Design Focus**: Efficient use of medium screen space
- **Container Width**: Full width with 35px padding
- **Navigation**: Full horizontal menu

### Desktop (1025px to 1439px)
- **Target Devices**: Standard desktop monitors, large laptops
- **Design Focus**: Default desktop experience
- **Container Width**: 1200px max-width
- **Navigation**: Full horizontal menu with hover states

### Large Desktop (1440px+)
- **Target Devices**: Large monitors, 4K displays
- **Design Focus**: Spacious layout with larger typography
- **Container Width**: 1400px max-width
- **Navigation**: Enhanced spacing

## Typography Scaling

### Headings

**Hero Title (h1)**
- Mobile: 36px
- Tablet: 48px
- Desktop: 52px
- Large Desktop: 64px

**Page Title (h1)**
- Mobile: 32px
- Tablet: 38px
- Desktop: 42px
- Large Desktop: 42px

**Section Title (h2)**
- Mobile: 28px
- Tablet: 28px
- Desktop: 32px
- Large Desktop: 36px

**Subheading (h3)**
- Mobile: 20px
- Tablet: 22px
- Desktop: 24px
- Large Desktop: 24px

### Body Text

**Post Content**
- Mobile: 16px
- Tablet: 17px
- Desktop: 18px
- Large Desktop: 19px

**Meta Information**
- All devices: 14-15px (consistent)

## Layout Adjustments

### Post Grid

**Mobile (up to 600px)**
```css
grid-template-columns: 1fr;
gap: 20px;
```
One column, stacked vertically

**Tablet (601px to 1024px)**
```css
grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
gap: 25px;
```
2 columns on most tablets

**Desktop (1025px+)**
```css
grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
gap: 30px;
```
3 columns typically

**Large Desktop (1440px+)**
```css
grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
gap: 40px;
```
3-4 columns with larger cards

### Navigation

**Desktop (1025px+)**
- Horizontal menu bar
- Hover dropdowns
- 30px gap between items

**Tablet (601px to 1024px)**
- Horizontal menu bar
- Hover dropdowns
- 20px gap between items

**Mobile (up to 600px)**
- Hamburger menu icon (☰)
- Slide-down menu animation
- Full-width stacked items
- Tap to expand dropdowns

## Touch Targets

All interactive elements meet WCAG 2.1 AA guidelines for touch target size.

### Minimum Sizes

**Navigation Links**: 44px × 44px minimum
**Social Icons**: 50px × 50px (exceeds minimum)
**Buttons**: 44px height minimum
**Category Badges**: 28px height on mobile
**Post Navigation**: 44px height minimum

### Implementation

```css
.nav-link {
    padding: 12px 20px;
    min-height: 44px;
    display: flex;
    align-items: center;
}

.social-links a {
    width: 50px;
    height: 50px;
    min-width: 44px;
    min-height: 44px;
}
```

## Mobile Menu Animation

### Hamburger Icon Animation

When menu is opened:
- Top bar: Rotates 45° and translates down
- Middle bar: Fades out (opacity: 0)
- Bottom bar: Rotates -45° and translates up
- Creates an "X" close icon

```css
.menu-toggle:checked ~ .menu-icon span:nth-child(1) {
    transform: rotate(45deg) translate(6px, 6px);
}

.menu-toggle:checked ~ .menu-icon span:nth-child(2) {
    opacity: 0;
}

.menu-toggle:checked ~ .menu-icon span:nth-child(3) {
    transform: rotate(-45deg) translate(6px, -6px);
}
```

### Menu Slide Animation

```css
.nav-menu {
    animation: slideDown 0.3s ease-out;
}

@keyframes slideDown {
    from {
        opacity: 0;
        transform: translateY(-10px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}
```

## Responsive Images

### Using srcset

For better performance, use srcset to serve appropriately sized images:

```markdown
---
featured_image: "/imgs/post-800w.jpg"
featured_image_srcset: "/imgs/post-400w.jpg 400w, /imgs/post-800w.jpg 800w, /imgs/post-1200w.jpg 1200w"
---
```

**Post Cards**
```html
sizes="(max-width: 600px) 100vw, (max-width: 1024px) 50vw, 33vw"
```
- Mobile: Full viewport width
- Tablet: 50% of viewport
- Desktop: 33% of viewport

**Single Post**
```html
sizes="(max-width: 600px) 100vw, (max-width: 1024px) 90vw, 800px"
```
- Mobile: Full viewport width
- Tablet: 90% of viewport
- Desktop: Fixed 800px

### Picture Element (Art Direction)

For different image crops on different devices:

```markdown
---
featured_image: "/imgs/post-desktop.jpg"
featured_image_mobile: "/imgs/post-mobile.jpg"
featured_image_tablet: "/imgs/post-tablet.jpg"
---
```

The template automatically uses:
- Mobile: Square or portrait crop
- Tablet: Wider crop
- Desktop: Full landscape

## Smooth Scrolling

The site implements smooth scrolling for anchor links:

```css
html {
    scroll-behavior: smooth;
}
```

This applies to:
- Skip to content links
- Back to top buttons
- In-page navigation
- Anchor links

### Accessibility Note

Users with `prefers-reduced-motion` should not see smooth scrolling. Add this for full accessibility:

```css
@media (prefers-reduced-motion: reduce) {
    html {
        scroll-behavior: auto;
    }
}
```

## Testing Responsive Design

### Browser DevTools

1. Open Chrome/Firefox DevTools (F12)
2. Click device toolbar icon
3. Test these viewports:
   - iPhone SE: 375px
   - iPhone 12 Pro: 390px
   - iPad: 768px
   - iPad Pro: 1024px
   - Desktop: 1920px
   - 4K: 2560px

### Key Test Points

**Mobile (375px - 600px)**
- [ ] Hamburger menu appears and works
- [ ] Menu animates smoothly
- [ ] All links are tappable (44px)
- [ ] Text is readable (16px minimum)
- [ ] Images don't overflow
- [ ] Forms are usable

**Tablet (768px - 1024px)**
- [ ] Layout uses available space
- [ ] Navigation is horizontal
- [ ] Grid shows 2 columns
- [ ] Images are appropriately sized
- [ ] No awkward gaps or spacing

**Desktop (1920px)**
- [ ] Content is centered with max-width
- [ ] Grid shows 3-4 columns
- [ ] Typography is comfortable to read
- [ ] Hover states work properly

**Large Desktop (2560px+)**
- [ ] Content doesn't stretch too wide
- [ ] Typography scales appropriately
- [ ] Grid cards maintain good proportions
- [ ] No excessive white space

## Performance Considerations

### Image Optimization

**Recommended Sizes**
- Mobile: 400-600px width
- Tablet: 800px width
- Desktop: 1200px width

**Formats**
- Use WebP with JPG fallback
- Compress to 80-85% quality
- Use lazy loading for below-fold images

### CSS

**Current Setup**
- Two CSS files: main.css and blog.css
- Minified in production
- Inline critical CSS (future enhancement)

### Loading Strategy

- CSS: Loaded in `<head>` (render-blocking)
- Images: Lazy loaded with `loading="lazy"`
- Fonts: System font stack (no web fonts loaded)

## Best Practices

### Mobile-First Approach

1. Design for mobile first
2. Add complexity for larger screens
3. Use min-width media queries when adding features
4. Use max-width for mobile-specific overrides

### Touch-Friendly Design

1. Minimum 44px × 44px touch targets
2. Adequate spacing between tappable elements
3. No hover-only interactions on mobile
4. Clear focus states for keyboard navigation

### Performance

1. Serve appropriately sized images
2. Use lazy loading for images
3. Minimize CSS and JavaScript
4. Test on real devices, not just emulators

### Accessibility

1. Maintain color contrast ratios
2. Ensure keyboard navigation works
3. Add ARIA labels where needed
4. Support reduced motion preferences
5. Test with screen readers

## Browser Support

### Target Browsers

- Chrome/Edge: Last 2 versions
- Firefox: Last 2 versions
- Safari: Last 2 versions
- iOS Safari: Last 2 versions
- Chrome Android: Last 2 versions

### CSS Features Used

- Flexbox: Full support
- CSS Grid: Full support
- CSS Variables: Not currently used (future enhancement)
- Media Queries: Full support
- Transforms: Full support
- Animations: Full support

## Future Enhancements

- [ ] Add CSS custom properties for consistent breakpoints
- [ ] Implement reduced motion preferences
- [ ] Add print stylesheet
- [ ] Support for landscape/portrait orientation
- [ ] Container queries (when widely supported)
- [ ] Automatic image optimization with Hugo
- [ ] Progressive image loading (blur-up technique)

## Related Documentation

- `FEATURED_IMAGES.md` - Image requirements and optimization
- `READING_TIME.md` - Reading time calculation
- `SUMMARIES.md` - Content guidelines
