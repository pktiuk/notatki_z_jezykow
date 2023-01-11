## Hugo

Hugo is a static site generator written in Go. It is designed to be fast and easy to use, and it can generate a static website from source files written in Markdown, HTML, and other formats.

The structure of a Hugo project typically includes the following elements:

    Configuration file: The configuration file (usually named config.toml, config.yaml, or config.json) contains settings for the site, such as the title, author, and base URL.

    Content: The content for the site is stored in the content directory. It is organized into subdirectories by content type, such as post for blog posts and page for standalone pages. Each content file contains front matter at the top, which is a block of metadata in YAML format that specifies the title, date, and other attributes of the content. The content body follows the front matter, and it can be written in Markdown, HTML, or another format.

    Layout: The layout for the site is stored in the layouts directory. It is organized into subdirectories by content type, and it includes templates for rendering the content. The templates use the Go programming language's template syntax to specify the layout of the content and to insert dynamic elements such as the title and body of the content.

    Static assets: The static assets for the site, such as images, CSS files, and JavaScript files, are stored in the static directory.

    Public: The generated static website is output to the public directory.

In addition to these core elements, a Hugo project may also include custom templates, shortcodes, and other customizations that allow you to tailor the site to your specific needs.

### Dodawanie nowego typu contentu

To define a new type of content called "product" in a Hugo project, you will need to follow these steps:

    Create a new directory in the content directory to store the product content. For example, you can create a product directory:

content
└── product

    In the configuration file, add a new section called product to define the product content type. For example:

```toml
[product]
title = "Product"
singular = "product"
plural = "products"
```

    Create a template for rendering product content in the layouts directory. For example, you can create a product directory and a single.html file in it:

```
layouts
└── product
    └── single.html
```

    In the single.html file, use the Go programming language's template syntax to specify the layout for a single product page. You can use placeholders to insert dynamic elements such as the title and body of the product. For example:

```html
<h1>{{ .Title }}</h1>

<div>{{ .Content }}</div>
```

    Create a new content file for each product you want to add to the site. The content file should be saved in the product directory you created in step 1, and it should include front matter at the top to specify the title, date, and other attributes of the product. For example:

```
content
└── product
    └── my-product.md
```

```
---
title: "My Product"
date: 2021-01-01
---

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis auctor, elit a feugiat fermentum, nisi nunc tempus tellus, id facilisis diam enim et nisl. In hac habitasse platea dictumst.
```

That's it! You have now created a new content type called "product" and added a product to your Hugo site. You can repeat these steps to add more products to the site.

Note that these are just basic steps to get you started with creating a new content type in Hugo. There are many other options and customizations you can use to tailor the content type and the templates to your specific needs. You can find more information about these options in the Hugo documentation.
