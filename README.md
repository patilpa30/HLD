# HLD
🏗️ High-Level System Design Components

This document explains the core components of a typical scalable web application architecture. Understanding these components is essential for System Design interviews.

🌐 1. User (Web Browser / Mobile App)
What is it?

The User is the client interacting with the application. This can be a web browser, mobile application, or any client capable of making HTTP requests.

Examples:

Chrome
Firefox
Safari
Android App
iOS App

Example Request

GET /products/15

or

POST /login
Why do we need it?

Every application begins with a client request. The user sends requests to access data, perform actions, or interact with the application.

Interview Explanation

The user is the entry point of the system. It sends HTTP requests through a browser or mobile application. Before the request reaches our servers, the domain name is resolved using DNS.

🌍 2. DNS (Domain Name System)
What is it?

DNS translates a human-readable domain name into an IP address that computers can understand.

Example

amazon.com
        ↓
54.239.xxx.xxx

Instead of remembering an IP address, users simply type the website name.

Why do we need it?

Humans remember names much more easily than IP addresses.

Without DNS, users would have to access websites using numeric IP addresses.

Real-Life Example
youtube.com
        ↓
142.250.xxx.xxx
Interview Explanation

DNS converts the domain name into an IP address, allowing the client to locate the destination server.

🚀 3. CDN (Content Delivery Network)
What is it?

A CDN stores copies of static content at multiple locations around the world so users can download files from the nearest server.

Without CDN

India
   ↓
USA Server
   ↓
Image Download

With CDN

India
   ↓
Mumbai CDN
   ↓
Image Download
What does a CDN cache?

✅ Images

✅ CSS

✅ JavaScript

✅ Videos

✅ Fonts

❌ Login APIs

❌ Payment APIs

❌ Database Queries

Why do we need it?
Reduces latency
Improves page load time
Reduces load on the origin server
Real-Life Examples
Instagram Profile Pictures
Netflix Images
Amazon Product Images
Interview Explanation

A CDN caches static assets close to users, reducing latency and improving application performance.

⚖️ 4. Load Balancer
What is it?

A Load Balancer distributes incoming requests across multiple servers.

Without Load Balancer

10,000 Users
      ↓
One Server

If the server crashes, the application becomes unavailable.

With Load Balancer

Users
   ↓
Load Balancer
   ↓
Server A
Server B
Server C
Why do we need it?
Prevent server overload
High Availability
Horizontal Scaling
Fault Tolerance
Popular Load Balancers
NGINX
HAProxy
AWS Application Load Balancer
Interview Explanation

A Load Balancer distributes incoming traffic across multiple servers to improve scalability, availability, and fault tolerance.

💻 5. Web Servers
What are they?

Web servers host the backend application and execute business logic.

Examples

FastAPI
Spring Boot
ASP.NET Core
Node.js
Django

Example

GET /users/15

The web server

Validates the request
Executes business logic
Checks cache
Reads database
Returns JSON
Why do we need them?

They process all incoming API requests and coordinate communication with databases, caches, and other services.

Interview Explanation

Web servers execute application logic, validate requests, and communicate with databases, caches, and external services.

🗄️ 6. Database
What is it?

The database stores permanent application data.

Examples

Users
Orders
Payments
Products
Comments

Popular SQL Databases

PostgreSQL
MySQL
SQL Server
Oracle

Example Query

SELECT *
FROM Users
WHERE Id = 15;
Why do we need it?

To store structured, reliable, and persistent data.

When should SQL be used?
Banking Systems
E-Commerce Orders
Payment Systems
Inventory Management
Interview Explanation

Relational databases provide ACID transactions and maintain data consistency for structured information.

⚡ 7. Cache
What is it?

A cache stores frequently accessed data in memory.

Without Cache

User
   ↓
Database

Every request hits the database.

With Cache

User
   ↓
Cache
   ↓
Database (only if needed)
Popular Technologies
Redis
Memcached
Real-Life Examples
Trending Products
User Sessions
Homepage Data
Frequently Viewed Products
Cache Flow

First Request

User
   ↓
Database
   ↓
Cache

Second Request

User
   ↓
Cache
Why do we need it?
Faster responses
Reduced database load
Better scalability
Interview Explanation

Cache stores frequently accessed data in memory, reducing database load and improving response time.

📨 8. Message Queue
What is it?

A Message Queue allows long-running tasks to be processed asynchronously instead of making users wait.

Imagine a user uploads a video.

Should the user wait 5 minutes while the server processes it?

No.

Instead, the application places the task into a Message Queue, immediately returns a success response to the user, and lets a background Worker process the video later.

Flow

User Uploads Video
        ↓
Web Server
        ↓
