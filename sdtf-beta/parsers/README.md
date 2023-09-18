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
2. The `output` property is composed of a `type` and a `filePath` or a `directoryPath`.

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



| Parser                                                  | Description                                                                                                                                                   | Usage example                                      |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| [to-sdtf](to-sdtf.md)                                   | This parser helps you get your design tokens as a SDTF graph in JSON.                                                                                         | [Example](to-sdtf.md#basic-usage)                  |
| [to-css-custom-properties](to-css-custom-properties.md) | This parser helps you transform design tokens in CSS Custom Properties.                                                                                       | [Example](to-css-custom-properties.md#basic-usage) |
| [to-style-dictionary](to-style-dictionary.md)           | This parser helps you generate [Style Dictionary](https://amzn.github.io/style-dictionary/#/) raw token files for all your design tokens coming from Specify. | [Example](to-style-dictionary.md#basic-usage)      |
