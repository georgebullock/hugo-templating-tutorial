---
title: "Hugo Code Sample"
date: 2022-02-10T16:51:11+01:00
draft: false
---

```
-------------------------------------------------------------------------
  File Structure
-------------------------------------------------------------------------
├── archetypes
├── config.toml
├── content
├── data
├── layouts
├── static
└── themes

-------------------------------------------------------------------------
  _baseof.HTML
-------------------------------------------------------------------------
<html>
  <head>
    <meta charset="UTF-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1.0, shrink-to-fit=no"
    />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />

    {{$styles := resources.Get "/styles.scss" | toCSS | minify}}
    <link rel="stylesheet" href="{{$styles.Permalink | relURL}}" />

    <title>{{ .Title }}</title>

  </head>

  <body>
    <div class="columns">
      <div class="column is-one-third">
        <!-- Define sidebar block to render sidebar content -->
        {{ block "sidebar" . }}{{ end }}
      </div>

      <div class="column">
        <!-- Define main block to render main content -->
        {{ block "main" . }}{{ end }}
      </div>
    </div>

    <!-- Define footer block to render footer content -->
    {{ block "footer" . }}{{ end }}

  </body>
</html>

-------------------------------------------------------------------------
  single.HTML
-------------------------------------------------------------------------
{{ define "sidebar" }}
  {{ partial "navigation.html" }}
{{ end }}

{{ define "main" }}
  <section class="section">
    <h1 class="title">{{ .Title }}</h1>
    {{ .Content }}
  </section>
{{ end }}

{{ define "footer" }}
  {{ partial "footer.html" }}
{{ end }}


-------------------------------------------------------------------------
  list.HTML
-------------------------------------------------------------------------
{{ define "sidebar" }}
  {{ partial "navigation.html" }}
{{ end }}

{{ define "main" }}
  <section class="section">
    <h1 class="title">Main Section</h1>
    {{ range (.Site.GetPage "section" "learn").Pages }}
    <ul>
      <li><a href="{{ .Permalink }}">{{ .Title }}</a></li>
    </ul>
    {{ end }}
  </section>
{{ end }}

{{ define "footer" }}
  {{ partial "footer.html" }}
{{ end }}
```
