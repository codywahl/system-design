# Design a URL Shortener Like Bit.ly

https://www.hellointerview.com/learn/system-design/problem-breakdowns/bitly

## Understanding the Problem

**🔗 What is [Bit.ly](https://bitly.com/)?** Bit.ly is a URL shortening service that converts long URLs into shorter, manageable links. It also provides analytics for the shortened URLs.

### [Functional Requirements](https://www.hellointerview.com/learn/system-design/in-a-hurry/delivery#1-functional-requirements)

**Core Requirements**

1.  Users should be able to submit a long URL and receive a shortened version.

    - Optionally, users should be able to specify a custom alias for their shortened URL.

    - Optionally, users should be able to specify an expiration date for their shortened URL.

2.  Users should be able to access the original URL by using the shortened URL.

**Below the line (out of scope):**

- User authentication and account management.

- Analytics on link clicks (e.g., click counts, geographic data).

### [Non-Functional Requirements](https://www.hellointerview.com/learn/system-design/in-a-hurry/delivery#2-non-functional-requirements)

**Core Requirements**

1.  The system should ensure uniqueness for the short codes (no two long URLs can map to the same short URL)

2.  The redirection should occur with minimal delay (< 100ms)

3.  The system should be reliable and available 99.99% of the time (availability > consistency)

4.  The system should scale to support 1B shortened URLs and 100M DAU

**Below the line (out of scope):**

- Data consistency in real-time analytics.

- Advanced security features like spam detection and malicious URL filtering.

### [Defining the Core Entities](https://www.hellointerview.com/learn/system-design/in-a-hurry/delivery#3-defining-the-core-entities)

In a URL shortener, the core entities are very straightforward:

1.  **Original URL**: The original long URL that the user wants to shorten.

2.  **Short URL**: The shortened URL that the user receives and can share.

3.  **User**: Represents the user who created the shortened URL.

### [The API](https://www.hellointerview.com/learn/system-design/in-a-hurry/delivery#4-api-or-system-interface)

// Shorten a URL

```
POST /urls

{

"long_url": "https://www.example.com/some/very/long/url",

"custom_alias": "optional_custom_alias",

"expiration_date": "optional_expiration_date"

}

->

{

"short_url": "http://short.ly/abc123"

}
```

// Redirect to Original URL

```
GET /{short_code}

-> HTTP 302 Redirect to the original long URL
```

![Diagram](/diagrams/Bit.ly.jpg)
