---
description: This parser helps you select design tokens from specific mode(s).
---

# select-modes

## Interface

```typescript
interface parser {
  name: 'select-modes';
  options: {
    modes: string[];
  };
}
```

## Options

<table><thead><tr><th width="292">Parameter</th><th width="127.33333333333331">Required</th><th width="341">Type</th><th width="136">Default</th><th width="253">Description</th></tr></thead><tbody><tr><td><code>modes</code></td><td>required</td><td><code>Array</code></td><td></td><td>The query that select items in the graph.</td></tr></tbody></table>

## Basic usage: select all tokens from a mode named "light"

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
1. We want to get all design tokens from the mode named "light"
2. We eventually generate our design tokens ass CSS variables in a CSS file thanks to the `to-css-custom-properties` parser.

{% code title=".specifyrc.json" lineNumbers="true" %}
```json5
{
  "version": "2",
  "repository": "@organization/repository",
  // Only use the personalAccessToken when working with the CLI
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Only get tokens from the mode named 'light' and gererate tokens in CSS",
      "parsers": [
        {
          "name": "select-modes",
          "options": {
            "modes": ["light"]
          }
        },
        {
          "name": "to-css-custom-properties",
          "options": {
            "selectorTemplate": "[data-theme=\"{{mode}}\"]"
          },
          "output": {
            "type": "file",
            "filePath": "public/css-custom-properties.css"
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
```css
[data-theme="light"] {
  --danger-dangerToken: rgb(209, 204, 204);
  --info-infoToken: rgb(219, 234, 254);
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
