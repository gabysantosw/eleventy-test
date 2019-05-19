---
layout: layout.njk
---
# Leaning Eleventy

## Steps

### Install locally
- Create a `package.json` for the project
  - `npm init`, then set up the basic json file
- Install eleventy locally
  - `npm install --save-dev @11ty/eleventy`, this takes less than a minute
  - The installation will add the Eleventy depencency: `"devDependencies": { "@11ty/eleventy": "^0.8.3" }` to the `package.json`
  - Will also add `node_modules` to the project
- Run eleventy locally
  - `npx eleventy`

### Add files
- Create an html file
- Create a markdown file
- Creating these files will add a `_site` output folder, this is where the final website will be located
  - Eleventy will transform that markdown file into html
- Live serve for eleventy
  - Run `npx eleventy --serve`, the npx means its running locally
  - Console will show the URL where site is being served, usually localhost:8080

### Runing eleventy
- `eleventy` -> searches current directory and outputs to `_site` folder
  - The same as `eleventy --input=. --output=_site`
- Other commands: [Eleventy command line](https://www.11ty.io/docs/usage/)

### The markdown -> html in `_site`
- Eleventy will transform that markdown into the related html tag
  - `#` -> will be a `h1` tag
  - backticks -> will be a `code` tag
  - same with other headings, lists and links

### making the markdown -> html actually valid html
- When the markdown file gets transformed it only adds the inside content, but an html file needs more than that (html, head, body, so on)
- To fix this we need to add a layout
  - Create a `_includes` folder
  - Create a nunjucks file (`layout.njk`) file
    - this nunjucks file will contain the basic html but allows to output data
    - `{{ content | safe }}` -> shows the entire content
  - Set the layout in the markdown file
    - `layout: layout.njk` -> goes at the top of the markdown file and is surrounded by `---`
- Now the markdown is actually visible in the html, it will be added in the content

### Linking your css / js files
1. Inside `_includes`:
  - Create file / folder and link using: `<style>{% include "css/styles.css" %}</style>`
  - For JS: `<script>{% include "js/script.js" %}</script>`
2. `<link rel="stylesheet" href="{{ '/css/styles.css' | url }}">` is used in 'eleventy-base-blog', don't know how

### to not commit to github node_modules
- create `.gitignore` file and add `node_modules/` in one line, `package-lock.json` is recommended to ignore too
