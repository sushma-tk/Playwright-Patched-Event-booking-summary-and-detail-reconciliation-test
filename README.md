# EventHub – Patched One Booking in Transit (Playwright)

This test intercepts the EventHub bookings API, changes **one** booking at runtime, and checks that the UI shows the patched values while all other bookings stay live.

## What the test does

1. Logs in and checks the **My Bookings** link is visible.
2. Intercepts the bookings **list** API and patches one booking (by id):
   - reference code
   - event title
   - ticket count
   - total amount
3. Opens **My Bookings** and finds the patched card **by its reference text** (not by position).
4. Checks the card shows the patched title, tickets, and total.
5. Checks another card still shows live (unchanged) data.
6. Intercepts the booking **detail** API for the same id and patches the same fields.
7. Opens **View Details** and checks:
   - URL uses the original booking id
   - reference, title, tickets, and total match the patched values
   - customer email is still the original live value
8. Goes back to **My Bookings** and finds the same card again by its patched reference.

## Tech

- Playwright (JavaScript)

## Setup

Update the test data at the top of the test file:

```js
const EMAIL = 'your-email@example.com';
const PASSWORD = 'your-password';
const targetBookingId = 12146; // a booking id from your account
```

> You need at least 2 bookings in your account for this test.

## Run

```bash
npx playwright test 
```

## App under test

https://eventhub.rahulshettyacademy.com