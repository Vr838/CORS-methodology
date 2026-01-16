## Proof of Concept (PoC)

The `poc/` directory contains HTML-based proof-of-concept files
demonstrating CORS misconfigurations.

### Included PoCs
- `cors-get-poc.html` – Credentialed cross-origin GET request
- `cors-post-poc.html` – Credentialed cross-origin POST request

### How It Works
- Uses `XMLHttpRequest` with `withCredentials = true`
- Sends requests from a malicious origin
- Exploits misconfigured `Access-Control-Allow-Origin`
- Requires `Access-Control-Allow-Credentials: true`

### Usage
Open the HTML file from any external origin (e.g., localhost or attacker domain)
while logged into the target application.

> **Note:** All domains are placeholders. Testing must be performed only on
authorized targets.
