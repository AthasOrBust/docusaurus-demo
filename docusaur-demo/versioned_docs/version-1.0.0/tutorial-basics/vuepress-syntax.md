---
title: VuePress Markdown syntax
description: VuePress-oriented Markdown rendered by Docusaurus to expose conversion differences.
sidebar_position: 8
---

# VuePress Markdown syntax

This is a `.md` file written in a VuePress-friendly style and rendered by Docusaurus. For MDX imports, Docusaurus theme components, an interactive counter, and Swagger UI, open [the paired Docusaurus MDX page](./docusaurus-vuepress.mdx).

## Shared Markdown

Both systems render ordinary headings, paragraphs, **emphasis**, lists, tables, links, images, and fenced code blocks. Front matter is YAML in both, but the fields are interpreted by each system's own configuration and plugins.

| Source | Typical use |
| --- | --- |
| `title: VuePress Markdown syntax` | Page title |
| `## A heading` | Section and anchor |
| `[Docusaurus MDX](./docusaurus-vuepress.mdx)` | Relative document link |

```js
const message = 'This common JavaScript fence renders in both systems.';
console.log(message);
```

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
```

To reproduce these in Docusaurus, use a React/MDX component or a Docusaurus theme component with the corresponding behavior.

## VuePress code blocks

Both render language-highlighted fences. VuePress themes may support extra fence metadata or plugins; Docusaurus-specific title and line-highlight metadata are not guaranteed to transfer.

````md
```js
// VuePress renders this as a highlighted code block.
console.log('Hello from VuePress');
```
````

See [the paired Docusaurus page](./docusaurus-vuepress.mdx#docusaurus-mdx) for imported MDX components, tabs, a live React example, and an embedded Swagger UI explorer.