---
cover: .gitbook/assets/cover.png
coverY: 0
---

# Flik Pay

## Step 1: Set up Flik Pay Component

The `flik-pay` component is available as part of `Monri.js`. To get started, include the following script on your page. This script **must be loaded directly from `monri.com`** to remain PCI-compliant —**you cannot self-host or bundle it**.

### Test Environment

```html
<script src="https://ipgtest.monri.com/dist/components.js"></script>
```

### Production Environment

```html
<script src="https://ipg.monri.com/dist/components.js"></script>
```

Then, create an instance of Monri and initialize components:

```js
const monri = Monri('<authenticity-token>');
const components = monri.components({clientSecret: '<client-secret>'});
```

Replace `<authenticity-token>` with the value from your merchant dashboard.

Replace `<client-secret>` with the value obtained when creating a payment via your backend.

⚠️ When switching to production, ensure you're using your production `authenticity_token` and `client_secret`.

## Step 2: Create your Payment Form Container

Create a DOM element where the flik-pay component will be injected.

```html
<div id="flik-pay-element"></div>
```

## Step 3: Initialize and Mount `flik-pay` Component

You can now create and mount the component. Optional styles can be passed depending on screen size:

```javascript
// Create an instance of the flik-pay Components.
const flikPay = components.create("flik-pay", {
    trx_token: "<trx_token>",
    environment: isTestSystem ? "test" : "prod",
    // define styling options for flik-pay Components
    style: {}
});
// Add an instance of the Flik Pay component into the `flik-pay-element` <div>.
flikPay.mount("flik-pay-element");
```

## Step 4: Optional - Listen to Payment Events

You can optionally listen to success or error events:

```js
flikPay.on('paymentSuccess', (result) => {
    console.log('Payment successful', result);
});

flikPay.on('paymentError', (error) => {
    console.error('Payment error', error);
});
```

| Option        | Description                                             |
| ------------- | ------------------------------------------------------- |
| `trx_token`   | Token received when creating the transaction on backend |
| `environment` | Either `'test'` or `'prod'`, depending on your system   |

## Notes

Ensure the container `#flik-pay-element` exists before calling mount.

Use media queries or window.innerWidth to adjust styles for mobile/desktop.

QR codes or bank options are rendered automatically inside the component.

Flik Pay supports real-time payments and is optimized for bank selection and QR scanning.
