---
description: This parser helps you transform design tokens in CSS Custom Properties.
---

# to-css-custom-properties

## Interface

```typescript
interface parser {
  name: 'to-css-custom-properties';
  output: Partial<{
    type: string;
    filePath: string;
  }>;
  options?: Partial<{
    tokenNameTemplate?: string;
    selectorTemplate?: string;
  }>;
}
```

## Options

<table data-full-width="true"><thead><tr><th width="224">Parameter</th><th width="101">Required</th><th width="105">Type</th><th>Default</th><th>Description</th></tr></thead><tbody><tr><td><code>selectorTemplate</code></td><td>optional</td><td><code>string</code></td><td></td><td>The pattern used to generate the CSS selector name(s). It must match <a href="https://github.com/janl/mustache.js#templates">mustache</a> template syntax.<br><br>You can use <code>collection</code>, <code>mode</code> and <code>groups</code> names.</td></tr><tr><td><code>tokenNameTemplate</code></td><td>optional</td><td><code>string</code></td><td></td><td>The pattern used to generate token names. It must match <a href="https://github.com/janl/mustache.js#templates">mustache</a> template syntax.<br><br>You can use <code>collection</code>, <code>mode</code>,<code>groups</code> and <code>token</code> names.</td></tr></tbody></table>

## Basic usage

A design token can have modes, be nested in groups and be part of a collection. The following use case will generate a single CSS file containing core tokens and semantic tokens.

{% tabs %}
{% tab title="Input" %}
```json
{
  "colors": {
    "$collection": { "$modes": ["light", "dark"] },
    "Core": {
      "blue-100": {
        "$type": "color",
        "$description": "token 1 aliased with n modes within collection within n groups",
        "$value": {
          "light": {
            "red": 255,
            "blue": 255,
            "alpha": 1,
            "green": 255,
            "model": "rgb"
          },
          "dark": {
            "red": 229,
            "blue": 29,
            "alpha": 1,
            "green": 29,
            "model": "rgb"
          }
        }
      },
      "blue-700": {
        "$type": "color",
        "$description": "token 2 aliased with n modes within collection within n groups",
        "$value": {
          "light": {
            "red": 255,
            "blue": 255,
            "alpha": 1,
            "green": 200,
            "model": "rgb"
          },
          "dark": {
            "red": 229,
            "blue": 0,
            "alpha": 1,
            "green": 0,
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
                "dark": {
                  "$mode": "dark",
                  "$alias": "colorszszszs.Core.blue-100"
                },
                "light": {
                  "$mode": "light",
                  "$alias": "colorszszszs.Core.blue-700"
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
{% endtab %}

{% tab title="Config" %}
```json
{
    "name": "css",
    "parsers": [
        {
            "name": "to-css-custom-properties",
            "output": {
                "type": "file",
                "filePath": "tokens.css"
            },
            "options": {
                "tokenNameTemplate": "--{{groups}}-{{token}}",
                "selectorTemplate": "[data-theme=\"{{mode}}\"]"
            }
        }
    ]
}
```
{% endtab %}

{% tab title="Output" %}
```css
/* tokens.css */
[data-theme="dark"] {
  --Core-blue-100: rgb(229, 29, 29);
  --Core-blue-700: rgb(229, 0, 0);
  --semantic-background-button-primary-hover: var(--Core-blue-100);
}
[data-theme="light"] {
  --Core-blue-100: rgb(255, 255, 255);
  --Core-blue-700: rgb(255, 200, 255);
  --semantic-background-button-primary-hover: var(--Core-blue-700);
}
```
{% endtab %}
{% endtabs %}
