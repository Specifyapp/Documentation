---
description: Learn more about how to query your SDTF token graph.
---

# Querying a SDTF graph

## Introduction

Your token system can be more complex than it seems. You will often need to interact with your token graph to transform a specific set of design tokens within a Specify configuration.

This article will help you understand how you can query your token graph to select a specific set of tokens.

## Compatible parsers

You'll need to query your graph when using the following parsers:

* [filter](parsers/filter.md)
* [change-case](parsers/change-case.md)

## Query structure

Every Query holds a single a where property being an object, to select one branch of the graph, or an array of objects, to select many branches of the graph (OR statement).

```typescript
Type Query = { where: Where | Array<Where> }
```

The `where` property splits in 3 kinds: token, group, collection - offering a dedicated set of options to match against the given kind.

The `name` property accepts a RegExp for a value. These resources will help you debug your regular expressions:

* [https://regex101.com/](https://regex101.com/)
* [https://regexr.com/](https://regexr.com/)

### Where Token

```typescript
type WhereToken = {
  token: 
    | string
    | {
      name?: string;
      description?: string?;
    }
  select: 
    | true
    | {
      token?: boolean;
      parents?:
        | true
        | {
          groups?: true;
          collections?: true;
        }
    }
}
```

### Where Group

```typescript
type WhereGroup = {
  group: string;
  select: 
    | true
    | {
      group?: boolean;
      parents?:
        | true
        | {
          groups?: true;
          collections?: true;
        }
      children:
        | true
        | {
          groups?: true;
          collections?: true;
          tokens?: true;
        }
    }
}
```

### Where Collection

```typescript
type WhereCollection = {
  collection: string;
  select: 
    | true
    | {
      collection?: boolean;
      parents?:
        | true
        | {
          groups?: true;
        }
      children:
        | true
        | {
          groups?: true;
          tokens?: true;
        }
    }
}
```

## Use cases

### Select tokens from a specific collection

{% code title=".specifyrc.json" lineNumbers="true" %}
```json
{
  "version": "2",
  "repository": "@organization/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Get tokens from collection named 'Colors'",
      "parsers": [
        {
          "name": "filter",
          "options": {
            "query": {
              "where": {
                "collection": "^Colors$",
                "select": {
                  "parents": true,
                  "children": true
                }
              }
            }
          }
        }
      ]
    }
  ]
}
```
{% endcode %}



### Select tokens from several collections matching a naming pattern

{% code title=".specifyrc.json" lineNumbers="true" %}
```json
{
  "version": "2",
  "repository": "@organization/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Get tokens from all collections whose names contain 'colors'",
      "parsers": [
        {
          "name": "filter",
          "options": {
            "where": {
              "collection": "colors",
              "select": {
                "collection": true,
                "children": {
                  "tokens": true
                }
              }
            }
          }
        }
      ]
    }
  ]
}
```
{% endcode %}

### Select tokens from a specific group

{% code title=".specifyrc.json" lineNumbers="true" %}
```json
{
  "version": "2",
  "repository": "@organization/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Get tokens from all groups named 'brand'",
      "parsers": [
        {
          "name": "filter",
          "options": {
            "query": {
              "where": {
                "group": "^brand$",
                "select": {
                  "parents": true,
                  "children": true
                }
              }
            }
          }
        }
      ]
    }
  ]
}
```
{% endcode %}

### Select tokens of a specific type from a collection

{% code title=".specifyrc.json" lineNumbers="true" %}
```json
{
  "version": "2",
  "repository": "@organization/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Get color tokens from the 'Android' collection",
      "parsers": [
        {
          "name": "filter",
          "options": {
            "where": {
              "collection": "^Android$",
              "andWhere": {
                "token": ".*",
                "withTypes": { "include": ["color"] },
                "select": {
                  "token": true,
                  "parents": {
                    "collections": true
                  }
                }
              }
            }
          }
        }
      ]
    }
  ]
}
```
{% endcode %}

### Select all tokens from a collection and from groups matching a naming pattern

{% code title=".specifyrc.json" lineNumbers="true" %}
```json
{
  "version": "2",
  "repository": "@organization/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Get color tokens from the 'Android' collection and from all groups named 'components'",
      "parsers": [
        {
          "name": "filter",
          "options": {
            "where": {
              "collection": "^Android$",
              "andWhere": {
                "group": "^components$",
                "andWhere": {
                  "token": ".*",
                  "withTypes": {
                    "include": ["color"]
                  },
                  "select": {
                    "token": true,
                    "parents": true
                  }
                }
              }
            }
          }
        }
      ]
    }
  ]
}
```
{% endcode %}

### Select tokens from several groups with different names

{% code title=".specifyrc.json" lineNumbers="true" %}
```typescript
{
  "version": "2",
  "repository": "@organization/repository",
  "personalAccessToken": "<your-personal-access-token>",
  "rules": [
    {
      "name": "Get tokens from the group named 'Components' and/or from the group named 'Semantic'",
      "parsers": [
        {
          "name": "filter",
          "options": {
            "where": {
              "collection": "^Android$",
              "andWhere": {
                "group": "^Components$|^Semantic$",
                "andWhere": {
                  "token": ".*",
                  "select": {
                    "token": true,
                    "parents": true
                  }
                }
              }
            }
          }
        }
      ]
    }
  ]
}
```
{% endcode %}
