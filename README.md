
# Team Poll System

A serverless polling API built with Azure Functions and Azure Service Bus.

Votes are submitted through an HTTP endpoint, processed asynchronously through a queue, and aggregated into poll results that can be retrieved through a results endpoint.

## Architecture

```mermaid
graph TB
    USER[Team Members] -->|POST /api/votes| SUBMIT[submitVote]
    SUBMIT --> QUEUE[Service Bus Queue]
    QUEUE --> PROCESS[processVote]
    PROCESS --> STORE[(Results Store)]

    VIEWER[Users] -->|GET /api/results/{pollId}| RESULTS[getResults]
    RESULTS --> STORE