---
description: This parser helps you transform design tokens into CSS Custom Properties.
---

# to-css-custom-properties

## Interface

```typescript
interface parser {
  name: 'to-css-custom-properties';
  output: {
    type: 'file';
    filePath: string;
  };
  options?: {
    tokenNameTemplate?: string;
    selectorTemplate?: string;
    includeCoreTokensInScopes?: boolean;
  };
}
```

## Options

<table data-full-width="true"><thead><tr><th width="243">Parameter</th><th width="101">Required</th><th width="118">Type</th><th width="119">Default</th><th>Description</th></tr></thead><tbody><tr><td><code>selectorTemplate</code></td><td>optional</td><td><code>string</code></td><td></td><td>The pattern used to generate the CSS selector name(s). It must match <a href="https://github.com/janl/mustache.js#templates">mustache</a> template syntax.<br><br>You can use <code>collection</code>, <code>mode</code> and <code>groups</code> names.</td></tr><tr><td><code>tokenNameTemplate</code></td><td>optional</td><td><code>string</code></td><td></td><td>The pattern used to generate token names. It must match <a href="https://github.com/janl/mustache.js#templates">mustache</a> template syntax.<br><br>You can use <code>collection</code>, <code>mode</code>,<code>groups</code> and <code>token</code> names.</td></tr><tr><td><code>includeCoreTokensInScopes</code></td><td>optional</td><td><code>boolean</code></td><td><code>false</code></td><td>When set to <code>true</code>, you will have both core tokens and alias tokens in each CSS scopes thus making alias tokens always resolvable.</td></tr></tbody></table>

## Basic usage

A design token can have modes, be nested in groups and be part of a collection. The following use case will generate a single CSS file containing core tokens and semantic tokens.

{% tabs %}
{% tab title="Input" %}
{% code lineNumbers="true" %}
```json
{
  "colors": {
    "$collection": { "$modes": ["Light", "Dark"] },
    "core": {
      "blue-100": {
        "$type": "color",
        "$description": "token 1 aliased with n modes within collection within n groups",
        "$value": {
          "Light": {
            "red": 219,
            "blue": 254,
            "alpha": 1,
            "green": 236,
            "model": "rgb"
          },
          "Dark": {
            "red": 41,
            "blue": 67,
            "alpha": 1,
            "green": 52,
            "model": "rgb"
          }
        }
      },
      "blue-700": {
        "$type": "color",
        "$description": "token 2 aliased with n modes within collection within n groups",
        "$value": {
          "Light": {
            "red": 17,
            "blue": 249,
            "alpha": 1,
            "green": 125,
            "model": "rgb"
          },
          "Dark": {
            "red": 96,
            "blue": 250,
            "alpha": 1,
            "green": 168,
            "model": "rgb"
          }
        }
      }
    },
    "semantic": {
      "background": {
        "button": {
          "primary": {
            "hover": {
              "$type": "color",
              "$description": "alias token with n modes within collection within n groups",
              "$value": {
                "Dark": {
                  "$mode": "dark",
                  "$alias": "colors.core.blue-100"
                },
                "Light": {
                  "$mode": "light",
                  "$alias": "colors.core.blue-700"
                }
              }
            }
          }
        }
      }
    }  
  }
}
```
{% endcode %}
{% endtab %}

{% tab title="Config" %}
{% code title=".specifyrc.json" lineNumbers="true" %}
```json5
{
  "version": "2",
  "repository": "@organization/repository",
  // Only use the personalAccessToken when working with the CLI
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Generate tokens as CSS Custom Properties",
      "parsers": [
        {
          "name": "to-css-custom-properties",
          "output": {
            "type": "file",
            "filePath": "tokens.css"
          },
          "options": {
            "tokenNameTemplate": "--{{groups}}-{{token}}",
            "selectorTemplate": "[data-theme=\"{{mode}}\"]",
            "includeCoreTokensInScopes": true
          }
        }
      ]
    }
  ]
}
```
{% endcode %}
{% endtab %}

{% tab title="Output" %}
{% code title="tokens.css" lineNumbers="true" %}
```css
[data-theme="dark"] {
  --core-blue-100: rgb(41, 52, 67);
  --core-blue-700: rgb(96, 168, 250);
  --semantic-background-button-primary-hover: var(--core-blue-100);
}
[data-theme="light"] {
  --core-blue-100: rgb(219, 236, 254);
  --core-blue-700: rgb(17, 125, 249);
  --semantic-background-button-primary-hover: var(--core-blue-700);
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Head towards our [templates section](../templates/css-custom-properties.md) to see how you can use this parser with others to suit a common use case when working with CSS.
{% endhint %}
