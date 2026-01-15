# Web Application CORS Testing Methodology

## Overview
This document describes my end-to-end, structured, and ethical approach to identifying Cross-Origin Resource Sharing (CORS) misconfigurations in web applications.

The methodology focuses on discovering **real-world, impactful CORS issues** that could enable unauthorized cross-origin access to authenticated or sensitive resources.

All testing is performed strictly within authorized scope and in accordance with responsible disclosure principles.

---

## Scope & Ethical Guidelines

- Testing only on authorized targets (bug bounty programs, labs, or owned assets)
- No denial-of-service, brute force, or mass exploitation
- Minimal proof-of-concept testing
- No data exfiltration, storage, or misuse
- Immediate responsible disclosure upon validation

---

## Phase 1: Asset & Endpoint Discovery

**Objective:** Identify reachable assets and endpoints where CORS logic may be implemented.

### Activities
- Discover live subdomains and services
- Identify API, backend, and internal-facing endpoints
- Collect historical and archived URLs
- Normalize and deduplicate discovered endpoints

### Rationale
CORS misconfigurations typically occur on API and backend endpoints rather than static content.

---

## Phase 2: Endpoint Prioritization & Filtering

**Objective:** Reduce noise and focus on endpoints with higher security impact.

### Prioritization Criteria
- REST or GraphQL APIs
- Authentication and session-related routes
- User, account, or profile management functionality
- Internal, admin, or backend services
- Billing, reporting, file handling, or data export features

Endpoints that meet these criteria are shortlisted for further analysis.

---

## Phase 3: Initial CORS Behavior Analysis

**Objective:** Observe how the application responds to cross-origin requests.

### Testing Approach
- Send requests with a custom, untrusted `Origin` header
- Analyze response headers for CORS-related behavior

### Headers of Interest
- `Access-Control-Allow-Origin`
- `Access-Control-Allow-Credentials`
- `Access-Control-Allow-Headers`
- `Access-Control-Allow-Methods`

---

## Phase 4: Misconfiguration Identification

**Objective:** Detect insecure CORS patterns.

A potential CORS issue is identified when:
- The application reflects the supplied Origin value, **and**
- Credentialed requests are explicitly allowed

### Example (Redacted)
```http
Access-Control-Allow-Origin: https://evil.example
Access-Control-Allow-Credentials: true
