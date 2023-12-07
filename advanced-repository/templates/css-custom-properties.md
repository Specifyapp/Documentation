---
description: >-
  This template is dedicated for Web developers using CSS. It helps you generate
  all types of design tokens as CSS Custom Properties in their respective CSS
  file.
---

# CSS Custom Properties

This example uses four different parsers:

* [filter](https://docs.specifyapp.com/sdtf-beta/parsers/filter) to target on a specific collection named "Colors" that contains our colors
* [convert-color](https://docs.specifyapp.com/sdtf-beta/parsers/convert-color) to convert our colors in HSL
* [change-case](../parsers/change-case.md) to change the name of our tokens and modes to kebabCase
* [to-css-custom-properties](https://docs.specifyapp.com/sdtf-beta/parsers/to-css-custom-properties) to generate a CSS file containing our tokens

This template is an example among others. Head toward the [to-css-custom-properties](https://docs.specifyapp.com/sdtf-beta/parsers/to-css-custom-properties) page to get all available options.&#x20;

{% tabs %}
{% tab title="config.json (CLI)" %}
If you use the CLI, you need to fill three properties:

* `repository`  is `@organization/repository`
* `personalAccessToken` which you can generate [in your account settings](https://specifyapp.com/user/personal-access-tokens)&#x20;
* `rules` lets you transform tokens by chaining parsers

```json
{
  "version": "2",
  "repository": "@organization/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "css",
      "parsers": [
        {
          "name": "filter",
          "options": {
            "query": {
              "where": {
                "collection": "Colors",
                "select": {
                  "parents": true,
                  "children": true
                }
              }
            }
          }
        },
        {
          "name": "convert-color",
          "options": {
            "toFormat": "hsl",
            "applyTo": {
              "collection": true
            }
          }
        },
        {
          "name": "change-case",
          "options": {
            "change": "names",
            "toCase": "kebabCase",
            "applyTo": {
              "collection": true
            }
          }
        },
        {
          "name": "change-case",
          "options": {
            "change": "modes",
            "toCase": "kebabCase",
            "applyTo": {
              "collection": true
            }
          }
        },
        {
          "name": "to-css-custom-properties",
          "output": {
            "type": "file",
            "filePath": "tokens.css"
          }
        }
      ]
    }
  ]
}
```
{% endtab %}

{% tab title="config.json (GitHub)" %}
If you use the GitHub, you need to fill two properties:

* `repository`  is `@organization/repository`
* `rules` lets you transform tokens by chaining parsers

{% hint style="info" %}
Make sure you have connected your GitHub account with your Specify account. Head toward [this article](https://help.specifyapp.com/en/articles/4722440-add-github-as-a-destination) to learn more.
{% endhint %}

```json
{
  "version": "2",
  "repository": "@organization/repository",
  "rules": [
    {
      "name": "css",
      "parsers": [
        {
          "name": "filter",
          "options": {
            "query": {
              "where": {
                "collection": "Colors",
                "select": {
                  "parents": true,
                  "children": true
                }
              }
            }
          }
        },
        {
          "name": "convert-color",
          "options": {
            "toFormat": "hsl",
            "applyTo": {
              "collection": true
            }
          }
        },
        {
          "name": "change-case",
          "options": {
            "change": "names",
            "toCase": "kebabCase",
            "applyTo": {
              "collection": true
            }
          }
        },
        {
          "name": "change-case",
          "options": {
            "change": "modes",
            "toCase": "kebabCase",
            "applyTo": {
              "collection": true
            }
          }
        },
        {
          "name": "to-css-custom-properties",
          "output": {
            "type": "file",
            "filePath": "tokens.css"
          }
        }
      ]
    }
  ]
}
```
{% endtab %}
{% endtabs %}
