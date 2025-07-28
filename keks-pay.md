---
cover: .gitbook/assets/cover.png
coverY: 0
---

# Keks Pay

## Step 1: Set up Keks Pay Component

The `keks-pay` component is available as part of `Monri.js`. To get started, include the following script on your page. This script **must be loaded directly from `monri.com`** to remain PCI-compliant —**you cannot self-host or bundle it**.

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

Create a DOM element where the keks-pay component will be injected.

```html
<div id="keks-pay-element"></div>
```

## Step 3: Initialize and Mount `keks-pay` Component

You can now create and mount the component. Optional styles can be passed depending on screen size:

```javascript
// Create an instance of the keks-pay Components.
const keksPay = components.create("keks-pay", {
    trx_token: "<trx_token>",
    environment: isTestSystem ? "test" : "prod",
    // define styling options for keks-pay Components
    style: {}
});
// Add an instance of the Keks Pay component into the `keks-pay-element` <div>.
keksPay.mount("keks-pay-element");
```

## Step 4: Optional - Listen to Payment Events

You can optionally listen to success or error events:

```js
keksPay.on('paymentSuccess', (result) => {
    console.log('Payment successful', result);
});

keksPay.on('paymentError', (error) => {
    console.error('Payment error', error);
});
```

| Option        | Description                                             |
| ------------- | ------------------------------------------------------- |
| `trx_token`   | Token received when creating the transaction on backend |
| `environment` | Either `'test'` or `'prod'`, depending on your system   |

## Notes

Ensure the container `#keks-pay-element` exists before calling mount.

Use media queries or window.innerWidth to adjust styles for mobile/desktop.

QR codes or bank options are rendered automatically inside the component.

Keks Pay supports real-time payments and is optimized for bank selection and QR scanning.
