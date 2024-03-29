---
description: This parser helps you get your design tokens as a SDTF graph in JSON.
---

# to-sdtf

## **Interface**

```typescript
interface parser {
  name: 'to-sdtf';
  output:
    | { type: 'directory'; directoryPath: string }
    | { type: 'file'; filePath: string }
    | { type: 'SDTF' }
    | { type: 'text' }
    | { type: 'JSON'; filePath: string };
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
      "name": "Generate tokens in JSON",
      "parsers": [
        {
          "name": "to-sdtf",
          "output": {
            "type": "file",
            "filePath": "output/tokens.json"
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
{% code title="tokens.json" lineNumbers="true" %}
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
{% endtabs %}
