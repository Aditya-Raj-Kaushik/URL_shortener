Scalable URL Shortener

A high-performance URL Shortener built with a microservice architecture that converts long URLs into short, shareable links and redirects users with minimal latency.

This project demonstrates real-world backend engineering practices, including caching, scalable system design, event-driven analytics, and DevOps automation.

The system is designed to simulate production-grade services similar to Bitly or TinyURL, focusing on high read throughput and low latency redirects.

Key Features

Generate short URLs from long links

Instant redirection using cached lookups

Click analytics tracking

Redis-based caching for fast reads

Microservice-based backend architecture

Containerized services with Docker

CI/CD pipeline integration

Code quality checks with SonarCloud

Example
Original URL
https://www.example.com/blog/how-distributed-systems-work

Shortened URL
https://short.ly/a82c7w

Visiting the shortened URL automatically redirects the user to the original destination.

Architecture Overview

The system is designed with separation of concerns so that different services can scale independently.

                Internet
                   |
                Nginx
                   |
          ---------------------
          |                   |
       Next.js            Redirect Service
      (Frontend)            (Node.js)
          |                     |
      URL Service             Redis
       (Node.js)                |
          |                  MongoDB
       MongoDB
          |
     Analytics Worker
Services

Frontend

User interface for creating short URLs

Dashboard for viewing analytics

URL Service

Generates unique short IDs

Stores URL mappings in the database

Redirect Service

Handles incoming short URL requests

Uses Redis to quickly retrieve original URLs

Analytics Worker

Tracks clicks and usage statistics

Tech Stack
Frontend

Next.js

Backend

Node.js

Express.js

Data Layer

MongoDB

Redis

Infrastructure

Docker

Nginx

DevOps

GitLab CI/CD

SonarCloud

How It Works
1. URL Shortening

User submits a long URL through the frontend

The request is sent to the URL Service

A unique ID is generated

The ID is encoded using Base62

The mapping is stored in MongoDB

A short URL is returned

2. URL Redirection

User accesses the short URL

Redirect service checks Redis cache

If cache hit → redirect immediately

If cache miss → fetch from MongoDB

Cache the result and redirect

This ensures low latency and reduced database load.

3. Analytics Tracking

Each redirect event increments a click counter associated with the short URL.

Analytics data can be used to measure:

total clicks

popularity of links
