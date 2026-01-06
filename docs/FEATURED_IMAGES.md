# Featured Images for Blog Posts

## Overview

Featured images are now supported for blog posts. They appear on post cards in the blog listing and at the top of individual blog post pages.

## How to Add a Featured Image

Add the `featured_image` parameter to your post's front matter:

```markdown
---
title: "Your Post Title"
date: 2026-01-05T10:00:00+02:00
categories: ["tutorials"]
tags: ["hugo", "blogging"]
draft: false
featured_image: "/imgs/your-image.jpg"
---

Your post content here...
```

## Image Guidelines

### Recommended Specifications
- **Format**: JPG, PNG, or WebP
- **Dimensions**: Minimum 1200x630px (recommended for social sharing)
- **Aspect Ratio**: 16:9 or 2:1 works best
- **File Size**: Keep under 500KB for optimal performance
- **Location**: Place images in the `static/imgs/` directory

### Image Storage
1. Add your image to `static/imgs/`
2. Reference it in front matter as `/imgs/your-image.jpg`
3. Hugo will copy it to the output directory automatically

### Example Structure
```
static/
  imgs/
    blog/
      2026-01-05-welcome.jpg
      2026-01-10-tutorial.png
    projects/
      project-screenshot.jpg
```

## How It Works

### Post Cards (Blog Listing)
- Featured image displays at the top of the card
- Height: 200px with object-fit cover
- Hover effect: Image zooms slightly (1.05x scale)
- Lazy loading enabled for performance
- If no featured image is set, card shows content only

### Single Post Page
- Featured image appears after the post meta information
- Full width with automatic height
- Rounded corners (10px border-radius)
- Box shadow for depth

## Styling Details

### Post Card Image
- Container: 200px height, full width
- Image: object-fit cover (maintains aspect ratio)
- Hover: transform scale(1.05)
- Background: #f7fafc (light gray fallback)

### Single Post Featured Image
- Full width within container
- Auto height (maintains aspect ratio)
- Border radius: 10px
- Box shadow: 0 10px 30px rgba(0, 0, 0, 0.15)
- Margin top: 30px

## Example Posts

See `content/posts/welcome-to-my-blog.md` for a working example.

## Optional: Featured Images

Featured images are completely optional. If you don't add a `featured_image` parameter:
- Post cards will show text content only
- Single post pages won't display a hero image
- Everything else works normally

## Tips

1. **Consistency**: Use similar aspect ratios across all posts for a cohesive look
2. **Optimization**: Compress images before adding them to the repository
3. **Alt Text**: The post title is automatically used as alt text
4. **Responsive**: Images automatically scale on mobile devices
5. **Performance**: Use lazy loading (built-in) for better performance

## Creating Featured Images

### Tools
- **Canva**: Easy templates for blog images
- **Figma**: Custom designs
- **Unsplash/Pexels**: Free stock photos
- **ImageOptim/TinyPNG**: Image compression

### Design Tips
- Include the post title in the image
- Use your brand colors (purple gradient: #667eea to #764ba2)
- Keep text readable at small sizes
- Ensure the image works when cropped to different ratios
- Consider how the image looks at 200px height in cards

## Troubleshooting

### Image Not Showing
1. Check the path starts with `/imgs/` (not `imgs/` or `./imgs/`)
2. Verify the image exists in `static/imgs/`
3. Rebuild Hugo: `hugo` or `hugo server -D`
4. Clear browser cache

### Image Looks Distorted
- Ensure minimum dimensions (1200x630px)
- Use 16:9 or 2:1 aspect ratio
- Check that object-fit: cover is working

### Performance Issues
- Compress images to < 500KB
- Use JPG for photos, PNG for graphics
- Consider WebP format for modern browsers
- Use appropriate dimensions (don't upload 4K images)

## Responsive Images

### Using srcset for Performance

Serve appropriately sized images based on device viewport:

```markdown
---
featured_image: "/imgs/post-800w.jpg"
featured_image_srcset: "/imgs/post-400w.jpg 400w, /imgs/post-800w.jpg 800w, /imgs/post-1200w.jpg 1200w"
---
```

The browser automatically selects the best image size based on:
- Device viewport width
- Device pixel ratio (retina vs standard)
- Network conditions (in some browsers)

### Art Direction with Picture Element

Use different crops or compositions for different screen sizes:

```markdown
---
featured_image: "/imgs/post-desktop.jpg"
featured_image_mobile: "/imgs/post-mobile-crop.jpg"
featured_image_tablet: "/imgs/post-tablet-crop.jpg"
---
```

**Example Use Cases:**
- Mobile: Portrait crop focusing on subject
- Tablet: Landscape crop with more context
- Desktop: Full wide landscape

See `docs/RESPONSIVE_DESIGN.md` for complete responsive image documentation.

## Future Enhancements

Planned improvements for featured images:
- [ ] Automatic image resizing/optimization
- [X] Multiple image sizes (srcset) for responsive images
- [ ] Social media meta tags (Open Graph, Twitter Cards)
- [ ] Default/placeholder images for posts without featured images
- [ ] Image caption support
- [ ] WebP format support with fallbacks
