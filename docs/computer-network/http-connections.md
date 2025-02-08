# Comparison of HTTP Connection Types

Here's a comparison of Persistent HTTP with Pipelining, Non-Persistent HTTP, and Non-Persistent HTTP with Parallel Connections, using a simple example of retrieving a webpage with an HTML file and 5 image objects.

## Assumptions

- **RTT (Round Trip Time)**: 100ms
- **Transmission time for each object (HTML or image)**: 200ms

## 1. Non-Persistent HTTP (Without Parallel Connections)

In Non-Persistent HTTP, each object requires a separate TCP connection. For each object (HTML + 5 images), there will be 2 RTTs: one to establish the connection and one to send the request and receive the response.

### Steps for Non-Persistent HTTP (Without Parallel Connections)

**Request for HTML:**

- 1 RTT to establish the TCP connection.
- 1 RTT to request and receive the HTML.
- **Total time for HTML**: 2 RTT + Transmission time for HTML.

**Request for each image (5 images):**

- For each image, 2 RTTs are required (1 for connection and 1 for request/response).
- **Total time for 5 images**: 5 × (2 RTT + Transmission time per image).

**Total Time (Non-Persistent HTTP without Parallel Connections):**

- HTML: 2 RTT + 200ms (transmission) = 200ms + 200ms = 400ms.
- 5 images: 5 × (2 RTT + 200ms) = 5 × (200ms + 200ms) = 2000ms.
- **Total time**: 400ms + 2000ms = 2400ms.

## 2. Persistent HTTP (Without Pipelining)

In Persistent HTTP, one TCP connection is kept open for multiple requests. However, without pipelining, the client still needs to wait for the response of each object before sending the next request.

### Steps for Persistent HTTP (Without Pipelining)

**Initial Request for HTML:**

- 1 RTT to establish the connection.
- 1 RTT to send the request and receive the response.
- **Total time for HTML**: 2 RTT + Transmission time for HTML.

**Subsequent Requests for each image (5 images):**

- Each image is sent after the HTML response is received.
- For each image, 1 RTT is required for the request and response (no additional connection setup).
- **Total time for 5 images**: 5 × (1 RTT + Transmission time per image).

**Total Time (Persistent HTTP without Pipelining):**

- HTML: 2 RTT + 200ms = 200ms + 200ms = 400ms.
- 5 images: 5 × (1 RTT + 200ms) = 5 × (100ms + 200ms) = 1500ms.
- **Total time**: 400ms + 1500ms = 1900ms.

## 3. Persistent HTTP with Pipelining

In Persistent HTTP with Pipelining, the client can send all requests in one go without waiting for each response. This reduces RTT since requests are sent in parallel.

### Steps for Persistent HTTP with Pipelining

**First get HTML**:

- 1 RTT for TCP connection (100ms)
- 1 RTT for HTTP request/response (100ms)
- Transmission time for HTML (200ms)

Total for HTML = 400ms

**Then pipeline requests for all 5 images**:

- 1 RTT for sending all image requests and starting to receive responses (100ms)
- Transmission time for 5 images (5 × 200ms = 1000ms)

Total for pipelined images = 1100ms

Total time = 400ms + 1100ms = 1500ms

## 4. Non-Persistent HTTP with Parallel Connections

In Non-Persistent HTTP with Parallel Connections, the client opens multiple TCP connections to fetch multiple objects simultaneously. In this case, the transmission time is reduced because objects are retrieved concurrently.

### Steps for Non-Persistent HTTP with Parallel Connections

**Request for HTML and all 5 images:**

**First, the HTML request**:

First, you must get the HTML file (sequential/independent):

- 1 RTT for TCP (100ms)
- 1 RTT for HTTP request/response (100ms)
- Transmission time (200ms)

Total for HTML = 400ms

**After getting HTML, browser discovers the 5 images and can request them all in parallel**:

- All TCP connections happen over the same 1 RTT (100ms)
- All HTTP requests/responses happen over the same 1 RTT (100ms)
- All transmissions happen in parallel over the same 200ms period

Total for parallel phase = 400ms

**Total Time (Non-Persistent HTTP with Parallel Connections):** 800ms.

## Summary of Times

| Type of HTTP                                    | Total Time |
| ----------------------------------------------- | ---------- |
| Non-Persistent HTTP (without Parallel)          | 2400ms     |
| Persistent HTTP (without Pipelining)            | 1900ms     |
| Persistent HTTP with Pipelining                 | 1500ms     |
| Non-Persistent HTTP (with Parallel Connections) | 800ms      |

## Key Takeaways

- **Non-Persistent HTTP (without parallel connections)** has the highest total time because it opens a new connection for each object.
- **Persistent HTTP without pipelining** is faster than non-persistent, but it still waits for each object’s response before sending the next request.
- **Persistent HTTP with pipelining** greatly reduces the time by allowing multiple requests in one go, sending them without waiting for responses in between.
- **Non-Persistent HTTP with parallel connections** performs better than non-persistent without parallel connections because it fetches multiple objects simultaneously.

---

### Attacks

- **DoS**: Single source attack that aims to overload a server and disrupt its service.

- **DDoS**: A more powerful, distributed version of DoS that involves multiple devices attacking a server, making it much harder to mitigate.

CDNs have multiple servers across the globe, so when a DDoS attack occurs, the traffic gets distributed among all those servers instead of overwhelming a single server.

### What is CDN ?

Content Delivery Network (CDN) is a network of servers that are distributed across different geographical locations. The main goal of a CDN is to deliver content to users more efficiently and quickly by reducing the distance between the user and the server hosting the content.
