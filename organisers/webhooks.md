# Webhooks

Our platform exposes **webhooks** that registration platforms can subscribe to for real-time updates. This lets you process participants, orders, and line items as they happen and keep your system in sync.

---

## Available events

Currently, the following events are available:

- `order.received`  
  Triggered when a new order is placed. Contains order-level, line item and participant information.  

- `lineitem.received`  
  Triggered for each line item when an order is placed. Contains line item and participant information.   

- `participant.created`  
  Triggered for each particpant when an order is placed. Contains only participant information.

> 🗒️ A line item always represents a single event, line items for team races will contain multiple participants where applicable.
> ⚡️ More event types (e.g. cancellations, transfers, refunds) will be added in the future.

---

## Setup, delivery & security

We use **Svix** to handle delivery, verification and retries. Svix provides signature headers for verification and management/reporting tools.

Setup is managed entirely through the organiser dashboard.

### 1. Log in
Log into your organiser account at [findarace.com](https://findarace.com).  
From the top-right menu, select your organiser profile.

### 2. Go to Settings
In the sidebar, click **Settings**.  
Scroll down to the **Webhooks** section and click **Manage**.

### 3. Enable webhooks
If webhooks are disabled, click **Enable** to switch them on.

### 4. Create a webhook
Click **Create your first webhook**.  
This opens the Svix dashboard (our webhook provider).

### 5. Add an endpoint
In the Svix dashboard:
- Click **Add Endpoint**  
- Enter the URL of your endpoint (where you want events delivered)  
- Save

### 6. Subscribe to events
From the **Event Catalog** in Svix, choose the events you want to receive:  
- `order.received`  
- `lineitem.received`  
- `participant.created`  

### 7. Done
Your endpoint will now begin receiving webhooks for the selected events.

---

## Event payloads

### `order.received`

```json
{
  "id": 123456,
  "number": "11aa11aa11aa11aa11aa11aa11aa11aa",
  "shortNumber": "11aa11aa",
  "dateOrdered": "2022-07-10 00:18:59",
  "email": "email@test.com",
  "billingAddress": {
    "title": "",
    "firstName": "Frist",
    "lastName": "Last",
    "address1": "1 Street Name",
    "address2": "",
    "address3": "",
    "city": "City",
    "county": "",
    "postCode": "XX1 1XX",
    "country": "United Kingdom",
    "phone": "",
    "alternativePhone": ""
  },
  "subtotal": 50,
  "tax": 8.34,
  "total": 50,
  "lineItems": [
    {
      "id": 123456,
      "description": "Super Cool Race - Half Marathon",
      "qty": 1,
      "subtotal": 25,
      "tax": 4.17,
      "total": 25,
      "distribution": {
        "bookingFee": 0,
        "commission": 3.00,
        "findarace": {
          "bookingFee": 0,
          "commission": 2.00,
          "total": 2.00
        },
        "platform": {
          "commission": 1.00,
          "total": 1.00
        },
        "organiser": 22.00
      },
      "participants": [
        {
          "id": 123456,
          "name": "First Last",
          "firstName": "First",
          "lastName": "Last",
          "email": "email@test.com",
          "phone": "00000 000000",
          "address1": "1 Street Name",
          "city": "City",
          "postCode": "XX1 1XX",
          "country": "United Kingdom",
          "dob": "03/06/1989",
          "gender": "Female",
          "team": false,
          "fields": {
            "wouldYouLikeToPurchaseATShirt": {
              "label": "Would you like to purchase a Unisex T-Shirt?",
              "value": "noThanks",
              "displayValue": "No Thanks"
            }
          },
          "waivers": [
            {
              "id": 123456,
              "name": "Global Terms & Conditions",
              "dateAccepted": "2022-07-10 00:15:17"
            }
          ]
        }
      ]
    }
  ]
}
```

---

### `lineitem.received`

```json
{
  "id": 123456,
  "description": "Super Cool Race - Half Marathon",
  "qty": 1,
  "subtotal": 25,
  "tax": 4.17,
  "total": 25,
  "distribution": {
    "bookingFee": 0,
    "commission": 3.00,
    "findarace": {
      "bookingFee": 0,
      "commission": 2.00,
      "total": 2.00
    },
    "platform": {
      "commission": 1.00,
      "total": 1.00
    },
    "organiser": 22.00
  },
  "participants": [
    {
      "id": 123456,
      "name": "First Last",
      "firstName": "First",
      "lastName": "Last",
      "email": "email@test.com",
      "phone": "00000 000000",
      "address1": "1 Street Name",
      "city": "City",
      "postCode": "XX1 1XX",
      "country": "United Kingdom",
      "dob": "03/06/1989",
      "gender": "Female",
      "team": false,
      "fields": {
        "wouldYouLikeToPurchaseATShirt": {
          "label": "Would you like to purchase a Unisex T-Shirt?",
          "value": "noThanks",
          "displayValue": "No Thanks"
        }
      },
      "waivers": [
        {
          "id": 123456,
          "name": "Global Terms & Conditions",
          "dateAccepted": "2022-07-10 00:15:17"
        }
      ]
    }
  ],
  "product": {
    "id": 123456,
    "type": "edition",
    "name": "Super Cool Race",
    "url": "https://findarace.test/events/super-cool-race"
  },
  "purchasable": {
    "id": 123456,
    "type": "race",
    "name": "Half Marathon",
    "sku": "SKU-123456",
    "price": "25.0000"
  }
}
```

---

### `participant.created`

```json
{
  "id": 123456,
  "name": "First Last",
  "firstName": "First",
  "lastName": "Last",
  "email": "email@test.com",
  "phone": "00000 000000",
  "address1": "1 Street Name",
  "city": "City",
  "postCode": "XX1 1XX",
  "country": "United Kingdom",
  "dob": "03/06/1989",
  "gender": "Female",
  "team": false,
  "fields": {
    "wouldYouLikeToPurchaseATShirt": {
      "label": "Would you like to purchase a Unisex T-Shirt?",
      "value": "noThanks",
      "displayValue": "No Thanks"
    }
  },
  "waivers": [
    {
      "id": 123456,
      "name": "Global Terms & Conditions",
      "dateAccepted": "2022-07-10 00:15:17"
    }
  ]
}
```

---

Brought to you by [findarace.com](https://findarace.com) | &copy; Find a Race
Because doing sh*t makes you happy :) 
- Refunds  

