# 🔐 Platform Webhook Guide

Our platform webhooks lets you notify **findarace.com** about important events. This document explains how/ where to send requests, what to expect in the response, the supported event types, how to sign payloads, and how to extend the integration if needed.

---

## 📡 Endpoint

All webhook requests must be sent as an **HTTP POST** request to:

```
https://findarace.com/hooks/platform/<partner>
```

Where `<partner>` is your platform handle (we will provide this when setting you up).

### Request requirements

- **Method:** `POST`  
- **Content-Type:** `application/json`  
- **Body:** Raw JSON payload (UTF-8 encoded)  
- **Headers:**  
  - `X-Webhook-Timestamp` → Unix timestamp in seconds  
  - `X-Webhook-Signature` → HMAC signature (see [Signing Requests](#-signing-requests))  

### Body requirements

- The **`type`** property is **required**.  
- The `data` property may contain additional fields depending on the webhook type.  
- Example minimal body:  

```json
{
  "type": "event.updated"
}
```

We will reject requests that are not `POST`, not JSON, missing headers, or missing the `type` property.


## 📥 Responses

Our webhook endpoint always responds with JSON.

---

### ✅ Successful requests

- **HTTP status:** `200 OK`  
- **Body:**
```json
{
  "ok": true,
  "message": "optional descriptive message"
}
```

The `message` field is optional and may be included to provide additional context.

---

### ❌ Failed requests

- **HTTP status:** appropriate error code (`400`, `403`, `404`, `500`, etc.)  
- **Body:**
```json
{
  "ok": false,
  "error": "optional error message",
  "errors": ["optional", "array", "of", "errors"]
}
```

- `error` is an optional single descriptive string.  
- `errors` is an optional array of error details when multiple issues are detected.  

---

### Example error responses

**Invalid signature:**
```http
HTTP/1.1 403 Forbidden
Content-Type: application/json
```
```json
{
  "ok": false,
  "error": "Invalid signature"
}
```

**Missing required field:**
```http
HTTP/1.1 400 Bad Request
Content-Type: application/json
```
```json
{
  "ok": false,
  "error": "Missing required property: type",
  "errors": ["'type' field is required"]
}
```


---

## 🎟 Supported Webhook Types

Currently we support the following webhook event types for all platforms.

### `event.updated`

Trigger when an existing (already authorised) event is updated.

**Payload:**
```json
{
  "type": "event.updated",
  "data": {
    "id": 123456
  }
}
```

---

### `event.authorized`

Trigger when an event has been created / authorised by an organiser.

**Payload:**
```json
{
  "type": "event.authorized",
  "data": {
    "id": 123,
    "name": "Some Event",
    "organiser": {
      "id": 456,
      "name": "Some RD",
      "contact": "Contact Name",
      "email": "some@rd.com",
      "phone": "01234 456789"
    }
  }
}
```

---

### `organiser.authorized`

Trigger when an organiser is authorised.

**Payload:**
```json
{
  "type": "organiser.authorized",
  "data": {
    "id": 456,
    "name": "Some RD",
    "contact": "Contact Name",
    "email": "some@rd.com",
    "phone": "01234 456789"
  }
}
```

---

### 🔧 Custom Event Types

We can also handle **platform-specific event types** if your system needs to send additional notifications.  
Simply provide the `type` and payload format, and we will extend our processing to handle it.

---

## 🔐 Signing Requests

To ensure webhook requests are authentic and have not been tampered with, each request must be signed with a shared secret.

### 🚀 Quick Start

1. Compute:
   ```
   signature = HMAC_SHA256(secret, "<timestamp>.<rawBody>")
   ```

   - `<timestamp>` = current Unix time in **seconds**  
   - `<rawBody>` = the exact JSON string you send in the request body  

2. Send these headers:
   ```
   X-Webhook-Timestamp: <timestamp>
   X-Webhook-Signature: <signature>
   ```

3. Send your raw JSON payload as the body.

---

### 1) Headers

- **`X-Webhook-Timestamp`**  
  The current Unix timestamp (number of seconds since 1970-01-01).

- **`X-Webhook-Signature`**  
  Lowercase **hex** HMAC-SHA256 of:
  ```
  <timestamp>.<rawBody>
  ```
  using the shared secret (`WEBHOOK_SECRET`).

---

### 2) Example Payload + Headers

**Body:**
```json
{"type":"event.updated","data":{"id":123456}}
```

**Generated headers:**
```
X-Webhook-Timestamp: 1724150400
X-Webhook-Signature: 5f0a9a6e9c6b4e1a...   (HMAC hex string)
```

---

### 3) Example Code

#### PHP
```php
$secret = $_ENV['WEBHOOK_SECRET'];
$body   = json_encode(['type' => 'event.updated', 'data' => ['id' => 123456]]);
$ts     = time();

$message   = $ts . '.' . $body;
$signature = hash_hmac('sha256', $message, $secret);

// Send headers:
//   X-Webhook-Timestamp: $ts
//   X-Webhook-Signature: $signature
// Body: $body
```

#### Node (JavaScript / TypeScript)
```js
import crypto from 'node:crypto';

const secret = process.env.WEBHOOK_SECRET;
const body = JSON.stringify({ type: 'event.updated', data: { id: 123456 } });
const ts = Math.floor(Date.now() / 1000);

const message = `${ts}.${body}`;
const sig = crypto.createHmac('sha256', secret).update(message).digest('hex');

// Send:
//   X-Webhook-Timestamp: ts
//   X-Webhook-Signature: sig
// Body: body
```

#### Python
```python
import time, hmac, hashlib, json, os

secret = os.getenv("WEBHOOK_SECRET").encode()
body = json.dumps({"type": "event.updated", "data": {"id": 123456}})
ts = str(int(time.time()))

message = f"{ts}.{body}".encode()
sig = hmac.new(secret, message, hashlib.sha256).hexdigest()

# Send:
#   X-Webhook-Timestamp: ts
#   X-Webhook-Signature: sig
# Body: body
```

---

## 🔧 Alternative Signing Methods

If your platform already uses a specific webhook signing scheme (e.g. Stripe-style, JWT-based), we can support **alternative methods** on a per-partner basis. Please let us know your preferred method, and we’ll ensure our system verifies requests accordingly.

---

## ⚠️ Important Notes

- Use the **exact raw body** you send — do not pretty-print or reformat JSON.  
- Timestamps must be in **seconds**, not milliseconds.  
- Our system only accepts requests where the timestamp is within **±5 minutes** of receipt.  
- Keep your secret safe — treat it like a password.

#
For support, if you have any questions or if you just want to chat please do get in touch at [support@findarace.com](mailto:support@findarace.com).

Brought to you by [findarace.com](https://findarace.com) | &copy; Find a Race
Because doing sh*t makes you happy :)
