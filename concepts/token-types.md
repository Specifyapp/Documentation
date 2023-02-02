---
description: "Types define every type of design token and asset Specify is compatible with. Use them to target specific types of design data you want to pull from Specify and manage with\_rules and parsers."
---

# Token types

## Introduction

Types define every type of design token and asset Specify is compatible with. Use them to target specific types of design tokens and assets you want to pull from Specify.

In Specify, types are displayed as "categories" of design data you can create and find in your Specify repository.

Specify is compatible with the following design tokens and assets under the `TokenType` type.

## Design tokens

### Border

A border is a line surrounding a UI element. According to your target platform capabilities, you can define the border to go inside (inner border), outside (outer border), or between them (center).

Borders are considered as [composite design tokens ↗](https://design-tokens.github.io/community-group/format/#composite-design-token) because they are composed of several design tokens.

{% hint style="info" %}
Looking for border radius? You can add them as a [Measurement](token-types.md#measurement) type.
{% endhint %}

```typescript
interface BorderValue {
  color: {
    value: ColorValue;
  };
  type:
    | 'none'
    | 'hidden'
    | 'dotted'
    | 'dashed'
    | 'solid'
    | 'double'
    | 'groove'
    | 'ridge'
    | 'inset'
    | 'outset';
  width: {
    value: MeasurementValue;
  };
  align?: string;
  radii?: MeasurementValue;
  rectangleCornerRadii?: Array<MeasurementValue>;
  dashes?: Array<MeasurementValue>;
}
```

### Color

Colors have meaning and support the purpose of the content, communicating things like hierarchy of information, interactive states, and the difference between distinct elements in your UI. Among all your design token types, color is surely one of the most important ones.

```typescript
interface ColorValue {
  r: number;
  g: number;
  b: number;
  a: number;
}
```

### Depth

The Depth token type sets a UI element's position on the z-axis. More commonly called z-index on [Web ↗](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index) and zIndex on [Android ↗](https://developer.android.com/reference/kotlin/androidx/compose/ui/package-summary#\(androidx.compose.ui.Modifier\).zIndex\(kotlin.Float\)) and [iOS ↗](https://developer.apple.com/documentation/uikit/uicollectionviewlayoutattributes/1617768-zindex).

```typescript
interface DepthValue {
  depth: number;
}
```

### Duration

Represents the length of time in milliseconds an animation or animation cycle takes to complete, such as 200 milliseconds (cf [DTCG ↗](https://design-tokens.github.io/community-group/format/#duration)).

```typescript
interface DurationValue {
  duration: number;
  unit: string;
}
```

### Gradient

A gradient is the gradual blending from one color to another. It enables the designer to almost create a new color. It makes objects stand out by adding a new dimension to the design and adding realism to the object. In simple terms, gradients add depth.

Gradients are considered as [composite design tokens ↗](https://design-tokens.github.io/community-group/format/#composite-design-token) because they are composed of several design tokens.

```typescript
interface StepForGradient {
  type: string;
  color: {
    value: ColorValue;
  };
  position: number;
}

interface Gradient {
  angle: string;
  colors: Array<StepForGradient>;
}

interface GradientValue {
  gradients: Array<Gradient>;
}
```

### Measurement

Measurement or [Dimension ↗](https://design-tokens.github.io/community-group/format/#dimension) design tokens help you define size values.

Common design tokens can be defined from this type:

* internal margins
* external margins
* a spacing scale
* a border width
* a breakpoint
* a font size
* border radii...

```typescript
interface MeasurementValue {
  measure: number;
  unit?: string;
}
```

### Opacity

Opacity design tokens help you set the opacity of UI elements.

```typescript
interface OpacityValue {
  opacity: number;
}
```

### Shadow

Shadows help you communicate components elevation in your UIs. Popular variations and names include box-shadow, drop shadow, and many more.

Shadows are considered as [composite design tokens ↗](https://design-tokens.github.io/community-group/format/#composite-design-token) because they are composed of several design tokens.

```typescript
type ShadowValue = Array<{
  color: {
    value: ColorValue;
  };
  offsetX: {
    value: MeasurementValue;
  };
  offsetY: {
    value: MeasurementValue;
  };
  blur: {
    value: MeasurementValue;
  };
  spread?: {
    value: MeasurementValue;
  };
  isInner: boolean;
}>;
```

### Text Style

Text styles or typography helps your UI be usable. They create balance, hierarchy and structure for your content. Some say that "Web is 95% typography". To push this even further let's say UI are 95% typography. In other words, pay a great deal of attention to typography.

A text style is composed of several child design decisions that could be considered as single design tokens like:

* a line-height
* a font size
* a letter spacing
* a font name

Text styles are considered as [composite design tokens ↗](https://design-tokens.github.io/community-group/format/#composite-design-token) because they are composed of several design tokens.

```typescript
export type TextTransformValue =
  | 'none'
  | 'capitalize'
  | 'uppercase'
  | 'lowercase';

export type TextDecorationValue =
  | 'none'
  | 'underline'
  | 'overline'
  | 'line-through'
  | 'dashed'
  | 'wavy';

export type HorizontalAlignValue =
  | 'initial'
  | 'left'
  | 'right'
  | 'center'
  | 'justify'
  | 'start'
  | 'end'
  | 'justify-all'
  | 'match-parent';

export type VerticalAlignValue =
  | 'initial'
  | 'baseline'
  | 'sub'
  | 'super'
  | 'text-top'
  | 'text-bottom'
  | 'middle'
  | 'top'
  | 'bottom';
  
export interface TextStyleValue {
  color?: {
    value: ColorValue;
  };
  font: {
    value: FontValue;
  };
  fontSize: {
    value: MeasurementValue;
  };
  lineHeight?: {
    value: MeasurementValue;
  };
  letterSpacing?: {
    value: MeasurementValue;
  };
  textAlign?: {
    horizontal?: HorizontalAlignValue;
    vertical?: VerticalAlignValue;
  };
  textTransform?: TextTransformValue;
  fontVariant?: Array<string>;
  textDecoration?: Array<TextDecorationValue>;
  textIndent?: {
    value: MeasurementValue;
  };
}
```

### Example

{% tabs %}
{% tab title="border" %}
{% code title=".specifyrc.js" lineNumbers="true" %}
```json
{
  "repository": "@workspace/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Design Tokens / Borders",
      "path": "borders.json",
      "filter": {
        "types": [
          "border"
        ]
      }
    }
  ]
}
```
{% endcode %}
{% endtab %}

{% tab title="color" %}
{% code title=".specifyrc.js" lineNumbers="true" %}
```json
{
  "repository": "@workspace/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Design Tokens / Colors",
      "path": "colors.json",
      "filter": {
        "types": [
          "color"
        ]
      }
    }
  ]
}
```
{% endcode %}
{% endtab %}

{% tab title="depth" %}
{% code title=".specifyrc.js" lineNumbers="true" %}
```json
{
  "repository": "@workspace/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Design Tokens / zIndex",
      "path": "zIndex.json",
      "filter": {
        "types": [
          "depth"
        ]
      }
    }
  ]
}
```
{% endcode %}
{% endtab %}

{% tab title="duration" %}
{% code title=".specifyrc.js" lineNumbers="true" %}
```json
{
  "repository": "@workspace/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Design Tokens / durations",
      "path": "durations.json",
      "filter": {
        "types": [
          "duration"
        ]
      }
    }
  ]
}
```
{% endcode %}
{% endtab %}

{% tab title="gradient" %}
{% code title=".specifyrc.js" lineNumbers="true" %}
```json
{
  "repository": "@workspace/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Design Tokens / Gradients",
      "path": "gradients.json",
      "filter": {
        "types": [
          "gradient"
        ]
      }
    }
  ]
}
```
{% endcode %}
{% endtab %}

{% tab title="measurement" %}
{% code title=".specifyrc.js" lineNumbers="true" %}
```json
{
  "repository": "@workspace/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Design Tokens / Measurements",
      "path": "measurements.json",
      "filter": {
        "types": [
          "measurement"
        ]
      }
    }
  ]
}
```
{% endcode %}
{% endtab %}

{% tab title="opacity" %}
{% code title=".specifyrc.js" lineNumbers="true" %}
```json
{
  "repository": "@workspace/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Design Tokens / Opacities",
      "path": "opacities.json",
      "filter": {
        "types": [
          "opacity"
        ]
      }
    }
  ]
}
```
{% endcode %}
{% endtab %}

{% tab title="shadow" %}
{% code title=".specifyrc.js" lineNumbers="true" %}
```json
{
  "repository": "@workspace/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Design Tokens / Shadows",
      "path": "shadows.json",
      "filter": {
        "types": [
          "shadow"
        ]
      }
    }
  ]
}
```
{% endcode %}
{% endtab %}

{% tab title="textStyle" %}
{% code title=".specifyrc.js" lineNumbers="true" %}
```json
{
  "repository": "@workspace/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Design Tokens / Text Styles",
      "path": "textStyles.json",
      "filter": {
        "types": [
          "textStyle"
        ]
      }
    }
  ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Assets

### Bitmap

Bitmaps are raster images you can use in many contexts. They are basically any image you can display in a UI that is a `.png`, `.jpeg`, `.webp`, `.avif`...

```typescript
interface BitmapValue {
  url: string;
  dimension?: number;
  format?: string;
}
```

### Font

Fonts are files containing typefaces used by your text styles.

In Specify, all font files are stored as .ttf files by default. You can pull and convert them on the fly thanks to the [convert-font ↗](https://github.com/Specifyapp/parsers/tree/master/parsers/convert-font) parser.

```typescript
export type Provider = 'Custom font' | 'Google Fonts';

export type FontWeightKeys = '100' | '200' | '300' | '400' | '500' | '600' | '700' | '800' | '900';

export interface FontValue {
  fontFamily: string;
  fontPostScriptName: string;
  fontWeight?: string | number;
  fontFileMissing?: boolean;
  isItalic?: boolean;
  provider?: Provider;
  url?: string;
  format?: 'ttf';
}
```

### Vector

By "vectors" we mean vector images (e.g., SVG and PDF files). You can use them for 2 main purposes: iconography and illustration. In the following section we will only focus on icons.

Icons act a visual aids to help users complete tasks. We advise you to have an harmonic set of icons you can use to draw attention to specific actions.

```typescript
interface VectorValue {
  url: string;
  format: 'svg' | 'pdf';
}
```

### Example

{% tabs %}
{% tab title="bitmap" %}
{% code title=".specifyrc.js" lineNumbers="true" %}
```json
{
  "repository": "@workspace/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Design Tokens / Images",
      "path": "bitmaps.json",
      "filter": {
        "types": [
          "bitmap"
        ]
      }
    }
  ]
}
```
{% endcode %}
{% endtab %}

{% tab title="font" %}
{% code title=".specifyrc.js" lineNumbers="true" %}
```json
{
  "repository": "@workspace/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Design Tokens / Fonts",
      "path": "fonts.json",
      "filter": {
        "types": [
          "font"
        ]
      }
    }
  ]
}
```
{% endcode %}
{% endtab %}

{% tab title="vector" %}
{% code title=".specifyrc.js" lineNumbers="true" %}
```json
{
  "repository": "@workspace/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Design Tokens / Icons",
      "path": "vectors.json",
      "filter": {
        "types": [
          "vector"
        ]
      }
    }
  ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
