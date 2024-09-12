---
layout: default
title: Lowercase
parent: Token filters
nav_order: 260
---

# Lowercase token filter

The `lowercase` token filter in OpenSearch is used to convert all characters in the token stream to lowercase, making searches case-insensitive.

## Parameters

The `lowercase` token filter in OpenSearch can be configured with parameter `language`. The possible options are: [`greek`](https://lucene.apache.org/core/8_7_0/analyzers-common/org/apache/lucene/analysis/el/GreekLowerCaseFilter.html), [`irish`](https://lucene.apache.org/core/8_7_0/analyzers-common/org/apache/lucene/analysis/ga/IrishLowerCaseFilter.html) and [`turkish`](https://lucene.apache.org/core/8_7_0/analyzers-common/org/apache/lucene/analysis/tr/TurkishLowerCaseFilter.html). Default is [Lucene’s LowerCaseFilter](https://lucene.apache.org/core/8_7_0/analyzers-common/org/apache/lucene/analysis/core/LowerCaseFilter.html). (String, _Optional_)

## Example

The following example request creates a new index named `custom_lowercase_example` and configures an analyzer with `lowercase` filter with Greek `language`:

```json
PUT /custom_lowercase_example
{
  "settings": {
    "analysis": {
      "analyzer": {
        "greek_lowercase_example": {
          "type": "custom",
          "tokenizer": "standard",
          "filter": ["greek_lowercase"]
        }
      },
      "filter": {
        "greek_lowercase": {
          "type": "lowercase",
          "language": "greek"
        }
      }
    }
  }
}
```
{% include copy-curl.html %}

## Generated tokens

Use the following request to examine the tokens generated using the analyzer:

```json
GET /custom_lowercase_example/_analyze
{
  "analyzer": "greek_lowercase_example",
  "text": "Αθήνα ΕΛΛΑΔΑ"
}
```
{% include copy-curl.html %}

The response contains the generated tokens:

```json
{
  "tokens": [
    {
      "token": "αθηνα",
      "start_offset": 0,
      "end_offset": 5,
      "type": "<ALPHANUM>",
      "position": 0
    },
    {
      "token": "ελλαδα",
      "start_offset": 6,
      "end_offset": 12,
      "type": "<ALPHANUM>",
      "position": 1
    }
  ]
}
```
