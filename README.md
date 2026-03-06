Scalable URL Shortener

A production-inspired URL Shortener system that converts long URLs into compact short links and redirects users with minimal latency.
This project demonstrates system design principles, microservice architecture, caching strategies, and CI/CD practices used in large-scale systems.

The platform allows users to create shortened URLs, redirect to original links instantly, and track usage analytics such as click counts.

Project Overview

A URL Shortener works by mapping a long URL to a shorter alias that can be shared easily. When a user accesses the shortened URL, the system retrieves the original URL and redirects the user.

Example:

Original URL
https://www.example.com/articles/how-to-build-a-distributed-system

Short URL
https://short.ly/a82c7w

When a user opens the short URL, the service quickly redirects them to the original destination.

This project is designed to simulate real-world large-scale systems handling millions of URLs and high read traffic.

Features
URL Shortening

Users can input a long URL and receive a unique shortened link.

Fast Redirection

Short URLs redirect users to the original link with minimal latency.

Analytics Tracking

Tracks the number of times each shortened URL is accessed.

Caching

Uses an in-memory cache to reduce database load and speed up redirection.

Scalable Architecture

Designed to handle high read traffic with a read-heavy architecture.

DevOps Integration

Includes containerization and CI/CD pipeline setup.

System Architecture

The system follows a microservice-based architecture where different services handle different responsibilities.

                Internet
                   |
                Nginx
                   |
            ----------------
            |              |
         Next.js        Redirect Service
        (Frontend)       (Node.js)
            |                |
        URL Service        Redis
          (Node.js)          |
            |             MongoDB
            |
        MongoDB
Technology Stack
Frontend

Next.js

Backend

Node.js

Express.js

Database

MongoDB

Caching

Redis

Reverse Proxy

Nginx

DevOps

Docker

GitLab CI/CD

SonarCloud

How the System Works
1. URL Creation Flow

User submits a long URL through the frontend.

The request is sent to the URL service.

A unique ID is generated.

The ID is encoded using Base62 encoding.

The short URL mapping is stored in the database.

The shortened URL is returned to the user.

2. URL Redirection Flow

User opens the short URL.

The request reaches the redirect service.

The service first checks the cache for the original URL.

If found, it instantly redirects the user.

If not found, the database is queried.

The result is cached for future requests.

3. Analytics Tracking

Every redirect request generates an event that increments the click counter for that URL.
Analytics data can be used to track link popularity and usage patterns.

Project Structure
url-shortener
│
├── frontend
│   ├── pages
│   ├── components
│   └── services
│
├── url-service
│   ├── controllers
│   ├── routes
│   ├── models
│   └── utils
│
├── redirect-service
│   ├── controllers
│   ├── routes
│   └── cache
│
├── analytics-worker
│
├── infrastructure
│   ├── docker
│   └── nginx
│
├── docker-compose.yml
└── README.md
API Endpoints
Create Short URL
POST /api/urls

Request

{
  "url": "https://example.com"
}

Response

{
  "shortUrl": "https://short.ly/a82c7w"
}
Redirect URL
GET /{shortId}

Response

302 Redirect → Original URL
Get Analytics
GET /api/analytics/{shortId}

Response

{
  "clicks": 1520
}
Scaling Strategy

To handle high traffic, the system implements several scaling techniques:

Horizontal Scaling

Multiple instances of services can run behind a load balancer.

Caching

Redis reduces database queries for frequently accessed URLs.

Sharding

Data can be distributed across multiple database shards based on URL prefixes.

Asynchronous Analytics

Analytics updates can be processed asynchronously to avoid slowing down redirects.

Future Improvements

Possible enhancements include:

Custom short URLs

URL expiration support

Geo-based analytics

Rate limiting

QR code generation for links

Distributed event streaming for analytics

Global CDN integration

Learning Objectives

This project demonstrates concepts such as:

Distributed system design

Caching strategies

High availability architecture

Microservices

Horizontal scalability

CI/CD pipelines

Backend performance optimization

License

This project is open-source and available for learning and educational purposes.
