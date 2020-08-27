---
layout: post
title: Jekyll SEO
description: SEO for blogs using jekyll.
keywords: Blogs, Jekyll, SEO
---

## Page Template
``` code
---
layout: post
title: Jekyll SEO
description: SEO for blogs using jekyll.
keywords: Blogs, Jekyll, SEO
---
```
## Configure Head
Add description and keywords for the SEO.
```code
 <meta name="description" content="{% if page.description %}{{ page.description }}{% else %}{{ site.description }}{% endif %}">
  {% if page.keywords %}
 <meta name="keywords" content="{{ page.keywords }}" />
  {% else %}
 <meta name="keywords" content="your-default-comma-separated-keywords" />
 {% endif %}
```

### Install Plugin 
 Install *jekyll-seo-tag*
Add jekyll SEO tag plugin to head using 
``` code
{% seo %}
```

## Add sitemap.xml

```code
---
layout: null
sitemap:
  exclude: 'yes'
---
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  {% for post in site.posts %}
    {% unless post.published == false %}
    <url>
      <loc>{{ site.url }}{{ post.url }}</loc>
      {% if post.sitemap.lastmod %}
        <lastmod>{{ post.sitemap.lastmod | date: "%Y-%m-%d" }}</lastmod>
      {% elsif post.date %}
        <lastmod>{{ post.date | date_to_xmlschema }}</lastmod>
      {% else %}
        <lastmod>{{ site.time | date_to_xmlschema }}</lastmod>
      {% endif %}
      {% if post.sitemap.changefreq %}
        <changefreq>{{ post.sitemap.changefreq }}</changefreq>
      {% else %}
        <changefreq>monthly</changefreq>
      {% endif %}
      {% if post.sitemap.priority %}
        <priority>{{ post.sitemap.priority }}</priority>
      {% else %}
        <priority>0.5</priority>
      {% endif %}
    </url>
    {% endunless %}
  {% endfor %}
  {% for page in site.pages %}
    {% unless page.sitemap.exclude == "yes" %}
      {% unless page.url contains 'index.html' %}
      <url>
        <loc>{{ site.url }}{{ page.url | remove: "index.html" }}</loc>
        {% if page.sitemap.lastmod %}
          <lastmod>{{ page.sitemap.lastmod | date: "%Y-%m-%d" }}</lastmod>
        {% elsif page.date %}
          <lastmod>{{ page.date | date_to_xmlschema }}</lastmod>
        {% else %}
          <lastmod>{{ site.time | date_to_xmlschema }}</lastmod>
        {% endif %}
        {% if page.sitemap.changefreq %}
          <changefreq>{{ page.sitemap.changefreq }}</changefreq>
        {% else %}
          <changefreq>monthly</changefreq>
        {% endif %}
        {% if page.sitemap.priority %}
          <priority>{{ page.sitemap.priority }}</priority>
        {% else %}
          <priority>0.3</priority>
        {% endif %}
      </url>
      {% endunless %}
    {% endunless %}
  {% endfor %}
</urlset>
```
## Add robots.txt
```code
User-agent: *
Sitemap: your-site-url/sitemap.xml
```

