---
layout: post
title: 'Generate C# Classes from JSON'
tags: ['C#', 'JSON']
categories: ['C#']
date: '2017-03-22 22:50'
author: 'GaryNg'
---

# Generate C# Classes from JSON
Use [json2csharp](http://json2csharp.com/)

# Example
```json
{
  "start": 0,
  "num_found": 1,
  "numFound": 1,
  "docs": [
    {
      "title_suggest": "Arduino In Action",
      "publisher": [
        "Manning Publications"
      ],
      "cover_i": 7615508,
      "isbn": [
        "1617290246",
        "9781617290244"
      ],
      "has_fulltext": false,
      "title": "Arduino In Action",
      "edition_key": [
        "OL26041428M"
      ],
      "last_modified_i": 1476438118,
      "edition_count": 1,
      "author_name": [
        "Joshua Noble"
      ],
      "cover_edition_key": "OL26041428M",
      "seed": [
        "/books/OL26041428M",
        "/works/OL17456639W",
        "/authors/OL3501238A"
      ],
      "first_publish_year": 2012,
      "publish_year": [
        2012
      ],
      "key": "/works/OL17456639W",
      "text": [
        "OL26041428M",
        "1617290246",
        "9781617290244",
        "Joshua Noble",
        "OL3501238A",
        "Arduino In Action",
        "/works/OL17456639W",
        "Manning Publications"
      ],
      "publish_date": [
        "2012"
      ],
      "author_key": [
        "OL3501238A"
      ],
      "type": "work",
      "ebook_count_i": 0
    }
  ]
}

```

generates

```csharp

public class Doc
{
    public string title_suggest { get; set; }
    public List<string> publisher { get; set; }
    public int cover_i { get; set; }
    public List<string> isbn { get; set; }
    public bool has_fulltext { get; set; }
    public string title { get; set; }
    public List<string> edition_key { get; set; }
    public int last_modified_i { get; set; }
    public int edition_count { get; set; }
    public List<string> author_name { get; set; }
    public string cover_edition_key { get; set; }
    public List<string> seed { get; set; }
    public int first_publish_year { get; set; }
    public List<int> publish_year { get; set; }
    public string key { get; set; }
    public List<string> text { get; set; }
    public List<string> publish_date { get; set; }
    public List<string> author_key { get; set; }
    public string type { get; set; }
    public int ebook_count_i { get; set; }
}

public class RootObject
{
    public int start { get; set; }
    public int num_found { get; set; }
    public int numFound { get; set; }
    public List<Doc> docs { get; set; }
}
```

# Reference
[json2csharp](http://json2csharp.com/)

# See Also
[JSON C# Class Generator](http://jsonclassgenerator.codeplex.com/)

GitHub: [JsonCSharpClassGenerator](https://github.com/JsonCSharpClassGenerator/JsonCSharpClassGenerator/)
