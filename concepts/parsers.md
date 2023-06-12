---
description: >-
  Parsers are functions allowing you to transform design tokens and assets
  coming from Specify to fit your needs and company standards.
---

# Parsers

## Why you need parsers

<figure><img src="../front/documentation/.gitbook/assets/where-parsers-happen-dark.jpg" alt=""><figcaption><p>Parsers help you transform raw design tokens and assets returned by Specify to match your company standards</p></figcaption></figure>

By default, without any parsers, Specify will return your design data as raw data:

* Design tokens are returned in JSON
* Assets are returned as files

There are high chances you need to transform those design data to fit your needs. Parsers help you do just that.

## What are parsers?

Parsers are functions allowing you to transform design tokens and assets coming from Specify to fit your needs and company standards.

<figure><img src="../front/documentation/.gitbook/assets/how-parsers-work.jpg" alt=""><figcaption><p>An example output pipeline that pulls colors from Specify, sorts them alphabetically and transforms them as CSS Custom Properties</p></figcaption></figure>

A parser does the following job:

1. Receives design data as input
2. Transforms this design data
3. Returns the transformed data

The data returned by a parser can either be:

* Design data that can be used by another parser coming next in your transformation pipeline
* A file so it can be used by people, frameworks, or scripts

{% hint style="info" %}
Parsers are what make Specify powerful and flexible. They help you be in total control of the design data you pull from Specify.
{% endhint %}

Parsers are ordered and takes specific input to generate specific output. This way, we can easily test the input coming from the previous parser to check if the whole parsers process will work.

## Categories

Parsers are classified in 2 categories: technology and utility.

### Technology

Technology parsers help you transform your design tokens to specific technologies and formats (CSS Custom properties, SCSS, Tailwind, a Javascript theme object compatible with React Native...)

Some examples:

* [to-react-native](https://github.com/Specifyapp/parsers/tree/master/parsers/to-react-native)
* [to-css-custom-properties](https://github.com/Specifyapp/parsers/tree/master/parsers/to-css-custom-properties)
* [to-scss-variables](https://github.com/Specifyapp/parsers/tree/master/parsers/to-scss-variables)
* [to-tailwind](https://github.com/Specifyapp/parsers/tree/master/parsers/to-tailwind)

### Utility

Utility parsers take care of "smaller" transformation. Like converting a pixel value to \`rem\` or transforming a string to kebabcase.

Some examples:

* [convert-font](https://github.com/Specifyapp/parsers/tree/master/parsers/convert-font)
* [kebabcasify](https://github.com/Specifyapp/parsers/tree/master/parsers/kebabcasify)
* [px-to-rem](https://github.com/Specifyapp/parsers/tree/master/parsers/px-to-rem)

## All parsers available

All parsers are open source and available on [the following GitHub repository](https://github.com/Specifyapp/parsers).

<table><thead><tr><th width="278">Name</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/camelcasify">camelcasify</a></td><td>Apply camelcase function on specific keys from a design token.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/convert-font">convert-font</a></td><td>Convert font files in several formats: <code>woff2</code>, <code>woff</code>, <code>otf</code>, <code>ttf</code>, <code>eot</code>.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/filter">filter</a></td><td>Filter design tokens and assets by their name using a regular expression.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/inline-css-variables-in-svg">inline-css-variables-in-svg</a></td><td>Replace hardcoded design token values in a SVG string by their corresponding CSS Custom Property.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/kebabcasify">kebabcasify</a></td><td>Apply kebabcase function on specific keys from a design token.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/link-design-tokens">link-design-tokens</a></td><td>Have design tokens referencing other ones. It replaces absolute values by their potential corresponding design token.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/name-assets-files-by-pattern">name-assets-files-by-pattern</a></td><td>Set a structured filename on your assets. It won't rename your asset but only add a new <code>filename</code> property on the asset object. The filename structure uses <a href="https://github.com/janl/mustache.js#templates">mustache</a> as a template engine.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/omit">omit</a></td><td>Omit keys from a design token not given in parameters.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/pascalcasify">pascalcasify</a></td><td>Apply pascalcase function on specific keys from a design token.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/pick">pick</a></td><td>Get only specific keys from a design token given in params.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/px-to-rem">px-to-rem</a></td><td>Convert the value of a Measurement design token from pixel to rem.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/prefix-by">prefix-by</a></td><td>Prefix a string or a whole file by a string.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/replace-string">replace-string</a></td><td>Replace any string matched by a regex by a new string.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/round-number">round-number</a></td><td>Round any measurement design token with specific precision.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/snakecasify">snakecasify</a></td><td>Apply snakecase function on specific keys from a design token.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/sort-by">sort-by</a></td><td>Loop on several design tokens and sort them according to their respective key values.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/suffix-by">suffix-by</a></td><td>Concatenate two strings.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/svg-to-jsx">svg-to-jsx</a></td><td>Wrap SVG files within a JSX component.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/svgo">svgo</a></td><td>Optimize vectors using <a href="https://github.com/svg/svgo">svgo</a>.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/to-css-custom-properties">to-css-custom-properties</a></td><td>Transform design tokens in CSS Custom Properties.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/to-css-font-import">to-css-font-import</a></td><td>Create CSS <code>@font-face</code> rules to import your font files.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/to-css-text-style">to-css-text-style</a></td><td>Create text styles as CSS classes.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/to-dsp">to-dsp</a></td><td>Create a <a href="https://github.com/AdobeXD/design-system-package-dsp">Design System Package (DSP)</a>.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/to-jss">to-jss</a></td><td>Transform design tokens in JSS.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/to-flutter">to-flutter</a></td><td>Transform design tokens for Flutter.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/to-react-native">to-react-native</a></td><td>Transform design tokens to a JavaScript theme object compatible with <a href="https://reactnative.dev/">React Native</a>.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/to-scss-map">to-scss-map</a></td><td>Generate <code>.scss</code> files containing Scss map and function / mixin to access the values of the tokens.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/to-scss-mixin-text-style">to-scss-mixin-text-style</a></td><td>Create text styles formatted as <a href="https://sass-lang.com/documentation/at-rules/mixin">SCSS mixins</a>.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/to-scss-variables">to-scss-variables</a></td><td>Transform design tokens in SCSS variables.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/to-style-dictionary">to-style-dictionary</a></td><td>Generate <a href="https://amzn.github.io/style-dictionary/#/">Style Dictionary</a> configuration files for all your design tokens coming from Specify.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/to-tailwind">to-tailwind</a></td><td>Create a theme compatible with the <a href="https://tailwindcss.com/docs/theme">TailwindCSS specification</a>. The theme is also compatible with <a href="https://windicss.org/">WindiCSS</a>.</td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/tree/master/parsers/to-theme-ui">to-theme-ui</a></td><td>Create a theme compatible with the <a href="https://theme-ui.com/theme-spec">theme-ui specification</a>.</td></tr></tbody></table>
