---
description: >-
  This parser helps you pull design tokens in JSON with token values in JSON or
  CSS.
---

# to-json

## **Interface**

```typescript
interface parser {
  name: 'to-json';
  output: {
    type: 'file';
    filePath: string;
  };
  options?: {
    output?: 'raw' | 'css';
  };
}
```



## Basic usage - JSON token values

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
      "name": "To JSON",
      "parsers": [
        {
          "name": "to-json",
          "output": {
            "type": "file",
            "filePath": "tokens.json"
          },
          "options": {
            "output": "raw"
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
    "Core": {
      "blue-100": {
        "dark": {
          "model": "rgb",
          "red": 229,
          "green": 29,
          "blue": 29,
          "alpha": 1
        },
        "light": {
          "model": "rgb",
          "red": 255,
          "green": 255,
          "blue": 255,
          "alpha": 1
        }
      },
      "blue-700": {
        "dark": {
          "model": "rgb",
          "red": 229,
          "green": 0,
          "blue": 0,
          "alpha": 1
        },
        "light": {
          "model": "rgb",
          "red": 255,
          "green": 200,
          "blue": 255,
          "alpha": 1
        }
      }
    },
    "semantic": {
      "background": {
        "button": {
          "primary": {
            "hover": {
              "dark": {
                "model": "rgb",
                "red": 229,
                "green": 29,
                "blue": 29,
                "alpha": 1
              },
              "light": {
                "model": "rgb",
                "red": 255,
                "green": 200,
                "blue": 255,
                "alpha": 1
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

## Advanced usage - CSS token values

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
      "name": "To JSON",
      "parsers": [
        {
          "name": "to-json",
          "output": {
            "type": "file",
            "filePath": "tokens.json"
          },
          "options": {
            "output": "css"
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
    "Core": {
      "blue-100": {
        "dark": "rgb(229, 29, 29)",
        "light": "rgb(255, 255, 255)"
      },
      "blue-700": {
        "dark": "rgb(229, 0, 0)",
        "light": "rgb(255, 200, 255)"
      }
    },
    "semantic": {
      "background": {
        "button": {
          "primary": {
            "hover": {
              "dark": "rgb(229, 29, 29)",
              "light": "rgb(255, 200, 255)"
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
