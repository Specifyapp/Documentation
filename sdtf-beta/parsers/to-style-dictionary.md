---
description: >-
  This parser helps you generate Style Dictionary raw token files for all your
  design tokens coming from Specify.
---

# to-style-dictionary

Unlike [the existing to-style-dictionary parser](https://github.com/Specifyapp/parsers/blob/master/parsers/to-style-dictionary), this one doesn't have any options yet.

## Interface

```typescript
interface parser {
  name: 'to-style-dictionary';
  output: {
    type: 'directory';
    directoryPath: string;
  };
}
```

## General output rules

* A collection will generate a folder at the top level
  1. The default level refers to the SDTF Token Type associated SD Category → `{collectionName?}`/`{SDCategory}`
  2. The next folder level is the name of the potential first group containing the token → `{collectionName?}`/`{SDCategory}`/`{1stLevelGroupName?}`
  3. The default filename is the name of the first group, or the name of the each mode the token might have, or `base.json` → `{collectionName?}`/`{SDCategory}`/`{ mode? | 1stLevelGroupName? | base}.json` (priority order for filename: `groupName` > `mode` > `base`)
* The token path inside the file must match the token file path with the following priority order: `collection` > `SDCategoryType` > `Mode` > `Groups`
  * `{collectionName?}`/`{SDCategory}`/`{1stLevelGroupName? | mode? | base}.json` → `{ collection: {type: {mode: { groupName: { tokenName: ... }}}}`

## Basic usage

{% tabs %}
{% tab title="Input" %}
{% code lineNumbers="true" %}
```json
{
  "colors": {
    "$collection": { "$modes": ["light", "dark"] },
    "core": {
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
                  "$alias": "colors.core.blue-100"
                },
                "light": {
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
```json
{
  "version": "2",
  "repository": "@organization/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Generate Style Dictionary raw token files",
      "parsers": [
        {
          "name": "to-style-dictionary",
          "output": {
            "type": "directory",
            "directoryPath": "output/tokens/"
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
{% code title="color/light/core.json" lineNumbers="true" %}
```javascript
{
  "colors": {
    "color": {
      "light": {
        "core": {
          "blue-100": {
            "value": "rgb(255, 255, 255)",
            "type": "color",
            "description": "token 1 aliased with n modes within collection within n groups"
          },
          "blue-700": {
            "value": "rgb(255, 200, 255)",
            "type": "color",
            "description": "token 2 aliased with n modes within collection within n groups"
          }
        }
      }
    }
  }
}
```
{% endcode %}

{% code title="color/dark/core.json" lineNumbers="true" %}
```json
{
  "colors": {
    "color": {
      "dark": {
        "core": {
          "blue-100": {
            "value": "rgb(229, 29, 29)",
            "type": "color",
            "description": "token 1 aliased with n modes within collection within n groups"
          },
          "blue-700": {
            "value": "rgb(229, 0, 0)",
            "type": "color",
            "description": "token 2 aliased with n modes within collection within n groups"
          }
        }
      }
    }
  }
}
```
{% endcode %}

{% code title="color/light/semantic.json" lineNumbers="true" %}
```json
{
  "colors": {
    "color": {
      "light": {
        "semantic": {
          "background": {
            "button": {
              "primary": {
                "hover": {
                  "value": "{colors.color.light.core.blue-700}",
                  "type": "color",
                  "description": "alias token with n modes within collection within n groups"
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
{% endtabs %}

{% hint style="info" %}
Heads toward our [templates section](https://app.gitbook.com/o/4xLRT3v2YVTuAxbYok2F/s/9mLpgMKJql1OpDNVdcbF/\~/changes/159/sdtf-beta/templates) to learn more on how to implement the to-style-dictionary parser within your config file.
{% endhint %}
