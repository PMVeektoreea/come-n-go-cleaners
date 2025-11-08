System Architecture — Come 'n Go Cleaners
Overview

Come 'n Go Cleaners is a two sided platform that connects verified cleaners with customers who need short, hourly cleaning sessions. The system supports booking, matching, payments in naira via Quickteller or Interswitch, session tracking, and ratings.

This document explains the main components, how they communicate, and why the chosen approach is practical and scalable.

High level components

Client apps

Mobile app: React Native for iOS and Android

Web app: React for browser access and admin dashboard

API layer

Backend: Node.js with Express

Data layer

Primary database: MongoDB for flexible user, booking, and cleaner data

Optional cache: Redis for session data and fast availability checks

Payments

Quickteller or Interswitch integration for naira payments and webhook handling

Background services

Worker queue using Bull or Bee Queue for tasks such as notifications and background verification

Notifications

Push notifications via Firebase Cloud Messaging

SMS via a local SMS gateway if needed

Hosting and deployment

Cloud provider such as AWS, Render, or DigitalOcean

Containerization with Docker for consistency

CI pipeline for automated tests and deployments

Component responsibilities
Mobile and Web clients

Allow users to register, log in, and edit profiles

Allow cleaners to register and upload verification documents

Enable booking flow: select chores, hours, and location, see available cleaners, confirm booking

Show cleaner details and ratings

Trigger payment flow and display payment status

Display booking status updates and arrival ETAs

Collect ratings and feedback after sessions

Backend API

Expose REST endpoints for authentication, bookings, cleaner search, payments, and ratings

Handle business rules for matching, availability checks, and booking confirmation

Validate incoming requests and sanitize inputs

Send events to worker queue for long running operations

Implement webhooks to process payment confirmations from Quickteller or Interswitch

Database schema overview

Use collections for users, cleaners, bookings, payments, and ratings.

Example documents

User

{
  "userId": "uuid",
  "name": "Victoria",
  "phone": "+2348012345678",
  "email": "vic@example.com",
  "role": "customer",
  "createdAt": "2025-11-01T10:00:00Z"
}


Cleaner

{
  "cleanerId": "uuid",
  "name": "Aisha",
  "phone": "+2348012345679",
  "skills": ["sweeping", "laundry"],
  "hourlyRate": 2500,
  "verification": {
    "idCheck": true,
    "backgroundCheck": true,
    "verifiedAt": "2025-10-30T09:00:00Z"
  },
  "ratings": {
    "average": 4.8,
    "count": 42
  }
}


Booking

{
  "bookingId": "uuid",
  "customerId": "uuid",
  "cleanerId": "uuid",
  "startTime": "2025-11-05T14:00:00Z",
  "durationHours": 2,
  "status": "confirmed",
  "totalAmount": 5000,
  "paymentId": "pay_1234",
  "createdAt": "2025-11-03T08:00:00Z"
}


Payment

{
  "paymentId": "pay_1234",
  "bookingId": "uuid",
  "amount": 5000,
  "currency": "NGN",
  "provider": "Quickteller",
  "status": "completed",
  "providerReference": "qt_5678",
  "createdAt": "2025-11-05T14:05:00Z"
}

Payment integration flow

User confirms booking. Backend creates a pending booking record and a payment intent.

Backend calls Quickteller or Interswitch API to initiate payment. The API returns a payment reference and a redirect or payment token.

Client completes the payment using the provider flow. For card payments, use the provider's secure checkout or tokenization.

Provider sends a webhook to the backend when payment succeeds or fails.

Backend updates booking and payment records, marks booking as confirmed on success, and enqueues notifications for user and cleaner.

Security notes

Do not store raw card details. Use provider tokenization or hosted pages.

Sign and verify webhooks using provider signature header.

Use HTTPS for all API endpoints and require authentication tokens.

How components communicate

Client apps call the REST API over HTTPS.

The API interacts with MongoDB and Redis.

Long running or external tasks are queued to a worker using Redis as the broker.

Payment provider communicates with backend via webhooks.

Notifications are sent by worker processes to Firebase or SMS gateway.

Scalability and reliability

Use stateless backend services behind a load balancer to scale horizontally.

Offload heavy or slow tasks to background workers.

Use Redis for caching availability and rate limiting to reduce DB load.

Schedule backups and point in time recovery for the database.

Monitor using a simple stack such as Prometheus and Grafana or Sentry for errors.

Deployment and DevOps

Dockerize services with a Dockerfile for each service.

Use a CI pipeline to run tests and build images.

Deploy to a managed cloud service with auto scaling and health checks.

Maintain separate environments for development, staging, and production.

Observability and monitoring

Log structured events with correlation ids for tracing bookings and payments.

Capture metrics for API latency, error rate, and worker queue length.

Set alerts on failed payments, high error rates, and worker backlog.

Privacy and compliance

Store only necessary personal data and consider retention policy for PII.

Secure user and cleaner documents used for verification.

Make sure payment flows meet local regulations for payment processing.

Future considerations

Add a dispatcher service to optimize cleaner routing and reduce arrival times.

Introduce a microservice for analytics and reporting to support business decisions.

Add multi city support and currency adapters if expanding beyond Nigeria.

Local setup quick steps

Clone repo and install dependencies for backend and frontend.

Create environment variables for database URI, provider keys, and push notification keys.

Run the database locally or use a managed instance.

Start backend with npm run dev and frontend with npm start.

Run worker with node worker.js.

Example commit messages

Added initial system architecture document

Added payment integration flow for Quickteller

Added database schema examples for bookings and users