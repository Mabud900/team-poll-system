# Team Poll System

A serverless polling API built with Azure Functions and Azure Service Bus.

Votes are submitted through an HTTP endpoint, processed asynchronously through a queue, and stored as aggregated poll results.

## Architecture

```mermaid
graph TB
    USER[Team Members] -->|POST /api/votes| SUBMIT[submitVote]
    SUBMIT --> QUEUE[Service Bus Queue]
    QUEUE --> PROCESS[processVote]
    PROCESS --> STORE[(Results Store)]

    VIEWER[Users] -->|GET /api/results/{pollId}| RESULTS[getResults]
    RESULTS --> STORE
```

## Flow

1. A user submits a vote through the API.
2. The vote is placed onto a Service Bus queue.
3. A queue-triggered function processes and stores the vote.
4. Results can be retrieved through the results endpoint.

## Project Structure

```text
├── src/
│   ├── functions/
│   └── lib/
├── infra/
├── scripts/
├── host.json
├── package.json
└── local.settings.example.json
```