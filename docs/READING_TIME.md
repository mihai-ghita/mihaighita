# Reading Time Estimates

## Overview

Reading time estimates help readers understand the time commitment before starting an article. The feature displays estimated reading time on both post cards and individual post pages.

## How It Works

Hugo automatically calculates reading time based on word count using the industry-standard reading speed of approximately 200-250 words per minute.

### Calculation
- **Formula**: `word_count / 200 words per minute`
- **Minimum**: 1 minute (even for very short posts)
- **Rounding**: Rounded to nearest minute

### Display Locations

**Post Cards (Blog Listing)**
- Format: `Date • X min read`
- Example: `January 5, 2026 • 2 min read`
- Position: Below post title, above categories

**Single Post Page**
- Format: `Date • X min read • Y words`
- Example: `January 5, 2026 • 2 min read • 235 words`
- Position: In post meta section, after title

## Technical Implementation

### Hugo Variables

Hugo provides these built-in variables:
- `.ReadingTime` - Estimated reading time in minutes
- `.WordCount` - Total word count of the post

### Template Code

**Post Card** (`layouts/partials/post-card.html`):
```html
<div class="post-card-info">
    <time datetime="{{ .Date.Format "2006-01-02" }}">
        {{ .Date.Format "January 2, 2006" }}
    </time>
    <span class="reading-time">{{ .ReadingTime }} min read</span>
</div>
```

**Single Post** (`layouts/posts/single.html`):
```html
<div class="post-meta-info">
    <time datetime="{{ .Date.Format "2006-01-02" }}">
        {{ .Date.Format "January 2, 2006" }}
    </time>
    <span class="reading-time">{{ .ReadingTime }} min read</span>
    <span class="word-count">{{ .WordCount }} words</span>
</div>
```

### Styling

The reading time is styled to match the date format:

```css
.reading-time {
    font-size: 14px;
    color: #718096;
    display: flex;
    align-items: center;
    gap: 4px;
}

.reading-time::before {
    content: "•";
    color: #cbd5e0;
}
```

## Reading Time Ranges

Based on word count, typical reading times:

| Word Count | Reading Time | Article Type |
|------------|--------------|--------------|
| 100-300    | 1-2 min      | Quick tip, announcement |
| 300-600    | 2-3 min      | Short tutorial, opinion piece |
| 600-1200   | 3-5 min      | Medium article, how-to guide |
| 1200-2000  | 5-8 min      | Long tutorial, deep dive |
| 2000-3000  | 8-12 min     | Comprehensive guide |
| 3000+      | 12+ min      | In-depth article, case study |

## Benefits

### For Readers
- **Time management**: Know commitment before reading
- **Content filtering**: Quick scan vs. deep dive
- **Better planning**: Choose articles based on available time
- **Reduced bounce**: Readers know what to expect

### For Authors
- **Content awareness**: See how long articles are
- **Consistency**: Maintain similar post lengths
- **Engagement metrics**: Track correlation with read time
- **SEO**: Can be used in rich snippets

## Best Practices

### Writing Guidelines

**Short Posts (1-3 min)**
- Quick tips, announcements, updates
- Single focused topic
- Scannable format with bullets/lists
- Clear takeaway

**Medium Posts (3-7 min)**
- Tutorials, how-to guides
- Multiple sections or steps
- Code examples and explanations
- Practical applications

**Long Posts (7+ min)**
- Comprehensive guides, deep dives
- Multiple concepts or topics
- Detailed explanations
- Case studies, research

### Optimization Tips

1. **Front-load value**: Most important info first
2. **Use subheadings**: Help readers scan and skip
3. **Break up content**: Use lists, code blocks, images
4. **Be concise**: Respect reader's time
5. **Consider splitting**: Very long posts into series

## Customization

### Adjusting Reading Speed

If you want to use a different reading speed, you can customize it with a partial:

```html
<!-- layouts/partials/reading-time.html -->
{{ $words := .WordCount }}
{{ $speed := 180 }} <!-- slower reading speed -->
{{ $minutes := div $words $speed }}
{{ $readTime := cond (lt $minutes 1) 1 $minutes }}
{{ $readTime }} min read
```

### Different Formats

**Detailed Format**:
```html
<span class="reading-time">
    {{ .ReadingTime }} minute{{ if gt .ReadingTime 1 }}s{{ end }} to read
</span>
```

**Range Format**:
```html
<span class="reading-time">
    {{ .ReadingTime }}-{{ add .ReadingTime 1 }} min
</span>
```

**With Icon** (if using icon library):
```html
<span class="reading-time">
    <svg><!-- clock icon --></svg>
    {{ .ReadingTime }} min
</span>
```

## Accessibility

The reading time feature is accessible:
- **Semantic HTML**: Plain text, no images
- **Screen readers**: Clearly announced
- **Color contrast**: Meets WCAG AA standards
- **No interaction required**: Informational only

## SEO Considerations

### Rich Snippets

Reading time can be added to structured data:

```json
{
  "@type": "Article",
  "timeRequired": "PT{{ .ReadingTime }}M"
}
```

### Meta Tags

Include in meta description or article data:

```html
<meta name="twitter:label1" content="Reading time">
<meta name="twitter:data1" content="{{ .ReadingTime }} min">
```

## Analytics Integration

Track correlation between reading time and engagement:

```javascript
// Example: Track with Google Analytics
gtag('event', 'article_view', {
  'reading_time': {{ .ReadingTime }},
  'word_count': {{ .WordCount }},
  'category': '{{ index .Params.categories 0 }}'
});
```

## Examples

### Post Card Display
```
┌─────────────────────────────────┐
│  [Featured Image]               │
├─────────────────────────────────┤
│  Building a REST API            │
│  January 5, 2026 • 5 min read  │
│  [tutorials]                    │
│  Step-by-step guide to...      │
└─────────────────────────────────┘
```

### Single Post Meta
```
Home → tutorials → Building a REST API

Building a REST API with Go

January 5, 2026 • 5 min read • 987 words    [tutorials]
─────────────────────────────────────────────────────
```

## Troubleshooting

### Reading Time Shows 0 or Negative
- **Cause**: Post has very little content
- **Fix**: Hugo shows minimum 1 minute, check template

### Reading Time Seems Inaccurate
- **Cause**: Code blocks counted at normal reading speed
- **Solution**: This is Hugo's default behavior, acceptable variance

### Not Displaying on Cards
- **Check**: Template syntax is correct
- **Check**: CSS is not hiding the element
- **Rebuild**: Run `hugo` to regenerate

## Future Enhancements

Potential improvements:
- [ ] Adjust speed for technical content (slower)
- [ ] Different speeds for different categories
- [ ] Visual indicators (coffee cups, book icons)
- [ ] Reading progress bar on long posts
- [ ] A/B test different reading speeds
- [ ] Track actual reading time vs estimate

## Related Documentation

- `SUMMARIES.md` - Writing effective post summaries
- `FEATURED_IMAGES.md` - Adding featured images
- Hugo Documentation: [Page Variables](https://gohugo.io/variables/page/)
