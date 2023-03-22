---
description: >-
  The Specify API lets you extend Specify functionalities beyond what we provide
  out of the box.
---

# REST API

## Introduction

The Specify API is based on REST structure. We support authentication via access tokens. Requests are made via HTTP endpoints with clear functions and appropriate response codes. Endpoints allow you to request design tokens and assets from a Specify repository.

## What you can do with the REST API

<figure><img src="../front/documentation/.gitbook/assets/specify-api.jpg" alt=""><figcaption><p>Overview of the possibilities offered by the Specify API</p></figcaption></figure>

Specify's REST API is useful if you want to use design data coming from Specify through custom scripts like a Figma plugin or a [Raycast script](https://www.raycast.com/).

In short, our REST API helps you request design data through HTTP requests. Like with our [CLI](cli.md) you can use parsers to transform design data.

However, you cannot directly generate files using the REST API as it only returns text. You'll have to write custom scripts to generate design files (e.g., `colors.css`).

To sum things up, to generate files from Specify (e.g., `colors.css` or `icon.svg`) containing design tokens or assets use the [CLI](cli.md) or our [GitHub application](https://specifyapp.com/developers/github).

## Endpoint

Specify provides the following endpoint to help you get design tokens and assets from a Specify repository.

`https://api.specifyapp.com/repository/{workspace}/{repository}/design-tokens`

### Parameters

{% swagger method="post" path="" baseUrl="https://api.specifyapp.com/repository/{workspace}/{repository}/design-tokens" summary="" expanded="true" %}
{% swagger-description %}
Get design tokens and assets from a Specify repository.
{% endswagger-description %}

{% swagger-parameter in="path" name="workspace" required="true" %}
The name of your organization in Specify.\\

For instance, in this URL `https://specifyapp.com/@specifyapp/Seeds/color` the workspace is "@specifyapp".
{% endswagger-parameter %}

{% swagger-parameter in="path" name="name" required="true" %}
The name of the Specify repository containing the design data you're requesting.\\

For instance, in this URL `https://specifyapp.com/@specifyapp/Seeds/color` the repository is "Seeds".
{% endswagger-parameter %}

{% swagger-parameter in="body" name="filter" type="Object" required="false" %}
Set all the

[Token types](../concepts/token-types.md)

you want to target.



`"filter": { "types": [ "color", "font", "textStyle" ] }`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="parsers" type="Object or Array" required="false" %}
Can contain an object or an array of objects. Each object corresponds to a specific

[parser](../concepts/parsers.md#all-parsers-available).
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Everything worked as expected." %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="No valid API key provided." %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="The API key doesn" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="The requested resource doesn" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="Something went wrong on Specify" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

Once you have your personal access token, you can pass it within the `Authorization` header of your request.

### Example

Here's a simple example to get colors in CSS variables from a repository called `all-design-data`in the `@acme-inc` workspace:

```bash
curl -X POST 'https://api.specifyapp.com/repository/@acme-inc/all-design-data/design-tokens' \
  -H 'Authorization: <your-personal-access-token>' \
  -H 'Content-Type: application/json' \
  -d '{"filter": { "types": ["color"]}, "parsers": [{"name": "to-css-custom-properties"}]}'
```

## Errors

Specify uses standard HTTP response codes for success and failure notifications. Our errors are further classified by type. In general: Codes in the 2xx range indicate success. Codes in the 4xx range indicate an error that failed given the information provided (e.g., a required parameter was omitted). Codes in the 5xx range indicate an error with Specify servers.

Some 4xx errors that could be handled programmatically include an error code that briefly explains the error reported.

### Attributes

| Property     | Type     | Description                                                                                                                                           |
| ------------ | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| `type`       | `string` | The type of error returned. One of `api_connection_error`, `api_error`, `authentication_error`, `invalid_request_error`, or `rate_limit_error`.       |
| `statusCode` | `string` | For some errors that could be handled programmatically, a short string indicating the error code reported.                                            |
| `message`    | `string` | A human-readable message providing more details about the error.                                                                                      |
| `validation` | `string` | All invalid query / payload parameters. All invalid query / payload parameters. This property will be displayed on specific endpoints error response. |
