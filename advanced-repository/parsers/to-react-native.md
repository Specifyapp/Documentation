---
description: >-
  This parser helps you pull design tokens as a theme compatible with React
  Native and their respective helper functions.
---

# to-react-native

## **Interface**

```typescript
interface parser {
  name: 'to-react-native';
  output: {
    type: 'file';
    filePath: string;
  };
  options?: {
    typescript?: boolean;
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
      "name": "To React Native theme",
      "parsers": [
        {
          "name": "to-react-native",
          "output": {
            "type": "file",
            "filePath": "public/theme.js"
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
```javascript
/** 
* @typedef {'primitive.spacing.1'} DimensionPath - All the valid paths for the tokens of type dimension.
* To use this type you can do: `@type {import('path/to/myTokensFile').DimensionPath}`
*/
/** 
* @typedef {'themedColor.highEmphasis'} ColorPath - All the valid paths for the tokens of type color.
* To use this type you can do: `@type {import('path/to/myTokensFile').ColorPath}`
*/
/**
* @typedef {DimensionPath | ColorPath} AllPath - All possible paths
*/
/**
* @typedef {typeof pathsByType} PathsByType - All the paths for a given token type. Needed for `getTokensByType`
*/
const pathsByType = /** @type {const} */ ({
  dimension: [ 'primitive.spacing.1' ],
  color: [ 'themedColor.highEmphasis' ]
});

/**
* @typedef {typeof colorModes[number]} ColorModes - All the valid modes of color.
* To use this type you can do: `@type {import('path/to/myTokensFile').ColorModes}`
*/
export const colorModes = /** @type {const} */ ([ 'dark', 'light' ]);

/**
* @typedef {typeof themedColorModes[number]} ThemedcolorModes - All the valid modes of themedColor.
* To use this type you can do: `@type {import('path/to/myTokensFile').ThemedcolorModes}`
*/
export const themedColorModes = /** @type {const} */ ([ 'light', 'dark' ]);

/**
@typedef {ColorModes | ThemedcolorModes} AllMode - All the available modes
*/

/** 
* @typedef {typeof tokens} Tokens - All the tokens. 
* Use `getTokenByMode` to retrieve one. 
*/
export const tokens = /** @type {const} */ ({
  'primitive.spacing.1': '4px',
  'themedColor.highEmphasis': { dark: '#ffffff', light: '#000000' }
});

/**
* Retrieve any token for a given mode. If available, the default mode will be: 'default'
* @template {AllPath} Path - A generic extending all the possible paths
* @template {Tokens[Path] extends Record<string, any>
    ? keyof Tokens[Path]
    : undefined} Mode - A generic representing all the valid modes for a given path
* @template {Tokens[Path] extends Record<string, any>
    ? Tokens[Path][Mode extends undefined ? never : Mode]
    : Tokens[Path]} Return - The return type
* @param {Path} path - The path to the token
* @param {Mode} mode - The mode of the token you want to retrieve 
* @returns {Return} - The value of a token for a given mode
*/
export function getTokenByMode(path, mode) {
  if (!tokens[path]) {
    throw new Error("Path: '" + path + "' doesn't exist. Here are all the valid paths:\n- " + Object.keys(tokens).join('\n- '))
  }

  if (typeof tokens[path] !== 'object') {
    return tokens[path] ;
  }

  if (!mode) throw new Error('Mode is undefined but it should be one of ' + Object.keys(tokens[path]).join(', ') + ' for path: ' + path);

  if (!tokens[path][mode]) {
    throw new Error("Invalid mode '" + mode.toString() + " at path '" + path + "', here are all the valid modes:\n- " + Object.keys(tokens[path]).join('\n- '))
  } 

  return tokens[path][mode]  
}

/**
* Retrieve all the tokens for a specific type (color, dimension, etc...).
* Note that the value will either be a string or an object if the token has modes
* @template {keyof PathsByType} Type - A generic extending all the possible types
* @template {Tokens[PathsByType[Type][number]]} Token - A generic representing a union of all the outputs
* @param {Type} type - The path to the token
* @returns {Array<Token>} - An array with all the values
*/
export function getTokensByType(type) {
  if (!pathsByType[type]) {
    throw new Error('The type: \'' + type + '\' does not exist')
  }

  return pathsByType[type].map(path => tokens[path]);
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
