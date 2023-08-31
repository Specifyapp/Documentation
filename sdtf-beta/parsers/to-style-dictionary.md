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
  output: Partial<{
    type: string;
    directoryPath: string;
  }>;
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
            "name": "to-style-dictionary",
            "output": {
                "type": "directory",
                "directoryPath": "output"
            }
        }
    ]
}
```
{% endtab %}

{% tab title="Output" %}
```javascript
// color/light/Core.json
{
  "colors": {
    "color": {
      "light": {
        "Core": {
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

// color/dark/core.json
{
  "colors": {
    "color": {
      "dark": {
        "Core": {
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

//color/light/semantic.json
{
  "colors": {
    "color": {
      "light": {
        "semantic": {
          "background": {
            "button": {
              "primary": {
                "hover": {
                  "value": "{colors.color.light.Core.blue-700}",
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

//color/dark/semantic.json
{
  "colors": {
    "color": {
      "dark": {
        "semantic": {
          "background": {
            "button": {
              "primary": {
                "hover": {
                  "value": "{colors.color.dark.Core.blue-100}",
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
{% endtab %}
{% endtabs %}