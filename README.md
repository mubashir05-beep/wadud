# Phase One – Tele‑Consultation Platform: **Wadud**

> **Al Wadud - The Loving:** The one who loves those who do good and bestows on them His compassion.

> **Goal:** Build a production‑ready, scalable Phase One system (not a throwaway MVP) that supports web + mobile users, doctors, and admins, with modular backend services, event‑driven architecture, and custom real‑time communication.

---

## 1. Product Scope (Phase One)

Phase One focuses on **core consultations, scheduling, payments, and real‑time communication**, with compliance‑ready foundations and scalability across regions.

Regions supported architecturally from day one (feature‑flagged):

* Pakistan (primary)
* Middle East (UAE, Qatar, Saudi – primary)

---

## 2. High‑Level Architecture

### Architectural Principles

* Modular microservices (independently deployable)
* Event‑driven communication (async by default)
* Region‑aware design (multi‑region later without rewrite)
* Minimal third‑party dependencies (core infra in‑house)
* Horizontal scalability from Phase One

### System Overview

* **API Gateway (BFF)** – Next.js
* **Core Backend Services** – Golang
* **Real‑Time Layer** – WebRTC + WebSockets
* **Event Bus** – Kafka / NATS
* **Data Layer** – PostgreSQL + Redis
* **Media Infrastructure** – Self‑hosted WebRTC SFU

---

## 3. Monorepo & Repo Strategy

### Recommendation: **Turborepo** (Primary Choice)

**Why Turborepo over Nx:**

* Lighter mental overhead
* Faster setup for Next.js + Go hybrid
* Excellent CI caching
* Ideal when frontend is the main orchestrator

Nx can be introduced later if orchestration complexity increases.

### Repo Structure (Example)

```
apps/
  web-user (Next.js)
  web-admin (Next.js)
  mobile (React Native / Expo)
  api-gateway (Next.js BFF)
services/
  auth-service (Go)
  user-service (Go)
  doctor-service (Go)
  booking-service (Go)
  payment-service (Go)
  notification-service (Go)
  chat-service (Go)
  webrtc-service (Go)
packages/
  shared-types
  ui-components
  proto / contracts
infra/
  terraform
  k8s
```

---

## 4. Core Backend Services (Phase One)

### 4.1 Authentication Service

* JWT + Refresh Tokens
* OAuth ready (Google / Apple – optional)
* Anonymous user sessions
* Role‑based access control (User / Doctor / Admin)

**Tech:** Golang, PostgreSQL, Redis

---

### 4.2 User Service

* User profile (anonymous or identified)
* Medical history (basic – Phase One)
* Consent management
* Region & language preferences

---

### 4.3 Doctor Service

* Doctor onboarding
* License & credential upload
* Availability scheduling
* Consultation history
* Earnings dashboard (Phase One basic)

---

### 4.4 Booking & Consultation Service

* Slot‑based & instant consultations
* Queue‑based matching (future‑ready)
* Consultation lifecycle

  * Requested
  * Accepted
  * In‑Progress
  * Completed
  * Cancelled

---

### 4.5 Payment Service

* Payment intent creation
* Commission calculation (platform %)
* Payout ledger (doctors)
* Multi‑gateway abstraction layer

**Gateways (Phase One):**

* Pakistan: JazzCash / EasyPaisa / Bank Transfer
* Future: Stripe / Checkout.com

---

### 4.6 Notification Service

* Push notifications (FCM / APNs)
* Email scheduling
* SMS hooks (future)

---

### 4.7 Chat Service (Custom)

* One‑to‑one chat
* Secure message storage
* Typing indicators
* File sharing (images/docs – limited)

**Tech:**

* WebSockets
* Redis Pub/Sub
* PostgreSQL for persistence

---

### 4.8 WebRTC Service

**Core Requirements:**

* Audio + video calls
* Screen sharing (Phase One optional)
* Call recording hooks (future)

**Infrastructure:**

* WebRTC SFU (mediasoup / ion‑sfu)
* TURN/STUN servers
* Region‑aware media routing

**Scalability Strategy:**

* Stateless signaling servers
* SFU horizontal scaling
* Separate media plane from control plane

---

## 5. Frontend Applications

### 5.1 User Web App (Next.js)

* Anonymous onboarding
* Doctor discovery
* Booking & payments
* Chat & video calls
* Consultation history

---

### 5.2 Mobile App (React Native)

* Full parity with web user app
* Push notifications
* Optimized video experience

---

### 5.3 Doctor Web App

* Availability management
* Consultation queue
* Earnings overview
* Chat & video

---

### 5.4 Admin Web Panel

* Doctor verification
* User management
* Consultation analytics
* Payment oversight
* Content moderation

---

## 6. Event‑Driven Backbone

### Events (Examples)

* UserRegistered
* DoctorOnboarded
* ConsultationStarted
* ConsultationCompleted
* PaymentCaptured
* NotificationTriggered

**Tech Choice:**

* Kafka (scale) OR NATS (simplicity Phase One)

---

## 7. Data & Storage

* PostgreSQL (primary relational DB)
* Redis (sessions, queues, caching)
* Object storage (S3‑compatible – MinIO initially)

---

## 8. Observability & DevOps

### Mandatory from Phase One

* Structured logging
* Metrics (Prometheus)
* Tracing (OpenTelemetry)
* Error tracking

### Infrastructure

* Docker everywhere
* Kubernetes (EKS / GKE / self‑hosted later)
* Terraform for infra as code

---

## 9. Security & Compliance (Foundational)

* Encrypted data at rest & in transit
* Secure media channels (DTLS/SRTP)
* Audit logs
* Consent tracking
* Region‑based data isolation (future)

---

## 10. Third‑Party Fallbacks (Optional)

* Zoom SDK (temporary fallback for video)
* Email: SES / SendGrid

Used only if WebRTC is delayed.

---

## 11. Phase One Deliverables

* Production‑ready backend services
* Web + Mobile apps
* Admin panel
* Custom chat + video
* Payments & notifications
* Scalable infra

---

## 12. Phase Two (Not in Scope Yet)

* Pharmacy integration
* Insurance support
* AI triage
* Cross‑border payments
* Desktop doctor app

---

**This Phase One of "Wadud" is designed to evolve directly into production without architectural rewrites.**