Message Queue
        ↓
200 OK Response
        ↓
Worker Processes Video
Popular Technologies
RabbitMQ
Apache Kafka
Amazon SQS
Azure Service Bus
Real-Life Use Cases
Email Notifications
SMS Sending
Video Processing
Image Resizing
PDF Generation
Payment Confirmation
Background Jobs
Why do we need it?
Faster API responses
Better scalability
Decouples services
Improves reliability
Interview Explanation

A Message Queue decouples services by allowing long-running tasks to be processed asynchronously without blocking the user's request.

👷 9. Workers
What are they?

Workers continuously listen to the Message Queue and execute background tasks.

Example

Queue

Send Welcome Email

Worker

Reads Job
      ↓
Sends Email
      ↓
Marks Job Completed
Real-Life Use Cases
Sending Emails
Processing Videos
Image Compression
Generating Reports
Notification Services
Why do we need them?

They prevent users from waiting for time-consuming operations.

Interview Explanation

Workers process background jobs asynchronously, improving user experience and overall system throughput.

📄 10. NoSQL Database
What is it?

A NoSQL database stores unstructured or semi-structured data and scales horizontally.

Popular Databases

MongoDB
Cassandra
DynamoDB
Real-Life Examples
Chat Messages
User Activity
Social Media Posts
Analytics
IoT Data
Why not SQL?

Different posts may have different structures.

Example

Post 1

Text

Post 2

Text
Images

Post 3

Text
Videos
Poll

NoSQL handles flexible schemas much better.

Interview Explanation

NoSQL databases are ideal for large-scale applications requiring schema flexibility and horizontal scalability.

📜 11. Logging
What is it?

Logging records application events and errors.

Examples

INFO    User Logged In

WARNING Invalid Token

ERROR   Database Timeout
Popular Tools
ELK Stack
Splunk
Grafana Loki
Why do we need it?

Logs help developers debug issues and audit system behavior.

Interview Explanation

Logging captures application events, making debugging and troubleshooting possible.

📊 12. Metrics
What are Metrics?

Metrics provide numerical measurements of system health.

Examples

CPU Usage
Memory Usage
Requests per Second
Error Rate
Response Time

Popular Tools

Prometheus
Grafana
CloudWatch
Why do we need them?

Metrics help measure application performance and identify bottlenecks.

Interview Explanation

Metrics provide quantitative insights into application performance and health.

🔍 13. Monitoring
What is Monitoring?

Monitoring continuously watches application metrics and alerts engineers when issues occur.

Example

CPU > 90%
        ↓
Alert Sent

or

Database Down
       ↓
Slack Notification
Popular Tools
Grafana
Prometheus Alertmanager
Datadog
New Relic
Why do we need it?

Monitoring helps detect failures before users are significantly affected.

Interview Explanation

Monitoring continuously observes system health and sends alerts whenever predefined thresholds are exceeded.

🤖 14. Automation
What is Automation?

Automation eliminates repetitive manual work by automatically performing operational tasks.

Examples

Deploying Applications
Scaling Servers
Database Backups
Infrastructure Provisioning
Restarting Failed Services

Popular Tools

Kubernetes
Terraform
Jenkins
GitHub Actions
Ansible
Why do we need it?

Automation improves consistency, reduces human error, and speeds up deployments and recovery.

Interview Explanation

Automation manages deployments, scaling, backups, and infrastructure tasks without manual intervention.

🔄 Complete Request Flow
User
   ↓
DNS
   ↓
CDN (Static Content)
   ↓
Load Balancer
   ↓
Web Server
   ↓
Cache
   ↓
Database
   ↓
Message Queue (if asynchronous work is required)
   ↓
Workers

Meanwhile,

Logging records application events.
Metrics collect performance data.
Monitoring watches the system and raises alerts.
Automation manages deployments, scaling, and recovery.
🎯 Interview Summary (One-Line Answers)
Component	One-Line Interview Answer
User	Sends requests to interact with the application.
DNS	Converts a domain name into an IP address.
CDN	Delivers static content from the nearest server to reduce latency.
Load Balancer	Distributes requests across multiple servers for scalability and high availability.
Web Server	Executes business logic and handles client requests.
Database	Stores structured, persistent application data.
Cache	Stores frequently accessed data in memory for faster responses.
Message Queue	Handles long-running tasks asynchronously without blocking users.
Worker	Processes background jobs from the message queue.
NoSQL	Stores flexible, high-volume data with horizontal scalability.
Logging	Records events and errors for debugging and auditing.
Metrics	Measures system performance and health.
Monitoring	Observes system metrics and sends alerts on failures.
Automation	Automates deployments, scaling, and operational tasks.
