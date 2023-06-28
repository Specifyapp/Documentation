| Parser | Description | Usage Example |
|---|---|---|
| camelcasify | Apply camelcase function on specific keys from a design token. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/camelcasify/README.md#usage) |
| convert-font | Convert font in several formats. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/convert-font/README.md#usage) |
| filter | Filter tokens and assets by their name using a regular expression. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/filter/README.md#usage) |
| inline-css-variables-in-svg | Replace all the `stroke` and `fill` attribute raw color value by its corresponding design token as a CSS variable. If no design token match, the raw value will be left as is. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/inline-css-variables-in-svg/README.md#usage) |
| kebabcasify | Apply kebabcase function on specific keys from a design token. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/kebabcasify/README.md#usage) |
| link-design-tokens | Have design tokens referencing other ones. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/link-design-tokens/README.md#usage) |
| name-assets-files-by-pattern | Set a structured filename on your assets. It won't rename your asset but only add a new `filename` property on the asset object. The filename structure uses [mustache](https://github.com/janl/mustache.js#templates) as a template engine. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/name-assets-files-by-pattern/README.md#usage) |
| omit | Omit keys from a design token not given in parameters. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/omit/README.md#usage) |
| pascalcasify | Apply pascalcase function on specific keys from a design token. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/pascalcasify/README.md#usage) |
| pick | Get only specific keys from a design token given in params. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/pick/README.md#usage) |
| prefix-by | Concatenate two strings. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/prefix-by/README.md#usage) |
| px-to-rem | Convert the value of a measurement design token from pixel to rem. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/px-to-rem/README.md#usage) |
| replace-string | Replace any string matched by a regex by a new string. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/replace-string/README.md#usage) |
| round-number | Round any measurement design token with specific precision. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/round-number/README.md#usage) |
| snakecasify | Apply snakecase function on specific keys from a design token. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/snakecasify/README.md#usage) |
| sort-by | Loop on several design tokens and sort them according to their respective key values. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/sort-by/README.md#usage) |
| suffix-by | Concatenate two strings. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/suffix-by/README.md#usage) |
| svg-to-jsx | Wrap SVG files within a JSX component. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/svg-to-jsx/README.md#usage) |
| svgo | Optimize vectors using [svgo](https://github.com/svg/svgo). | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/svgo/README.md#usage) |
| to-css-custom-properties | Transform design tokens in CSS Custom Properties. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/to-css-custom-properties/README.md#usage) |
| to-css-font-import | Create CSS `@font-face` rules to import your font files. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/to-css-font-import/README.md#usage) |
| to-css-text-style | Create text styles as CSS classes. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/to-css-text-style/README.md#usage) |
| to-dsp | Create a [Design System Package (DSP)](https://github.com/AdobeXD/design-system-package-dsp). | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/to-dsp/README.md#usage) |
| to-flutter | Format design tokens to create a theme compatible with the [Flutter specification](https://docs.flutter.dev/cookbook/design/themes). | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/to-flutter/README.md#usage) |
| to-jss | Transform design tokens in JSS. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/to-jss/README.md#usage) |
| to-react-native | Transform design tokens to a JavaScript `theme` object compatible with [React Native](https://reactnative.dev/). | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/to-react-native/README.md#usage) |
| to-scss-map | Generate `.scss` files containing Scss map and function / mixin to access the values of the tokens. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/to-scss-map/README.md#usage) |
| to-scss-mixin-text-style | Create text styles formatted as [SCSS mixins](https://sass-lang.com/documentation/at-rules/mixin). | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/to-scss-mixin-text-style/README.md#usage) |
| to-scss-variables | Transform design tokens in SCSS variables. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/to-scss-variables/README.md#usage) |
| to-style-dictionary | Generate [Style Dictionary](https://amzn.github.io/style-dictionary/#/) configuration files for all your design tokens coming from Specify. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/to-style-dictionary/README.md#usage) |
| to-tailwind | Format design tokens to create a theme compatible with the [TailwindCSS specification](https://tailwindcss.com/docs/theme). | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/to-tailwind/README.md#usage) |
| to-theme-ui | Format design tokens to create a theme compatible with the [theme-ui specification](https://theme-ui.com/theme-spec). | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/to-theme-ui/README.md#usage) |
| to-typescript-definition | Format design tokens to create their corresponding TypeScript types. | [Example](https://github.com/Specifyapp/parsers/blob/master/parsers/to-typescript-definition/README.md#usage) |