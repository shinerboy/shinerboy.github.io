---
title: "Post: Image (Standard)"
categories:
  - Post Formats
  - projects
tags:
  - image
  - Post Formats
---

The preferred way of using images is placing them in the `/assets/images/` directory and referencing them with an absolute path. Prepending the filename with `{% raw %}{{ site.url }}{{ site.baseurl }}/assets/images/{% endraw %}` will make sure your images display properly in feeds and such.

Standard image with no width modifier classes applied.

**HTML:**

```html
{% raw %}<img src="{{ site.url }}{{ site.baseurl }}/assets/images/yosemite.jpg" alt="">{% endraw %}
```

**or Kramdown:**

```markdown
{% raw %}![alt]({{ site.url }}{{ site.baseurl }}/assets/images/yosemite.jpg){% endraw %}
```

![Unsplash image 9]({{ site.url }}{{ site.baseurl }}/assets/images/yosemite.jpg)

Image that fills page content container by adding the `.full` class with:

**HTML:**

```html
{% raw %}<img src="{{ site.url }}{{ site.baseurl }}/assets/images/yosemite.jpg" alt="" class="full">{% endraw %}
```

**or Kramdown:**

```markdown
{% raw %}![alt]({{ site.url }}{{ site.baseurl }}/assets/images/yosemite.jpg)
{: .full}{% endraw %}
```

![Unsplash image 10]({{ site.url }}{{ site.baseurl }}/assets/images/yosemite.jpg)
{: .full}