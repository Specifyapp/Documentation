---
description: This parser helps you filter a SDTF graph.
---

# filter

## Interface

```typescript
interface parser {
  name: 'filter';
  options: {
    query: SDTFQuery;
    resolveAliases?: boolean;
    allowUnresolvableAliases?: boolean;
  };
}
```

## Options

<table><thead><tr><th width="292">Parameter</th><th width="127.33333333333331">Required</th><th width="341">Type</th><th width="136">Default</th><th width="253">Description</th></tr></thead><tbody><tr><td><code>query</code></td><td>required</td><td><code>SDTFQuery</code></td><td></td><td>The query that select items in the graph.</td></tr><tr><td><code>resolveAliases</code></td><td>optional</td><td><code>boolean</code></td><td><code>false</code></td><td>Whether to resolve the aliases of the graph.<br><br>Thus, preventing aliases to become unresolvable when their source is not included in the selected items.</td></tr><tr><td><code>allowUnresolvableAliases</code></td><td>optional</td><td><code>boolean</code></td><td><code>true</code></td><td>Whether to allow unresolvable aliases to flow through. <br><br>This option is <strong>only available when</strong> <code>resolveAliases = true</code></td></tr></tbody></table>

## Basic usage: select all tokens from a group in a collection

{% tabs %}
{% tab title="Input" %}
<pre class="language-json" data-line-numbers><code class="lang-json">{
  "colors": {
    "$collection": {
      "$modes": ["light", "dark"]
    },
<strong>    "info": {
</strong><strong>      "infoToken": {
</strong><strong>        "$type": "color",
</strong><strong>        "$value": {
</strong><strong>          "light": {
</strong><strong>            "model": "rgb",
</strong><strong>            "red": 219,
</strong><strong>            "green": 234,
</strong><strong>            "blue": 254,
</strong><strong>            "alpha": 1
</strong><strong>          },
</strong><strong>          "dark": {
</strong><strong>            "model": "rgb",
</strong><strong>            "red": 219,
</strong><strong>            "green": 234,
</strong><strong>            "blue": 254,
</strong><strong>            "alpha": 1
</strong><strong>          }
</strong><strong>        }
</strong><strong>      }
</strong><strong>    },
</strong>    "danger": {
      "dangerToken": {
        "$type": "color",
        "$value": {
          "light": {
            "model": "rgb",
            "red": 209,
            "green": 204,
            "blue": 204,
            "alpha": 1
          },
          "dark": {
            "model": "rgb",
            "red": 19,
            "green": 34,
            "blue": 54,
            "alpha": 1
          }
        }
      }
    }
  }
}
</code></pre>
{% endtab %}

{% tab title="Config" %}
1. We want to get all tokens in all groups named "info"
2. We also want to get the `parent` collection...
3. ... and all `children` tokens within the "info" group(s)
4. We eventually generate our transformed SDTF graph in a JSON file thanks to the `to-sdtf` parser.

{% code title=".specifyrc.json" lineNumbers="true" %}
```json
{
  "version": "2",
  "repository": "@organization/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Only get tokens from a group named 'info' and gererate tokens in JSON",
      "parsers": [
        {
          "name": "filter",
          "options": {
            "query": {
              "where": {
                "group": "info",
                "select": {
                  "parents": true,
                  "children": true
                }
              }
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
{% code title="tokens.json" lineNumbers="true" %}
```json
{
  "colors": {
    "$collection": {
      "$modes": ["light", "dark"]
    },
    "info": {
      "infoToken": {
        "$type": "color",
        "$value": {
          "light": {
            "model": "rgb",
            "red": 219,
            "green": 234,
            "blue": 254,
            "alpha": 1
          },
          "dark": {
            "model": "rgb",
            "red": 219,
            "green": 234,
            "blue": 254,
            "alpha": 1
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
