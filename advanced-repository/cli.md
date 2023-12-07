---
description: >-
  In this guide you’ll learn how to transform design data coming from Figma
  Variables, Figma Styles and/or Tokens Studio into CSS Custom Properties using
  the Specify CLI.
---

# CLI & Config

## 1. Install the CLI

Install the `@specifyapp/cli` via npm.

{% tabs %}
{% tab title="NPM" %}
```bash
npm install @specifyapp/cli 
```
{% endtab %}
{% endtabs %}

## 2. Create your Specify configuration file

&#x20;To create your Specify config file, you need to follow these steps:

* Create an empty file named `.specifyrc.json`
* Add the following content

{% tabs %}
{% tab title="JSON" %}
{% code lineNumbers="true" %}
```json
{
  "version": "2",
  "repository": "@organization/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "CSS Styles",
      "parsers": [
        {
          "name": "to-css-custom-properties",
          "output": {
            "type":"file",
            "filePath": "style.css"
          }
        }
      ]
    },
    {
      "name": "Raw SDTF",
      "parsers": [
        {
          "name": "to-sdtf",
          "output": {
            "type":"file",
            "filePath": "raw.json"
          }
        }
      ]
    }
  ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% file src="../.gitbook/assets/specifyrc.json" %}

## 3. Properties to update in the configuration file before using it:

* A property `version` is shown which refers to the new Advanced Repository from which we are extracting tokens. Use the `version: "2"`.
* Add your organization and repository name under the `repository` property.
* Get a personal access token [here ↗︎](https://specifyapp.com/user/personal-access-tokens).
* Run the command `specify pull` to fetch your design tokens.

## 4. CSS output example

Specify exports your Figma Variables Modes as CSS data-attributes:

{% tabs %}
{% tab title="CSS" %}
```css
:root[data-Colors="Dark"] {
  --Core-Label-blue-base: rgb(96, 168, 250);
  --Aliases-Icon-info: var(--Core-Label-blue-base);
  --Core-Label-red-base: rgb(221, 72, 64);
  --Aliases-Icon-error: var(--Core-Label-red-base);
  --Core-Neutral-neutral-6: rgb(174, 178, 183);
  --Aliases-Icon-default: var(--Core-Neutral-neutral-6);
  --Core-Label-green-base: rgb(125, 216, 121);
  --Aliases-Icon-success: var(--Core-Label-green-base);
  --Core-Label-orange-base: rgb(255, 158, 41);
  --Aliases-Icon-warning: var(--Core-Label-orange-base);
  --Core-Neutral-neutral-3: rgb(68, 71, 75);
  --Aliases-Icon-disabled: var(--Core-Neutral-neutral-3);
  --Core-Primary-app-base: rgb(98, 77, 227);
  --Aliases-Icon-selected: var(--Core-Primary-app-base);
}
:root[data-Dimensions="Mobile"] {
  --Base-dimension-02: 2px;
  --Radii-radius-01: var(--Base-dimension-02);
  --Base-dimension-08: 8px;
  --Radii-radius-02: var(--Base-dimension-08);
  --Base-dimension-04: 4px;
  --Base-dimension-12: 12px;
  --Base-dimension-16: 16px;
  --Base-dimension-24: 24px;
  --Base-dimension-32: 32px;
  --Spacings-spacing-01: var(--Base-dimension-02);
  --Spacings-spacing-02: var(--Base-dimension-04);
  --Spacings-spacing-03: var(--Base-dimension-12);
  --Spacings-spacing-04: var(--Base-dimension-16);
}
:root[data-Dimensions="Desktop"] {
  --Base-dimension-02: 2px;
  --Radii-radius-01: var(--Base-dimension-02);
  --Base-dimension-08: 8px;
  --Radii-radius-02: var(--Base-dimension-08);
  --Base-dimension-04: 4px;
  --Base-dimension-12: 12px;
  --Base-dimension-16: 16px;
  --Base-dimension-24: 24px;
  --Base-dimension-32: 32px;
  --Spacings-spacing-01: var(--Base-dimension-04);
  --Spacings-spacing-02: var(--Base-dimension-08);
  --Spacings-spacing-03: var(--Base-dimension-12);
  --Spacings-spacing-04: var(--Base-dimension-16);
}
```
{% endtab %}
{% endtabs %}

We would like to improve this output according to your needs as much as we can. Feel free to share your feedback with us via:

* [The community ↗ ](https://feedback.specifyapp.com/beta-program)
* The in-app chat

{% hint style="info" %}
**Things to take into account when using the CLI**\


* The configuration file can handle MJS, CJS, and JSON.
* There is no more `path` property in the parser settings, it is now replaced by an `output` key inside every parser.
{% endhint %}

