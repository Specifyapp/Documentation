---
description: >-
  A 5min guide on collecting and pulling your first design tokens and assets
  with Specify.
---

# Getting started

## Introduction

In this guide you’ll learn how to pull your first design tokens and assets to CSS Custom Properties using the Specify CLI.

{% hint style="info" %}
This guide helps you to sync tokens from Figma local styles and frames to Specify. Want to sync Figma Variables instead? [Click here](../sdtf-beta/getting-started.md) to learn more.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=iFa-MEjFbmE" %}

## Before getting started

To get the most out of this guide, you’ll need:

* A Specify account
* A Specify repository containing some design tokens and assets ([Learn more ↗](glossary.md#repository))

## 1. Install the CLI

Install `@specifyapp/cli` via npm or Yarn.

{% tabs %}
{% tab title="NPM" %}
```bash
npm install -g @specifyapp/cli
```
{% endtab %}

{% tab title="Yarn" %}
```bash
yarn global add @specifyapp/cli
```
{% endtab %}
{% endtabs %}

## 2. Create your Specify config file

Create a configuration file for your desired output format using one of our templates ↗️

```bash
specify init
```

## 3. Add your Specify repository

Add your Specify `repository` from which you want to pull your design tokens and assets. [Learn more ↗](https://specify.gitbook.io/specify-documentation/usage/cli#commands).

{% tabs %}
{% tab title="JavaScript (CommonJS)" %}
<pre class="language-javascript" data-line-numbers><code class="lang-javascript">module.exports = {
<strong>  repository: '@workspace/repository',
</strong>  personalAccessToken: '&#x3C;your-personal-access-token>',
  rules: [],
};
</code></pre>
{% endtab %}

{% tab title="JSON" %}
<pre class="language-json" data-line-numbers><code class="lang-json">{
<strong>  "repository": "@workspace/repository",
</strong>  "personalAccessToken": "&#x3C;your-personal-access-token>",
  "rules": []
}
</code></pre>
{% endtab %}
{% endtabs %}

## 4. Add your personal access token

Generate a `personalAccessToken` for the CLI and add it in your configuration.

{% tabs %}
{% tab title="JavaScript (CommonJS)" %}
<pre class="language-javascript" data-line-numbers><code class="lang-javascript">module.exports = {
  repository: '@workspace/repository',
<strong>  personalAccessToken: '&#x3C;your-personal-access-token>',
</strong>  rules: [],
};
</code></pre>
{% endtab %}

{% tab title="JSON" %}
<pre class="language-json" data-line-numbers><code class="lang-json">{
  "repository": "@workspace/repository",
<strong>  "personalAccessToken": "&#x3C;your-personal-access-token>",
</strong>  "rules": []
}
</code></pre>
{% endtab %}
{% endtabs %}

## 5. Pull your design tokens and assets

Our configuration is ready and we can now pull our design tokens and assets using the `pull` command.

```bash
specify pull
```
