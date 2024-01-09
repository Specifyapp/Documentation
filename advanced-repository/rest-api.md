---
description: >-
  The Specify API lets you extend Specify functionalities beyond what we provide
  out of the box.
---

# REST API

{% hint style="info" %}
New to Specify? Head over to the existing REST API [documentation](https://docs.specifyapp.com/apps-and-tools/rest-api) to learn more about why it can be useful for your team and how to use it.
{% endhint %}

## Endpoint

Specify provides the following endpoint to help you get design tokens and assets from a Specify repository.

`https://api.specifyapp.com/v2/{workspace}/repository/{repository}/execute-rule`

## Parameters

{% swagger method="post" path="" baseUrl="https://api.specifyapp.com/v2/repository/{workspace}/{repository}/execute-rule" summary="Get tokens graph" %}
{% swagger-description %}
Get design tokens and assets from a Specify repository. You can only execute a single rule with this endpoint.
{% endswagger-description %}

{% swagger-parameter in="path" name="workspace" required="true" %}
The name of your organization in Specify. For instance, in this URL `https://specifyapp.com/ @specifyapp/Seeds` the workspace is "@specifyapp".
{% endswagger-parameter %}

{% swagger-parameter in="path" name="name" %}
The name of the Specify repository containing the design data you're requesting. For instance, in this URL `https://specifyapp.com / @specifyapp/Seeds` the repository is "Seeds".
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="" required="true" %}
The name of your rule
{% endswagger-parameter %}

{% swagger-parameter in="body" name="parsers" type="Object or Array" required="true" %}
Can contain an object or an array of objects. Each object corresponds to a specific parser.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Everything worked as expected." %}

{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="No valid API key provided." %}

{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="" %}

{% endswagger-response %}

{% swagger-response status="404: Not Found" description="" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="Something went wrong on Specify" %}

{% endswagger-response %}
{% endswagger %}

Once you have your personal access token, you can pass it within the `Authorization` header of your request.

## Example

Here's a simple example to get tokens in JSON from a repository called `all-design-data`in the `@acme-inc` workspace:

```bash
curl -X POST 'https://api.specifyapp.com/v2/@acme-inc/repository/all-design-data/execute-rule' \
--header 'Authorization: <your-personal-access-token>' \
--header 'Content-Type: application/json' \
--data '{
    "name": "SDTF",
    "parsers": [
        {
            "name": "as-is",
            "output": {
                "type": "file",
                "filePath": "tokens.json"
            }
        }
    ]
}'
```

## Commands

### Pull

Pull design tokens and assets from your Specify repository.

```bash
specify pull
```
