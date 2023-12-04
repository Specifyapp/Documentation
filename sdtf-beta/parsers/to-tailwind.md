---
description: >-
  This parser helps you generate a Tailwind theme from all your design tokens
  coming from Specify.
---

# to-tailwind

Unlike the existing to-tailwind parser, this one doesn't have any options yet.

## Interface

```typescript
interface parser {
  name: 'to-tailwind';
  output: {
    type: 'file';
    filePath: string; // e.g theme.js
  };
}
```

## Basic usage

{% tabs %}
{% tab title="Input" %}
{% code lineNumbers="true" %}
```json
{
  "colors": {
    "$collection": {
      "$modes": [
        "light",
        "dark"
      ]
    },
    "aliases": {
      "border": {
        "active": {
          "$type": "color",
          "$value": {
            "dark": {
              "$alias": "colors.core.label.blue-base",
              "$mode": "dark"
            },
            "light": {
              "$alias": "colors.core.label.blue-base",
              "$mode": "light"
            }
          }
        }
      }
    },
    "core": {
      "label": {
        "blue-base": {
          "$type": "color",
          "$value": {
            "dark": {
              "model": "rgb",
              "red": 96,
              "green": 168,
              "blue": 250,
              "alpha": 1
            },
            "light": {
              "model": "rgb",
              "red": 17,
              "green": 125,
              "blue": 249,
              "alpha": 1
            }
          }
        },
        "blue-lighter": {
          "$type": "color",
          "$value": {
            "dark": {
              "model": "rgb",
              "red": 41,
              "green": 52,
              "blue": 67,
              "alpha": 1
            },
            "light": {
              "model": "rgb",
              "red": 219,
              "green": 236,
              "blue": 254,
              "alpha": 1
            }
          }
        }
      }
    }
  },
  "dimensions": {
    "$collection": {
      "$modes": [
        "desktop",
        "mobile"
      ]
    },
    "base": {
      "dimension-01": {
        "$type": "dimension",
        "$value": {
          "mobile": {
            "value": 2,
            "unit": "px"
          },
          "desktop": {
            "value": 4,
            "unit": "px"
          }
        }
      },
      "dimension-02": {
        "$type": "dimension",
        "$value": {
          "mobile": {
            "value": 4,
            "unit": "px"
          },
          "desktop": {
            "value": 8,
            "unit": "px"
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
      "name": "Generate tokens as a Tailwind theme",
      "parsers": [
        {
          "name": "to-tailwind",
          "output": {
            "type": "file",
            "filePath": "theme.js"
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
{% code title="theme.js" lineNumbers="true" %}
```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  theme: {
    extend: {
      colors: {
        colors: {
          core: {
            label: {
              'blue-lighter': {
                'dark': 'rgb(41, 52, 67)',
                'light': 'rgb(219, 236, 254)'
              },
              'blue-base': {
                'dark': 'rgb(96, 168, 250)',
                'light': 'rgb(17, 125, 249)'
              }
            }
          },
          aliases: {
            border: {
              active: {
                'dark': 'rgb(98, 77, 227)',
                'light': 'rgb(235, 33, 33)'
              }
            }
          }
        }
      },
      spacing: {
        'dimensions-base-dimension-01-desktop': '4px',
        'dimensions-base-dimension-01-mobile': '2px',
        'dimensions-base-dimension-02-desktop': '8px',
        'dimensions-base-dimension-02-mobile': '4px'
      }
    }
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
