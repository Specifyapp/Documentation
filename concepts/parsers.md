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

Utility parsers take care of "smaller" transformation. Like converting a pixel value to `rem` or transforming a string to kebabcase.

Some examples:

* [convert-font](https://github.com/Specifyapp/parsers/tree/master/parsers/convert-font)
* [kebabcasify](https://github.com/Specifyapp/parsers/tree/master/parsers/kebabcasify)
* [px-to-rem](https://github.com/Specifyapp/parsers/tree/master/parsers/px-to-rem)

## All parsers available

All parsers are open source and available on [the following GitHub repository](https://github.com/Specifyapp/parsers).

<table data-full-width="true"><thead><tr><th>Parser</th><th width="660.3333333333334">Description</th><th>Usage Example</th></tr></thead><tbody><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/camelcasify">camelcasify</a></td><td>Apply camelcase function on specific keys from a design token.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/camelcasify/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/convert-font">convert-font</a></td><td>Convert font in several formats.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/convert-font/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/filter">filter</a></td><td>Filter tokens and assets by their name using a regular expression.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/filter/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/inline-css-variables-in-svg">inline-css-variables-in-svg</a></td><td>Replace all the <code>stroke</code> and <code>fill</code> attribute raw color value by its corresponding design token as a CSS variable. If no design token match, the raw value will be left as is.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/inline-css-variables-in-svg/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/kebabcasify">kebabcasify</a></td><td>Apply kebabcase function on specific keys from a design token.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/kebabcasify/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/link-design-tokens">link-design-tokens</a></td><td>Have design tokens referencing other ones.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/link-design-tokens/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/name-assets-files-by-pattern">name-assets-files-by-pattern</a></td><td>Set a structured filename on your assets. It won't rename your asset but only add a new <code>filename</code> property on the asset object. The filename structure uses <a href="https://github.com/janl/mustache.js#templates">mustache</a> as a template engine.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/name-assets-files-by-pattern/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/omit">omit</a></td><td>Omit keys from a design token not given in parameters.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/omit/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/pascalcasify">pascalcasify</a></td><td>Apply pascalcase function on specific keys from a design token.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/pascalcasify/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/pick">pick</a></td><td>Get only specific keys from a design token given in params.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/pick/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/prefix-by">prefix-by</a></td><td>Concatenate two strings.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/prefix-by/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/px-to-rem">px-to-rem</a></td><td>Convert the value of a measurement design token from pixel to rem.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/px-to-rem/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/replace-string">replace-string</a></td><td>Replace any string matched by a regex by a new string.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/replace-string/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/round-number">round-number</a></td><td>Round any measurement design token with specific precision.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/round-number/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/snakecasify">snakecasify</a></td><td>Apply snakecase function on specific keys from a design token.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/snakecasify/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/sort-by">sort-by</a></td><td>Loop on several design tokens and sort them according to their respective key values.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/sort-by/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/suffix-by">suffix-by</a></td><td>Concatenate two strings.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/suffix-by/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/svg-to-jsx">svg-to-jsx</a></td><td>Wrap SVG files within a JSX component.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/svg-to-jsx/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/svgo">svgo</a></td><td>Optimize vectors using <a href="https://github.com/svg/svgo">svgo</a>.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/svgo/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-css-custom-properties">to-css-custom-properties</a></td><td>Transform design tokens in CSS Custom Properties.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-css-custom-properties/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-css-font-import">to-css-font-import</a></td><td>Create CSS <code>@font-face</code> rules to import your font files.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-css-font-import/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-css-text-style">to-css-text-style</a></td><td>Create text styles as CSS classes.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-css-text-style/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-dsp">to-dsp</a></td><td>Create a <a href="https://github.com/AdobeXD/design-system-package-dsp">Design System Package (DSP)</a>.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-dsp/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-flutter">to-flutter</a></td><td>Format design tokens to create a theme compatible with the <a href="https://docs.flutter.dev/cookbook/design/themes">Flutter specification</a>.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-flutter/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-jss">to-jss</a></td><td>Transform design tokens in JSS.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-jss/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-react-native">to-react-native</a></td><td>Transform design tokens to a JavaScript <code>theme</code> object compatible with <a href="https://reactnative.dev/">React Native</a>.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-react-native/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-scss-map">to-scss-map</a></td><td>Generate <code>.scss</code> files containing Scss map and function / mixin to access the values of the tokens.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-scss-map/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-scss-mixin-text-style">to-scss-mixin-text-style</a></td><td>Create text styles formatted as <a href="https://sass-lang.com/documentation/at-rules/mixin">SCSS mixins</a>.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-scss-mixin-text-style/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-scss-variables">to-scss-variables</a></td><td>Transform design tokens in SCSS variables.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-scss-variables/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-style-dictionary">to-style-dictionary</a></td><td>Generate <a href="https://amzn.github.io/style-dictionary/#/">Style Dictionary</a> configuration files for all your design tokens coming from Specify.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-style-dictionary/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-tailwind">to-tailwind</a></td><td>Format design tokens to create a theme compatible with the <a href="https://tailwindcss.com/docs/theme">TailwindCSS specification</a>.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-tailwind/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-theme-ui">to-theme-ui</a></td><td>Format design tokens to create a theme compatible with the <a href="https://theme-ui.com/theme-spec">theme-ui specification</a>.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-theme-ui/README.md#usage">Example</a></td></tr><tr><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-typescript-definition">to-typescript-definition</a></td><td>Format design tokens to create their corresponding TypeScript types.</td><td><a href="https://github.com/Specifyapp/parsers/blob/master/parsers/to-typescript-definition/README.md#usage">Example</a></td></tr></tbody></table>
