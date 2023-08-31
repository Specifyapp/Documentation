---
description: >-
  In this guide you’ll learn how to transform design data coming from Figma
  Variables and/or Tokens Studio into CSS Custom Properties using the Specify
  CLI.
---

# CLI & Config

## 1. Install the @beta CLI

Install the `@specifyapp/cli@beta` via npm.

{% tabs %}
{% tab title="NPM" %}
```bash
npm install @specifyapp/cli@beta 
```
{% endtab %}
{% endtabs %}

## 2. Create your Specify configuration file

Since the feature is in beta we do not have a command yet to create a config file - as we do on the base Specify platform. Therefore, for now, you need to follow these steps:

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
          "name": "as-is",
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

* A property `version` is shown which refers to the new repository in beta from which we are extracting tokens. Use the `version: "2"` for the beta.
* Add your organization and repository name under the `repository` property.
* Get a personal access token [here ↗︎](https://specifyapp.com/user/personal-access-tokens).
* Run the command `specify pull` to fetch your design tokens.

{% hint style="info" %}
When an error occurs, please make sure to check your collection, group and variable names in the Figma file. Generating CSS variables with the CLI is not possible when spaces are included in the names.
{% endhint %}

## 4. CSS output example

Specify exports your Figma Variables Modes as CSS data-attributes:

{% tabs %}
{% tab title="CSS" %}
```css
:root[data-Colors="Dark"] {
  --Colors-Core-Label-blue-base: rgb(96, 168, 250);
  --Colors-Aliases-Icon-info: var(--Colors-Core-Label-blue-base);
  --Colors-Core-Label-red-base: rgb(221, 72, 64);
  --Colors-Aliases-Icon-error: var(--Colors-Core-Label-red-base);
  --Colors-Core-Neutral-neutral-6: rgb(174, 178, 183);
  --Colors-Aliases-Icon-default: var(--Colors-Core-Neutral-neutral-6);
  --Colors-Core-Label-green-base: rgb(125, 216, 121);
  --Colors-Aliases-Icon-success: var(--Colors-Core-Label-green-base);
  --Colors-Core-Label-orange-base: rgb(255, 158, 41);
  --Colors-Aliases-Icon-warning: var(--Colors-Core-Label-orange-base);
  --Colors-Core-Neutral-neutral-3: rgb(68, 71, 75);
  --Colors-Aliases-Icon-disabled: var(--Colors-Core-Neutral-neutral-3);
  --Colors-Core-Primary-app-base: rgb(98, 77, 227);
  --Colors-Aliases-Icon-selected: var(--Colors-Core-Primary-app-base);
}
:root[data-Dimensions="Mobile"] {
  --Dimensions-Base-dimension-02: 2px;
  --Dimensions-Radii-radius-01: var(--Dimensions-Base-dimension-02);
  --Dimensions-Base-dimension-08: 8px;
  --Dimensions-Radii-radius-02: var(--Dimensions-Base-dimension-08);
  --Dimensions-Base-dimension-04: 4px;
  --Dimensions-Base-dimension-12: 12px;
  --Dimensions-Base-dimension-16: 16px;
  --Dimensions-Base-dimension-24: 24px;
  --Dimensions-Base-dimension-32: 32px;
  --Dimensions-Spacings-spacing-01: var(--Dimensions-Base-dimension-02);
  --Dimensions-Spacings-spacing-02: var(--Dimensions-Base-dimension-04);
  --Dimensions-Spacings-spacing-03: var(--Dimensions-Base-dimension-12);
  --Dimensions-Spacings-spacing-04: var(--Dimensions-Base-dimension-16);
}
:root[data-Dimensions="Desktop"] {
  --Dimensions-Base-dimension-02: 2px;
  --Dimensions-Radii-radius-01: var(--Dimensions-Base-dimension-02);
  --Dimensions-Base-dimension-08: 8px;
  --Dimensions-Radii-radius-02: var(--Dimensions-Base-dimension-08);
  --Dimensions-Base-dimension-04: 4px;
  --Dimensions-Base-dimension-12: 12px;
  --Dimensions-Base-dimension-16: 16px;
  --Dimensions-Base-dimension-24: 24px;
  --Dimensions-Base-dimension-32: 32px;
  --Dimensions-Spacings-spacing-01: var(--Dimensions-Base-dimension-04);
  --Dimensions-Spacings-spacing-02: var(--Dimensions-Base-dimension-08);
  --Dimensions-Spacings-spacing-03: var(--Dimensions-Base-dimension-12);
  --Dimensions-Spacings-spacing-04: var(--Dimensions-Base-dimension-16);
}
```
{% endtab %}
{% endtabs %}

We would like to improve this output according to your needs as much as we can. Feel free to share your feedback with us via:

* [The community ↗ ](https://feedback.specifyapp.com/beta-program)
* The in-app chat

{% hint style="info" %}
**Things to take into account when using the beta CLI**\


* The configuration file can handle MJS, CJS, and JSON.
* You can no longer specify token types inside the Configuration File (`filter.types` property).
* You can’t synchronize design tokens from the CLI (with the `sync` command) when using the version `“2"`.
* There is no more `path` property in the parser settings, it is now replaced by an `output` key inside every parser.
* There’s no template yet.
* There are 2 parsers available:
  * `to-css-custom-properties` that can only return [Figma Variables available types](https://help.figma.com/hc/en-us/articles/14506821864087/) (only Colors and Dimensions for now).
  * `as-is` that returns your design token graph in JSON\

{% endhint %}

