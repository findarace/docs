# 🔐 Platform Webhook Guide

Our webhook system lets your platform notify **findarace.com** about important events. This document explains where to send requests, the supported event types, how to sign payloads, and how to extend the integration if needed.

---

## 📡 Endpoint

Send all webhook requests to:

```
https://findarace.com/hooks/platform/<partner>
```

Where `<partner>` is your platform handle (avaiable in your dashboard).

---

## 🎟 Supported Webhook Types

Currently we support the following webhook event types for all platforms.

### `event.updated`

Triggered when an event is updated.

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

Triggered when an event has been authorised by an organiser.

**Payload:**
```json
{
  "type": "event.authorized",
  "data": {
    "id": 123,
    "organiser": {
      "id": 456,
      "name": "Some RD",
      "email": "some@rd.com",
      "phone": "01234 456789"
    }
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
