---
title: VuePress Markdown syntax
description: VuePress-oriented Markdown rendered by Docusaurus to expose conversion differences.
sidebar_position: 8
---

# VuePress Markdown syntax

This is a `.md` file written in a VuePress-friendly style and rendered by Docusaurus. It is intentionally not a live VuePress site: Vue-specific tags and theme containers are fenced so Docusaurus can display them as examples. Use the version selector to compare **Latest** with the original **1.0.0** docs snapshot. For MDX imports, Docusaurus theme components, an interactive counter, and Swagger UI, open [the paired Docusaurus MDX page](./docusaurus-vuepress.mdx).

## Shared Markdown

Both systems render ordinary headings, paragraphs, **emphasis**, lists, tables, links, images, and fenced code blocks. Front matter is YAML in both, but the fields are interpreted by each system's own configuration and plugins.

| Source | Typical use |
| --- | --- |
| `title: VuePress Markdown syntax` | Page title |
| `## A heading` | Section and anchor |
| `[Docusaurus MDX](./docusaurus-vuepress.mdx)` | Relative document link |

## Page metadata and routes

VuePress front matter can configure the page route and theme behavior. Exact fields depend on the installed VuePress version and theme:

```yaml title="VuePress front matter"
---
title: API overview
permalink: /api/overview.html
lang: en-US
sidebar: auto
sidebarDepth: 2
editLink: true
lastUpdated: true
---
```

Docusaurus uses different fields, such as `id`, `slug`, and `sidebar_position`. This page's source is interpreted using Docusaurus front matter instead, so copying VuePress-only options over does not automatically recreate their behavior.

VuePress commonly permits extensionless links and routes shaped by its theme. Docusaurus links can target doc IDs, relative document files, or configured routes. Verify generated URLs and anchors rather than relying on a blind search-and-replace.

## Images and static files

VuePress serves files from its `public/` directory at the site root; Docusaurus uses `static/`. Both can express a root-relative image URL when the asset is deployed at the same path:

![Workspace-provided image used as a documentation asset](/img/dictionarysorrows.jpg)

```md
![Workspace-provided image](/img/dictionarysorrows.jpg)
```

Relative images colocated with a Markdown document are also common in both ecosystems, but their asset processing and deployment base paths can differ.

```js
const message = 'This common JavaScript fence renders in both systems.';
console.log(message);
```

VuePress themes may also provide warning, danger, and code-group containers. Their names and fence conventions are theme/plugin APIs, not universal Markdown:

````md
::: warning Check the response

The API can return a `404` for an unknown identifier.

:::

::: code-group

```bash [npm]
npm run docs:version 1.0.0
```

```bash [pnpm]
pnpm docs:version 1.0.0
```

:::
````

## VuePress containers

VuePress themes commonly provide custom containers. Some container names overlap with Docusaurus admonitions, while theme-specific containers may render differently or not at all when converted.

:::tip
This familiar tip container is supported by both tools, though its theme styling can differ.
:::

The following VuePress details container is shown as source so Docusaurus can render the syntax literally for comparison:

```md
::: details Click to expand

VuePress themes can render this as a collapsible container.

:::
```

## VuePress components

VuePress resolves registered Vue components in Markdown. Docusaurus uses MDX and React instead, so Vue tags are not drop-in equivalents. These examples remain fenced to avoid treating Vue syntax as MDX JSX:

```md
<Badge type="tip" text="New" />

<VPButton href="/guide/">Explore the guide</VPButton>

<ApiStatus :status="200" />
```

To reproduce these in Docusaurus, use a React/MDX component or a Docusaurus theme component with the corresponding behavior.

The syntax also changes: Vue uses directives and bindings such as `:status="200"` and `v-if`; MDX uses JSX props and JavaScript expressions such as `status={200}` and `{condition && <Note />}`.

## VuePress code blocks

Both render language-highlighted fences. VuePress themes may support extra fence metadata or plugins; Docusaurus-specific title and line-highlight metadata are not guaranteed to transfer.

````md
```js
// VuePress renders this as a highlighted code block.
console.log('Hello from VuePress');
```
````

See [the paired Docusaurus page](./docusaurus-vuepress.mdx#docusaurus-mdx) for imported MDX components, tabs, a live React example, and an embedded Swagger UI explorer.

## API specifications and executable examples

VuePress can host an OpenAPI file as a static asset and render it with a theme component or plugin. There is no single built-in VuePress Swagger tag, so the syntax depends on the integration selected by the site. This project serves the same [OpenAPI demo spec](/openapi/demo.yaml) through Swagger UI embedded by the Docusaurus MDX page.

```yaml
openapi: 3.0.3
info:
	title: Documentation Demo API
	version: 1.0.0
paths:
	/todos/{id}:
		get:
			responses:
				'200':
					description: Todo record
```

Runnable snippets have the same caveat: a highlighted code fence is not automatically executable. Both sites need a component or plugin to run code, and API “Try it out” requests also depend on CORS, authentication, and network access.

## Versioned docs

VuePress does not provide Docusaurus-style versioned docs snapshots by default. Sites commonly maintain versioned branches or directories and configure theme navigation or plugins around them. Here the version dropdown is a Docusaurus feature: it switches between the current **Latest** docs and the preserved **1.0.0** snapshot.