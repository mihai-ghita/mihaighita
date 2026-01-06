# Blog Post Summaries

## Overview

Blog post summaries appear on post cards in the blog listing page. Properly crafted summaries help readers understand what your post is about and encourage them to read more.

## How Summaries Work

Hugo provides three ways to define summaries, checked in this order:

### 1. Manual Description (Recommended)

Add a `description` field in your front matter for complete control:

```markdown
---
title: "Your Post Title"
date: 2026-01-05T10:00:00+02:00
description: "A concise, engaging summary of your post in 140-160 characters."
---

Your post content here...
```

**Best for:** When you want precise control over what appears in post cards and social media previews.

### 2. Summary Divider

Use the `<!--more-->` comment to define where the summary ends:

```markdown
---
title: "Your Post Title"
date: 2026-01-05T10:00:00+02:00
---

This is the summary part that will appear in post cards.

<!--more-->

This is the rest of your post content that won't appear in the summary.
```

**Best for:** When your opening paragraph makes a good natural summary.

### 3. Auto-Generated Summary

If no description or `<!--more-->` divider is provided, Hugo automatically generates a summary using the first 30 words (configured in `config.yaml`).

**Best for:** Quick posts where the opening works as a summary.

## Summary Display

### Post Cards
- Displayed below the post title and metadata
- HTML tags are stripped automatically using `plainify`
- Truncated to 160 characters maximum
- Ellipsis (...) added if truncated
- Clean, readable text only

### Configuration

Summary length is configured in `config.yaml`:

```yaml
summaryLength: 30  # Number of words for auto-summary
```

## Best Practices

### Length Guidelines
- **Optimal:** 120-160 characters
- **Minimum:** 80 characters
- **Maximum:** 160 characters (automatically truncated)

### Writing Tips
1. **Be specific:** Tell readers exactly what they'll learn
2. **Include keywords:** Help with SEO and searchability
3. **Create interest:** Make readers want to click and read more
4. **Avoid HTML:** Use plain text only in descriptions
5. **Front-load value:** Most important info first

### Good Examples

```markdown
description: "Learn how to build scalable data pipelines using Apache Airflow, Docker, and PostgreSQL in this step-by-step tutorial."
```

```markdown
description: "5 practical tips for improving your code review process, based on lessons learned from reviewing 1000+ pull requests."
```

```markdown
description: "A deep dive into React Server Components: what they are, how they work, and when you should use them in your Next.js apps."
```

### Bad Examples

```markdown
# Too vague
description: "This post is about web development."

# Too long
description: "In this comprehensive guide, I'll walk you through everything you need to know about building modern web applications using the latest technologies including React, Next.js, TypeScript, Tailwind CSS, and deploying to Vercel with continuous integration."

# Contains HTML
description: "<p>Learn about <strong>data engineering</strong> in this post.</p>"

# Too short
description: "Web tips."
```

## Technical Details

### Template Logic

The post card template checks summaries in this order:

```go
{{ if .Description }}
  <!-- Use manual description -->
  <p class="post-card-summary">{{ .Description }}</p>
{{ else if .Summary }}
  <!-- Use auto-generated or <!--more--> summary, strip HTML, truncate -->
  <p class="post-card-summary">{{ .Summary | plainify | truncate 160 }}</p>
{{ end }}
```

### Functions Used
- `plainify`: Strips all HTML tags and converts to plain text
- `truncate 160`: Truncates to 160 characters, adds "..."

### CSS Styling

```css
.post-card-summary {
    color: #4a5568;
    line-height: 1.6;
    font-size: 15px;
}
```

## SEO Benefits

Good summaries help with:
- **Post cards:** Attractive listings that encourage clicks
- **Meta descriptions:** Can be reused for SEO meta tags
- **Social sharing:** Better previews on social media
- **RSS feeds:** Clear descriptions in feed readers
- **Search results:** May appear in search snippets

## Examples in Practice

### Example 1: Technical Tutorial

```markdown
---
title: "Building a REST API with Go and PostgreSQL"
description: "Step-by-step guide to creating a production-ready REST API using Go, PostgreSQL, and Docker with authentication and testing."
featured_image: "/imgs/go-api-tutorial.jpg"
---

In this tutorial, you'll learn how to build a REST API...

<!--more-->

## Prerequisites
...
```

### Example 2: Project Showcase

```markdown
---
title: "Building a Real-Time Analytics Dashboard"
description: "How I built a real-time analytics dashboard processing 10M events/day using Kafka, ClickHouse, and React with sub-second latency."
featured_image: "/imgs/analytics-dashboard.jpg"
---

This project started when our team needed...

<!--more-->

## Architecture Overview
...
```

### Example 3: Career Insights

```markdown
---
title: "5 Lessons from My First Year as a Senior Engineer"
description: "Key lessons learned transitioning to senior engineer: technical leadership, mentoring, architecture decisions, and work-life balance."
featured_image: "/imgs/senior-engineer.jpg"
---

One year ago, I was promoted to senior engineer...

<!--more-->

## 1. Technical Leadership
...
```

## Troubleshooting

### Summary Shows HTML Tags
- **Solution:** Add a manual `description` field in front matter
- **Or:** The template now uses `plainify` to strip HTML automatically

### Summary Too Long
- **Solution:** Keep description under 160 characters
- **Auto-fix:** Template automatically truncates to 160 characters

### Summary Too Short
- **Solution:** Aim for 120-160 characters for best results
- **Note:** Short summaries are allowed but may not be as effective

### No Summary Showing
- **Check:** Ensure post has content
- **Check:** Front matter is properly formatted
- **Check:** No template errors (check Hugo build output)

## Future Enhancements

Planned improvements:
- [ ] Different summary lengths for different contexts (card, meta, social)
- [ ] Summary character count validation in CI/CD
- [ ] Automatic keyword extraction
- [ ] A/B testing for summary effectiveness
- [ ] Summary templates for common post types

## Related Documentation

- `FEATURED_IMAGES.md` - Adding featured images to posts
- `config.yaml` - Summary configuration settings
- Hugo Documentation: [Content Summaries](https://gohugo.io/content-management/summaries/)
