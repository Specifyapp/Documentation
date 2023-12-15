---
description: >-
  This parser helps you pull design tokens as TypeScript objects for all token
  types and their respective helper functions.
---

# to-typescript

## **Interface**

```typescript
interface parser {
  name: 'to-typescript';
  output: {
    type: 'file';
    filePath: string;
  };
  options?: {
    moduleExport?: 'es6' | 'commonjs';
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
    "Core": {
      "blue-100": {
        "$type": "color",
        "$value": {
          "dark": {
            "red": 229,
            "blue": 29,
            "alpha": 1,
            "green": 29,
            "model": "rgb"
          },
          "light": {
            "red": 255,
            "blue": 255,
            "alpha": 1,
            "green": 255,
            "model": "rgb"
          }
        },
        "$description": "token 1 aliased with n modes within collection within n groups"
      },
      "blue-700": {
        "$type": "color",
        "$value": {
          "dark": {
            "red": 229,
            "blue": 0,
            "alpha": 1,
            "green": 0,
            "model": "rgb"
          },
          "light": {
            "red": 255,
            "blue": 255,
            "alpha": 1,
            "green": 200,
            "model": "rgb"
          }
        },
        "$description": "token 2 aliased with n modes within collection within n groups"
      }
    },
    "semantic": {
      "background": {
        "button": {
          "primary": {
            "hover": {
              "$type": "color",
              "$value": {
                "dark": {
                  "$mode": "dark",
                  "$alias": "colors.Core.blue-100"
                },
                "light": {
                  "$mode": "light",
                  "$alias": "colors.Core.blue-700"
                }
              },
              "$description": "alias token with n modes within collection within n groups"
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
      "name": "To TypeScript",
      "parsers": [
        {
          "name": "to-typescript",
          "output": {
            "type": "file",
            "filePath": "tokens.ts"
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
{% code title="tokens.js" lineNumbers="true" %}
```typescript
/** 
* @enum {string} All the valid paths for the collection colors.
* Use it when calling `getColorsTokenByMode`
*/
export const colorsColorPath = {
  'colors.Core.blue-100': 'colors.Core.blue-100',
  'colors.Core.blue-700': 'colors.Core.blue-700',
  'colors.semantic.background.button.primary.hover': 'colors.semantic.background.button.primary.hover'
} as const;

export type colorsColorPathType = keyof typeof colorsColorPath;

export type colorsPathType = colorsColorPathType;

/**
* All the modes of the collection colors.
* Use it when calling `getColorsTokenByMode`
*/
export const colorsModes = [ 'light', 'dark' ] as const;

export type colorsModesType = typeof colorsModes[number];

/** 
* All the tokens of the collection colors.
* Use `getColorsTokenByMode` to retrieve the tokens
*/
export const colors = {
  'colors.Core.blue-100': { dark: 'rgb(229, 29, 29)', light: 'rgb(255, 255, 255)' },
  'colors.Core.blue-700': { dark: 'rgb(229, 0, 0)', light: 'rgb(255, 200, 255)' },
  'colors.semantic.background.button.primary.hover': { dark: 'rgb(229, 29, 29)', light: 'rgb(255, 200, 255)' }
} as const;

/**
* Retrieve a token for the collection 'colors'.
* @param {keyof typeof colorsPath} path - The path to the token
* @param {'light' | 'dark'} mode - The mode of the token you want to retrieve 
* @returns {number | string} The value of a token for a given mode
*/
export function getColorsTokenByMode<T extends colorsPathType, M extends keyof typeof colors[T]>(path: T, mode: M) {
  if (!colors[path]) {
    throw new Error("Path: '" + path + "' doesn't exist for collection 'colors'. Here are all the valid paths for each type:" + `
- color:
    - colors.Core.blue-100
    - colors.Core.blue-700
    - colors.semantic.background.button.primary.hover`)
  }

  if (!colors[path][mode]) {
    throw new Error("Invalid mode '" + mode.toString() + "' for collection 'colors' at path '" + path + "', here are all the valid modes:\n- " + Object.keys(colors[path]).join('\n- '))
  }

  return colors[path][mode]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
