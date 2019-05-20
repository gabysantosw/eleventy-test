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

### the `.eleventy.js` file
- We'll use it to set a folder for the input, by default is the current directory:
  - `module.exports = { dir: { input: "folder-name" } }`
- Setting the html template and markdown template to nunjucks, we add these properties to the `module.exports`: `markdownTemplateEngine: "njk"` and `htmlTemplateEngine: "njk"`
The file will end up like:
```js
module.exports = {
  dir: {
    input: "source",
  },
  markdownTemplateEngine: "njk",
  htmlTemplateEngine: "njk"
};
```

### Content is displayed
- `backtics` go inside a p tag and a code tag
- code syntax will go inside a pre tag and a code tag, a class 'language-js' will be added if code language is specified
- headings will correspond to h1-h6
- list items will be wrapped inside ul / ol
- list item text will be wrapped around a p tag, inside an li

### Collections / tags
- setting a `tags: post` to the file will save it in a collection
- these collection can be accessed with `collection.post`
- other contents like 'title' of the file can be accessed using `.data.title`
- setting tags in the .md can be done like: `tags: ['cats', 'dogs']` or `tags:
  - cats
  - dogs`

### Nunjucks for in
`{%- for post in collections.post -%}` -> initiates the loop
`{%- endfor -%}` -> ends loop

### Navigation links with a class for current page
- `page.url` -> Eleventy variable to find the current page
- `tags.url` -> can be accessed through collections
- Using the for post in collections.post to compare the `page.url` with the `post.url`
```html
<ul>
{%- for post in collections.post -%}
  <li{% if page.url == post.url %} class="active"{% endif %}>{{ post.data.title }}</li>
{%- endfor -%}
</ul>
```

### All collection
- `collections.all` -> Eleventy places all the content inside
- `eleventyExcludeFromCollections: true` can be set in the .md to avoid the content to be available in collections

### Collection data
- `.url`
- `.inputPath`
- `.fileSlug`
- `outputPath`
- `.url`
- `.date`
- `.data`
- `templateContent`
