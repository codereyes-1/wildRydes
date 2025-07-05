# Wild Rydes

**Serverless Unicorn Ride‑Hailing on AWS**

**Wild Rydes** is a sample, end‑to‑end serverless application that demonstrates how to combine AWS managed services—**Amazon Cognito, API Gateway, AWS Lambda, DynamoDB, and Amplify**—to deliver a fully‑featured ride‑hailing web experience. Users register, sign in, pinpoint a pickup location on an interactive map, and summon a nearby unicorn (yes, really!).

## Table of Contents

- [Architecture Highlights](#architecture-highlights)
- [Tech Stack](#tech-stack)
- [Deployment / Installation](#deployment--installation)
- [Usage](#usage)
- [License](#license)

## Architecture Highlights

- **Static SPA hosted on Amplify** – Git‑based CI/CD automatically builds and deploys the HTML/CSS/JS front‑end to an S3‑backed hosting environment with global CDN acceleration.
- **Secure user management with Amazon Cognito** – The site leverages Cognito Hosted UI and Secure Remote Password (SRP) protocol for sign‑up, email verification, and JWT‑based authentication.
- **RESTful backend** – Amazon API Gateway exposes a `/ride` endpoint that triggers a Node.js AWS Lambda function, which writes ride requests to **Amazon DynamoDB** and returns unicorn assignment details.
- **Interactive mapping** – Client‑side JavaScript integrates Mapbox GL JS to let riders select pickup coordinates and animates the unicorn’s approach.
- **End‑to‑end serverless** – No servers to patch or scale; each component is managed and automatically scales with demand.

## Tech Stack

| Layer            | Technologies                                            |
| ---------------- | ------------------------------------------------------- |
| **Front‑End**    | HTML5 · CSS3 · JavaScript (ES6) · jQuery · Mapbox GL JS |
| **Auth**         | Amazon Cognito User Pools                               |
| **API**          | Amazon API Gateway (REST) · AWS Lambda (Node.js 20)     |
| **Data**         | Amazon DynamoDB (single‑table design)                   |
| **Hosting / CI** | AWS Amplify Console · Amazon S3 · Amazon CloudFront     |

## Deployment / Installation

### Prerequisites

- **AWS account** with Administrator credentials (for workshop/testing purposes)
- **Node.js 14+** and **npm** (for Amplify CLI)

### One‑Click Amplify Console Deploy (Recommended)

1. Fork this repo to your GitHub account.
2. Log in to the **AWS Amplify Console**.
3. Choose **“New App → Host web app”**, select **GitHub** as the source, and connect the forked repository.
4. Accept the default build settings—Amplify detects the static site and provisions an S3 bucket, CloudFront distribution, and CI pipeline.
5. Once build completes, the live URL is displayed. Proceed to configure the backend below.

### Provision Cognito, API Gateway, Lambda, and DynamoDB via Amplify CLI

```bash
# Install Amplify CLI if necessary
npm install -g @aws-amplify/cli

# Initialise the Amplify project (accept defaults)
cd wildRydes
amplify init

# Add authentication (Cognito User Pool)
amplify add auth

# Add REST API backed by Lambda function
amplify add api   # choose REST → Node.js  → /ride

# Add DynamoDB table for RideRequests
amplify add storage   # select NoSQL → Amazon DynamoDB → single table

# Deploy all resources
aut amplify push   # typo? should be: amplify push

# Publish the front‑end to Amplify hosting
amplify publish
```

Amplify outputs the `` of the API and rewrites `js/config.js` at build time, wiring the front‑end to the freshly deployed backend.

> **Note:** If you prefer manual CloudFormation/SAM deployment, refer to the original [AWS Serverless Workshops](https://github.com/aws-samples/aws-serverless-workshops) for step‑by‑step templates.

## Usage

1. Navigate to the Amplify‑hosted URL and **Sign Up** with a valid email address.
2. Verify your email via the Cognito Hosted UI flow.
3. **Sign In**; the application stores Cognito‑issued JWTs in memory.
4. Click **“Set Pickup”** on the map, place the marker, then **“Request Unicorn.”**
5. Watch as your assigned unicorn gallops toward the pickup point—status updates are streamed from the `/ride` Lambda response.

## License

Distributed under the **MIT‑0 License**—a permissive variant identical to MIT but with an explicit “no attribution required” clause. See the [`LICENSE`](LICENSE) file for details.

