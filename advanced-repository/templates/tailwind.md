---
description: This template helps you generate your design tokens as a Tailwind theme.
---

# Tailwind

This example uses the following parser:

* [to-tailwind](../parsers/to-tailwind.md) to generate your design tokens as a Tailwind theme

{% tabs %}
{% tab title="config.json (CLI)" %}
If you use the CLI, you need to fill three properties:

* `repository`  is `@organization/repository`
* `personalAccessToken` which you can generate [in your account settings](https://specifyapp.com/user/personal-access-tokens)&#x20;
* `rules` are where you provide parsers and compatible options

```json
{
  "version": "2",
  "repository": "@organization/repository",
  // Only use the personalAccessToken when working with the CLI
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Generate tokens as a Tailwind theme",
      "parsers": [
        {
          "name": "to-tailwind",
          "output": {
            "type": "file",
            "filePath": "theme.js"
          }
        }
      ]
    }
  ]
}
```
{% endtab %}

{% tab title="config.json (GitHub)" %}
If you use the GitHub, you need to fill two properties:

* `repository`  is `@organization/repository`
* `rules` lets you transform tokens by chaining parsers

{% hint style="info" %}
Make sure you have connected your GitHub account with your Specify account. Head toward [this article](https://help.specifyapp.com/en/articles/4722440-add-github-as-a-destination) to learn more.
{% endhint %}

```json
{
  "version": "2",
  "repository": "@organization/repository",
  "rules": [
    {
      "name": "Generate tokens as a Tailwind theme",
      "parsers": [
        {
          "name": "to-tailwind",
          "output": {
            "type": "file",
            "filePath": "theme.js"
          }
        }
      ]
    }
  ]
}
```
{% endtab %}
{% endtabs %}
