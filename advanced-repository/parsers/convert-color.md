---
description: >-
  This parser helps you convert color formats of color tokens.
---

# convert-color

## Interface

```typescript
interface parser {
  name: 'convert-color';
  options: {
    toFormat:
      | 'hex'
      | 'rgb'
      | 'hsl'
      | 'hsb'
      | 'lch'
      | 'lab';
    applyTo?:
      | { collection: string | true }
      | { group: string | true }
      | { token: string | true }
      | SDTFQuery;
  };
}
```

## Options

<table><thead><tr><th width="186">Parameter</th><th width="127.33333333333331">Required</th><th width="341">Type</th><th width="136">Default</th><th width="237">Description</th></tr></thead><tbody><tr><td><code>toColorFormat</code></td><td>required</td><td><pre class="language-typescript"><code class="lang-typescript">| 'hex' 
| 'rgb' 
| 'hsl' 
| 'hsb' 
| 'lch' 
| 'lab'
</code></pre></td><td></td><td>The target color format to convert to. Actual value conversion is done by the <a href="https://www.npmjs.com/package/colord">colord</a> package.</td></tr><tr><td><code>applyTo</code></td><td>optional</td><td><pre class="language-typescript"><code class="lang-typescript">| { collection: string | true }
| { group: string | true }
| { token: string | true }
| SDTFQuery
</code></pre></td><td><pre><code>{ token: true }
</code></pre></td><td>The selection where to apply the transformation.<br><br><code>collection</code>, <code>group</code>, <code>token</code> take a Regex string or <code>true</code> to select anything of the kind.<br><br>An <code>SDTFQuery</code> can be used for advance use cases.</td></tr></tbody></table>

## Basic usage

{% tabs %}
{% tab title="Input" %}
<pre class="language-json" data-line-numbers><code class="lang-json">{
<strong>  "Colors": {
</strong><strong>    "$collection": { "$modes": ["Light", "Dark"] },
</strong><strong>    "Core": {
</strong><strong>      "blue 100": {
</strong>        "$type": "color",
        "$description": "token 1 aliased with n modes within collection within n groups",
        "$value": {
<strong>          "Light": {
</strong>            "red": 219,
            "blue": 254,
            "alpha": 1,
            "green": 236,
            "model": "rgb"
          },
<strong>          "Dark": {
</strong>            "red": 41,
            "blue": 67,
            "alpha": 1,
            "green": 52,
            "model": "rgb"
          }
        }
      },
<strong>      "blue 700": {
</strong>        "$type": "color",
        "$description": "token 2 aliased with n modes within collection within n groups",
        "$value": {
<strong>          "Light": {
</strong>            "red": 17,
            "blue": 249,
            "alpha": 1,
            "green": 125,
            "model": "rgb"
          },
<strong>          "Dark": {
</strong>            "red": 96,
            "blue": 250,
            "alpha": 1,
            "green": 168,
            "model": "rgb"
          }
        }
      }
    },
<strong>    "semantic": {
</strong><strong>      "background": {
</strong><strong>        "button": {
</strong><strong>          "primary": {
</strong><strong>            "hover": {
</strong>              "$type": "color",
              "$description": "alias token with n modes within collection within n groups",
              "$value": {
<strong>                "Dark": {
</strong><strong>                  "$mode": "dark",
</strong><strong>                  "$alias": "Colors.Core.blue 100"
</strong>                },
<strong>                "Light": {
</strong><strong>                  "$mode": "light",
</strong><strong>                  "$alias": "Colors.Core.blue 700"
</strong>                }
              }
            }
          }
        }
      }
    }  
  }
}
</code></pre>
{% endtab %}

{% tab title="Config" %}
We convert all colors from our SDTF graph in `hsl`.

We then generate our transformed SDTF graph in a JSON file thanks to the [to-sdtf](to-sdtf.md) parser.

{% code title=".specifyrc.json" lineNumbers="true" %}
```json5
{
  "version": "2",
  "repository": "@organization/repository",
  // Only use the personalAccessToken when working with the CLI
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Convert colors in HSL and generate tokens in JSON",
      "parsers": [
        {
          "name": "convert-color",
          "options": {
            "toFormat": "hsl"
          }
        },
        {
          "name": "to-sdtf",
          "output": {
            "type": "file",
            "filePath": "tokens.json"
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
<pre class="language-json" data-title="tokens.json" data-line-numbers><code class="lang-json">{
<strong>  "colors": {
</strong><strong>    "$collection": { "$modes": ["light", "dark"] },
</strong><strong>    "core": {
</strong><strong>      "blue-100": {
</strong>        "$type": "color",
        "$description": "token 1 aliased with n modes within collection within n groups",
        "$value": {
<strong>          "light": {
</strong>            "model": "hsl",
            "hue": 211,
            "saturation": 95,
            "lightness": 93,
            "alpha": 1
          },
<strong>          "dark": {
</strong>            "model": "hsl",
            "hue": 215,
            "saturation": 24,
            "lightness": 21,
            "alpha": 1
          }
        }
      },
<strong>      "blue-700": {
</strong>        "$type": "color",
        "$description": "token 2 aliased with n modes within collection within n groups",
        "$value": {
<strong>          "light": {
</strong>            "model": "hsl",
            "hue": 212,
            "saturation": 95,
            "lightness": 52,
            "alpha": 1
          },
<strong>          "dark": {
</strong>            "model": "hsl",
            "hue": 212,
            "saturation": 94,
            "lightness": 68,
            "alpha": 1
          }
        }
      }
    },
<strong>    "semantic": {
</strong><strong>      "background": {
</strong><strong>        "button": {
</strong><strong>          "primary": {
</strong><strong>            "hover": {
</strong>              "$type": "color",
              "$description": "alias token with n modes within collection within n groups",
              "$value": {
<strong>                "dark": {
</strong><strong>                  "$mode": "dark",
</strong><strong>                  "$alias": "colors.core.blue-100"
</strong>                },
<strong>                "light": {
</strong><strong>                  "$mode": "light",
</strong><strong>                  "$alias": "colors.core.blue-700"
</strong>                }
              }
            }
          }
        }
      }
    }  
  }
}
</code></pre>
{% endtab %}
{% endtabs %}
