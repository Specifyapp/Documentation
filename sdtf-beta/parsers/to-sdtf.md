---
description: This parser helps you get your design tokens as a SDTF graph in JSON.
---

# to-sdtf

## **Interface**

```typescript
interface parser {
  name: 'to-sdtf';
  output: Partial<{
    type: string;
    filePath: string;
  }>;
}
```



## Basic usage

{% tabs %}
{% tab title="Input" %}
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
{% endtab %}

{% tab title="Config" %}
```json
{
    "name": "SDTF",
    "parsers": [
        {
            "name": "to-sdtf",
            "output": {
                "type": "file",
                "filePath": "tokens.json"
            }
        }
    ]
}
```
{% endtab %}

{% tab title="Output" %}
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
{% endtab %}
{% endtabs %}
