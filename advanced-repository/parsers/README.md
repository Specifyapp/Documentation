---
description: >-
  Parsers are functions allowing you to transform design tokens and assets
  coming from Specify to fit your needs and company standards.
---

# Parsers

Not familiar with parsers? Head over to the existing parsers documentation and learn more about why you need them and how to use them.

{% hint style="info" %}
We're currently working on making [our existing parsers](../../concepts/parsers.md#all-parsers-available) compatible with the SDTF. We'll update this page accordingly.
{% endhint %}

## General properties

You must set a name and your desired output for each parser:

1. The `name` is the name of the parser
2. The `output` property indicates which type of output you want the parser to produce

### Output types

Parsers support none, some or more output types, please refer to dedicated parser pages for details.

#### File

Use case: the parser is expected to produce exactly one file.

```typescript
type FileOutput = {
  type: 'file';
  filePath: string;
}
```

**Directory**

Use case: the parser is expected to produce 0 to N files, all placed in the given `directoryPath`.

```typescript
type DirectoryOutput = {
  type: 'directory';
  directoryPath: string;
}
```

Example with the `to-css-custom-properties` parser:

```json
"parsers": [
  {
    "name": "to-css-custom-properties",
    "output": {
      "type": "file",
      "filePath": "style.css"
    }
  }
  // ...
]
```

## Available parsers



<table data-full-width="true"><thead><tr><th width="264">Parser</th><th width="586.3333333333334">Description</th><th>Usage example</th></tr></thead><tbody><tr><td><a href="change-case.md">change-case</a></td><td>This parser helps you change the case of names or modes over a SDTF graph.</td><td><a href="change-case.md#basic-usage">Example</a></td></tr><tr><td><a href="convert-color.md">convert-color</a></td><td>This parser helps you convert the color formats of color compatible tokens over a SDTF graph.</td><td><a href="convert-color.md#basic-usage">Example</a></td></tr><tr><td><a href="filter.md">filter</a></td><td>This parser helps you filter a SDTF graph.</td><td><a href="filter.md#basic-usage-select-all-tokens-from-a-group-in-a-collection">Example</a></td></tr><tr><td><a href="select-modes.md">select-modes</a></td><td>This parser helps you select design tokens from specific mode(s).</td><td><a href="select-modes.md#basic-usage-select-all-tokens-from-a-mode-named-light">Example</a></td></tr><tr><td><a href="to-css-custom-properties.md">to-css-custom-properties</a></td><td>This parser helps you transform design tokens in CSS Custom Properties.</td><td><a href="to-css-custom-properties.md#basic-usage">Example</a></td></tr><tr><td><a href="to-sdtf.md">to-sdtf</a></td><td>This parser helps you get your design tokens as a SDTF graph in JSON.</td><td><a href="to-sdtf.md#basic-usage">Example</a></td></tr><tr><td><a href="to-style-dictionary.md">to-style-dictionary</a></td><td>This parser helps you generate <a href="https://amzn.github.io/style-dictionary/#/">Style Dictionary</a> raw token files for all your design tokens coming from Specify.</td><td><a href="to-style-dictionary.md#basic-usage">Example</a></td></tr><tr><td><a href="to-tailwind.md">to-tailwind</a></td><td>This parser helps you generate a Tailwind theme from all your design tokens coming from Specify.</td><td><a href="to-tailwind.md#basic-usage">Example</a></td></tr></tbody></table>
