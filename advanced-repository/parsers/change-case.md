---
description: This parser helps you change the case of names or modes over a SDTF graph.
---

# change-case

## Interface

```typescript
interface parser {
  name: 'change-case';
  options: {
    change?: 'name' | 'modes';
    toCase:
      | 'camelCase'
      | 'capitalCase'
      | 'constantCase'
      | 'kebabCase'
      | 'noCase'
      | 'pascalCase'
      | 'pascalSnakeCase'
      | 'pathCase'
      | 'sentenceCase'
      | 'snakeCase'
      | 'trainCase';
    applyTo:
      | { collection: string | true }
      | { group: string | true }
      | { token: string | true }
      | SDTFQuery;
  };
}
```

## Options

<table><thead><tr><th width="151">Parameter</th><th width="127.33333333333331">Required</th><th width="341">Type</th><th width="136">Default</th><th width="237">Description</th></tr></thead><tbody><tr><td><code>change</code></td><td>optional</td><td><pre><code>'names' | 'modes'
</code></pre></td><td><code>'names'</code></td><td>Change the names or the modes of the selected items.</td></tr><tr><td><code>toCase</code></td><td>required</td><td><pre class="language-typescript"><code class="lang-typescript">| 'camelCase'
| 'capitalCase'
| 'constantCase'
| 'kebabCase'
| 'noCase'
| 'pascalCase'
| 'pascalSnakeCase'
| 'pathCase'
| 'sentenceCase'
| 'snakeCase'
| 'trainCase'
</code></pre></td><td></td><td>The case transformation to apply. Actual transform is done by the <a href="https://www.npmjs.com/package/change-case">change-case</a> package.</td></tr><tr><td><code>applyTo</code></td><td>required</td><td><pre class="language-typescript"><code class="lang-typescript">| { collection: string | true }
| { group: string | true }
| { token: string | true }
| SDTFQuery
</code></pre></td><td></td><td>The selection where to apply the transformation.<br><br><code>collection</code>, <code>group</code>, <code>token</code> take a Regex string or <code>true</code> to select anything of the kind.<br><br>An <code>SDTFQuery</code> can be used for advance use cases. Learn more about <a href="../querying-a-sdtf-graph.md">how to query your SDTF graph</a>.</td></tr></tbody></table>

## Basic usage

This example helps you transform in `kebabCase` the name all collections, groups, tokens and modes. Use this example if you want to generate CSS Custom properties with the `to-css-custom-properties` parser.

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
</strong>            "red": 255,
            "blue": 255,
            "alpha": 1,
            "green": 255,
            "model": "rgb"
          },
<strong>          "Dark": {
</strong>            "red": 229,
            "blue": 29,
            "alpha": 1,
            "green": 29,
            "model": "rgb"
          }
        }
      },
<strong>      "blue 700": {
</strong>        "$type": "color",
        "$description": "token 2 aliased with n modes within collection within n groups",
        "$value": {
<strong>          "Light": {
</strong>            "red": 255,
            "blue": 255,
            "alpha": 1,
            "green": 200,
            "model": "rgb"
          },
<strong>          "Dark": {
</strong>            "red": 229,
            "blue": 0,
            "alpha": 1,
            "green": 0,
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
We change the case of the token `names` and the `modes` to `kebabCase`. We applyTo the collection level so we transform in `kebabCase`:

* the collection names
* the group names
* the token names
* the mode names

We eventually generate our transformed SDTF graph in a JSON file thanks to the [to-sdtf](to-sdtf.md) parser.

{% code title=".specifyrc.json" lineNumbers="true" %}
```json5
{
  "version": "2",
  "repository": "@organization/repository",
  // Only use the personalAccessToken when working with the CLI
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Format all token names and modes to kebabCase and generate tokens in JSON",
      "parsers": [
        {
          "name": "change-case",
          "options": {
            "change": "names",
            "toCase": "kebabCase",
            "applyTo": {
              "collection": true
            }
          }
        },
        {
          "name": "change-case",
          "options": {
            "change": "modes",
            "toCase": "kebabCase",
            "applyTo": {
              "collection": true
            }
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
</strong>            "red": 255,
            "blue": 255,
            "alpha": 1,
            "green": 255,
            "model": "rgb"
          },
<strong>          "dark": {
</strong>            "red": 229,
            "blue": 29,
            "alpha": 1,
            "green": 29,
            "model": "rgb"
          }
        }
      },
<strong>      "blue-700": {
</strong>        "$type": "color",
        "$description": "token 2 aliased with n modes within collection within n groups",
        "$value": {
<strong>          "light": {
</strong>            "red": 255,
            "blue": 255,
            "alpha": 1,
            "green": 200,
            "model": "rgb"
          },
<strong>          "dark": {
</strong>            "red": 229,
            "blue": 0,
            "alpha": 1,
            "green": 0,
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
