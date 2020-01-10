# Gridsome Casper V3 Starter

Grisome starter based on [Ghost Casper V3](https://github.com/TryGhost/Casper) and tailwindcss.

## Demo
[https://gridsome-starter-casper-v3.now.sh/](https://gridsome-starter-casper-v3.now.sh/)

## Features

* Gridsome
* Tailwindcss with some custom configuration
  * tailwindcss tables plugin
* Light and Dark Mode with auto detect  
* v-tooltip
* SCSS
* Markdown
* Tags
* Categories
* Author Pages
* Blog
* About Page
* Pagination

## Plugins

With Gridsome offering a plugin-rich ecosystem, there are a few key plugins that make this project possible. 

- [Gridsome Source Filesystem](https://gridsome.org/plugins/@gridsome/source-filesystem) Transform files into content that can be fetched with GraphQL in your components.
- [gridsome-source-static-meta](https://gridsome.org/plugins/gridsome-source-static-meta) source plugin that converts values in JSON and/or YAML files into keys on the global GraphQL metaData query.
- [gridsome-remark-classes](https://gridsome.org/plugins/@noxify/gridsome-remark-classes) Gridsome Remark plugin to add css classes to any element
- [gridsome-remark-table-align](https://gridsome.org/plugins/@noxify/gridsome-remark-table-align) Gridsome Remark plugin move the `table` align defintion to the `tableCell` definition.



## Install

### 1. Install Gridsome CLI tool if you don't have

`npm install --global @gridsome/cli`

### 2. Create a Gridsome project

1. `gridsome create my-blog https://github.com/noxify/gridsome-starter-casper-v3` to install gridsome with this starter
2. `cd my-blog` to open the folder
3. `gridsome develop` to start a local dev server at `http://localhost:8080`
4. Happy coding 🎉🙌
