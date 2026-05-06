Scalable URL Shortener Service
A high-performance, distributed URL shortening system built with .NET Core and PostgreSQL, featuring a multi-layered caching strategy and a custom distributed ID generation logic to ensure massive scalability.

🚀 Key Features
Distributed ID Generation: Implements a Range-Based Token Handler pattern to prevent ID collisions across multiple API instances without hitting a central bottleneck for every request.

High Availability: Designed for horizontal scaling behind a Load Balancer, allowing for zero-downtime rolling deployments.

Intelligent Caching: Integrated Redis layer to reduce database load and provide sub-millisecond redirect speeds for popular links.

Stateless Architecture: API instances are completely stateless, allowing them to scale in and out based on demand (ideal for Azure App Service or Kubernetes).

Base62 Encoding: Converts internal numerical IDs into short, user-friendly alphanumeric strings (e.g., 1050 → gw).

🛠 Tech Stack
Backend: .NET Core (Web API)

Database: PostgreSQL

Cache: Redis (used for both data caching and range management)

Infrastructure: Azure App Service / Docker

🏗 System Architecture
The system utilizes a central Token Manager to delegate unique ranges of IDs to various API instances. This ensures that even if we scale to 50+ instances, each one can generate unique short URLs locally in memory.

The ID Generation Flow:
API Instance A requests a range from the Token Manager (e.g., Redis INCRBY).

Token Manager assigns range 1000-1999 and updates its global state.

API Instance A generates short URLs locally until the range is exhausted.

Encoding Service transforms the ID into a Base62 string for the final URL.

🏁 Getting Started
Prerequisites
.NET 8.0 SDK

PostgreSQL Instance

Redis Server
