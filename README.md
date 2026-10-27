# Marcel's Website
marwage.github.io

## Interactive demos

Standalone interactive pages live in `static/<slug>/index.html`. Embed one in a
blog post with the `demo` shortcode:

```md
{{< demo src="/marathon/" title="Marathon pace chart" caption="Pace, speed, and finish time over 42.195 km." >}}
```

The shortcode adds the page's embed mode (`?embed=1`) and sizes the iframe to its
content. Keep `static/embed.css` for the shared embed-mode styling, and include
the same embed-mode snippet and stylesheet link in any new demo page.
