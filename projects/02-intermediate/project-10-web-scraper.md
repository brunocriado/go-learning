# Project 10: Concurrent Web Scraper

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a high-performance web scraper using Go's Colly framework. Learn web scraping techniques, rate limiting, concurrent crawling, and data extraction patterns.

**Difficulty:** Intermediate  
**Estimated Time:** 20-30 hours  
**Category:** Web Scraping, Data Extraction

## Prerequisites

- Completed [Project 8: WebSocket Chat](project-08-websocket-chat.md)
- Understanding of HTML/CSS selectors
- HTTP protocol knowledge

**Required Packages:**
```bash
go get github.com/gocolly/colly/v2
go get github.com/PuerkitoBio/goquery
```

## What You'll Learn

- Web scraping with Colly
- HTML parsing with goquery
- CSS selectors and XPath
- Rate limiting and politeness
- Concurrent crawling
- Handling pagination
- JavaScript-rendered pages
- Proxy rotation
- User-agent rotation
- Data storage and export

## Core Features

### 1. Basic Scraping
- HTML parsing
- CSS selectors
- Data extraction
- Link following
- Depth limiting

### 2. Advanced Features
- JavaScript execution
- Login/authentication
- Cookie handling
- Form submission
- File downloads

### 3. Politeness & Ethics
- robots.txt respect
- Rate limiting
- Request delays
- Concurrent request limits
- User-agent headers

### 4. Data Management
- CSV/JSON export
- Database storage
- Duplicate detection
- Data validation
- Error handling

## Implementation Guide

### Basic Scraper

```go
package main

import (
    "fmt"
    "github.com/gocolly/colly/v2"
)

type Product struct {
    Name  string
    Price string
    URL   string
}

func main() {
    c := colly.NewCollector(
        colly.AllowedDomains("example.com"),
        colly.MaxDepth(2),
    )
    
    // Rate limiting
    c.Limit(&colly.LimitRule{
        DomainGlob:  "*",
        Parallelism: 2,
        Delay:       1 * time.Second,
    })
    
    var products []Product
    
    // Extract product data
    c.OnHTML(".product", func(e *colly.HTMLElement) {
        product := Product{
            Name:  e.ChildText(".product-name"),
            Price: e.ChildText(".price"),
            URL:   e.Attr("href"),
        }
        products = append(products, product)
    })
    
    // Follow pagination
    c.OnHTML("a.next-page", func(e *colly.HTMLElement) {
        c.Visit(e.Request.AbsoluteURL(e.Attr("href")))
    })
    
    // Error handling
    c.OnError(func(r *colly.Response, err error) {
        fmt.Println("Error:", err)
    })
    
    c.Visit("https://example.com/products")
    
    // Export to JSON
    saveToJSON(products, "products.json")
}
```

### Concurrent Scraper with Queue

```go
import (
    "github.com/gocolly/colly/v2"
    "github.com/gocolly/colly/v2/queue"
)

func scrapeWithQueue() {
    c := colly.NewCollector()
    
    q, _ := queue.New(
        2, // Number of consumer threads
        &queue.InMemoryQueueStorage{MaxSize: 10000},
    )
    
    c.OnHTML("a[href]", func(e *colly.HTMLElement) {
        q.AddURL(e.Request.AbsoluteURL(e.Attr("href")))
    })
    
    // Add seed URLs
    q.AddURL("https://example.com")
    
    q.Run(c)
}
```

### robots.txt Respecting Scraper

```go
import "github.com/gocolly/colly/v2/extensions"

func main() {
    c := colly.NewCollector()
    
    // Respect robots.txt
    extensions.Referer(c)
    extensions.RandomUserAgent(c)
    
    // Check robots.txt before visiting
    c.CheckHead = true
    
    c.Visit("https://example.com")
}
```

## Project Structure

```
web-scraper/
├── main.go
├── scraper/
│   ├── collector.go
│   ├── parser.go
│   └── exporter.go
├── models/
│   └── product.go
├── storage/
│   ├── csv.go
│   ├── json.go
│   └── database.go
├── config/
│   └── config.yaml
└── README.md
```

## Testing Strategy

- Mock HTTP responses for tests
- Test HTML parsing
- Validate data extraction
- Test rate limiting
- Error handling scenarios

## Challenges & Solutions

### Challenge 1: JavaScript Content
**Problem:** Dynamic content not in HTML  
**Solution:** Use chromedp or selenium for browser automation

### Challenge 2: Getting Blocked
**Problem:** Website blocking requests  
**Solution:** Rotate user agents, use proxies, respect rate limits

### Challenge 3: Pagination
**Problem:** Different pagination patterns  
**Solution:** Pattern detection, query parameter manipulation

## Best Practices

1. Always respect robots.txt
2. Use reasonable rate limits
3. Identify your scraper (User-Agent)
4. Handle errors gracefully
5. Cache responses when possible
6. Monitor for structure changes
7. Consider API alternatives first

## Next Steps

- Add proxy support
- Implement browser automation
- Create scheduled scraping
- Move to [Project 11: CLI System Monitor](project-11-system-monitor.md)

## Resources

- [Colly Documentation](http://go-colly.org/)
- [Web Scraping Best Practices](https://github.com/colly)

---

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)
