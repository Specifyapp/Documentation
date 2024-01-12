---
description: This parser helps you convert units of dimension tokens.
---

# convert-dimension

## Interface

```typescript
interface parser {
  name: 'convert-dimension';
  options: {
    toFormat: '%' | 'px' | 'em' | 'rem' | 'pt' | 'pc' | 'in' | 'cm' | 'mm' | 'ex' | 'cap' | 'ch' | 'ic' | 'lh' | 'rlh' | 'vw' | 'svw' | 'lvw' | 'dvw' | 'vh' | 'svh' | 'lvh' | 'dvh' | 'vi' | 'svi' | 'lvi' | 'dvi' | 'vb' | 'svb' | 'lvb' | 'dvb' | 'vmin' | 'svmin' | 'lvmin' | 'dvmin' | 'vmax' | 'svmax' | 'lvmax' | 'dvmax'
    baseValue?: {
      rem?: number
    }
    applyTo?: SDTFQuery,
  };
}
```

## Options

<table><thead><tr><th width="186">Parameter</th><th width="127.33333333333331">Required</th><th width="341">Type</th><th width="136">Default</th><th width="237">Description</th></tr></thead><tbody><tr><td><code>toFormat</code></td><td>required</td><td><pre class="language-typescript"><code class="lang-typescript">| '%' 
| 'px' 
| 'em' 
| 'rem' 
| 'pt' 
| 'pc' 
| 'in' 
| 'cm' 
| 'mm' 
| 'ex' 
| 'cap' 
| 'ch' 
| 'ic' 
| 'lh' 
| 'rlh' 
| 'vw' 
| 'svw' 
| 'lvw' 
| 'dvw' 
| 'vh' 
| 'svh' 
| 'lvh' 
| 'dvh' 
| 'vi' 
| 'svi' 
| 'lvi' 
| 'dvi' 
| 'vb' 
| 'svb' 
| 'lvb' 
| 'dvb' 
| 'vmin' 
| 'svmin' 
| 'lvmin' 
| 'dvmin' 
| 'vmax' 
| 'svmax' 
| 'lvmax' 
| 'dvmax'
</code></pre></td><td></td><td>The target color format to convert to. Actual value conversion is done by the <a href="https://www.npmjs.com/package/colord">colord</a> package.</td></tr><tr><td><code>baseValue</code></td><td>optional</td><td><pre class="language-typescript"><code class="lang-typescript">{ rem: number }
</code></pre></td><td></td><td></td></tr><tr><td><code>applyTo</code></td><td>optional</td><td><pre class="language-typescript"><code class="lang-typescript">| { collection: string | true }
| { group: string | true }
| { token: string | true }
| SDTFQuery
</code></pre></td><td><pre><code>{ token: true }
</code></pre></td><td>The selection where to apply the transformation.<br><br><code>collection</code>, <code>group</code>, <code>token</code> take a Regex string or <code>true</code> to select anything of the kind.<br><br>An <code>SDTFQuery</code> can be used for advance use cases. Learn more about <a href="../querying-a-sdtf-graph.md">how to query your SDTF graph</a>.</td></tr></tbody></table>

## Basic usage

{% tabs %}
{% tab title="Input" %}
{% code lineNumbers="true" %}
```json
{
  "Foundation": {
    "spacing": {
      "1": {
        "$type": "dimension",
        "$value": {
          "default": {
            "value": 4,
            "unit": "px"
          }
        }
      },
      "2": {
        "$type": "dimension",
        "$value": {
          "default": {
            "value": 8,
            "unit": "px"
          }
        }
      },
      "3": {
        "$type": "dimension",
        "$value": {
          "default": {
            "value": 12,
            "unit": "px"
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
      "name": "Convert spacing in rem and generate tokens in JSON",
      "parsers": [
        {
          "name": "convert-dimension",
          "options": {
            "toFormat": "rem"
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
  "Foundation": {
    "spacing": {
      "1": {
        "$type": "dimension",
        "$value": {
          "default": {
            "value": 0.25,
            "unit": "rem"
          }
        }
      },
      "2": {
        "$type": "dimension",
        "$value": {
          "default": {
            "value": 0.5,
            "unit": "rem"
          }
        }
      },
      "3": {
        "$type": "dimension",
        "$value": {
          "default": {
            "value": 0.75,
            "unit": "rem"
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
