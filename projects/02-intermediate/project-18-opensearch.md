# Project 18: OpenSearch/Elasticsearch Integration

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a search engine API using OpenSearch/Elasticsearch. Learn full-text search, aggregations, and search optimization.

**Difficulty:** Intermediate  
**Estimated Time:** 35-50 hours

## Prerequisites

**Required Packages:**
```bash
go get github.com/opensearch-project/opensearch-go
```

## What You'll Learn

- Full-text search
- Query DSL
- Aggregations
- Bulk indexing
- Search ranking
- Faceted search

## Implementation Guide

```go
package main

import (
    "github.com/opensearch-project/opensearch-go"
)

type SearchService struct {
    client *opensearch.Client
}

func (s *SearchService) Search(query string) ([]Product, error) {
    res, err := s.client.Search(
        s.client.Search.WithIndex("products"),
        s.client.Search.WithBody(strings.NewReader(`{
            "query": {
                "multi_match": {
                    "query": "`+query+`",
                    "fields": ["name^3", "description", "tags"]
                }
            },
            "aggs": {
                "categories": {
                    "terms": {"field": "category"}
                }
            }
        }`)),
    )
    
    // Parse results
    var products []Product
    // ... parse JSON response
    
    return products, nil
}
```

## Project Structure

```
opensearch-api/
├── main.go
├── search/
│   ├── service.go
│   ├── indexer.go
│   └── query.go
└── README.md
```

## Congratulations!

You've completed all Intermediate projects! Move to [Advanced Projects](../03-advanced/README.md).

---

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)
