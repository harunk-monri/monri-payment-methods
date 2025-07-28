# IPS - Instant Payments Serbia

## Step 1: Set up IPS-RS Component

The `ips-rs` component is available as part of `Monri.js`. To get started, include the following script on your page.
This script **must be loaded directly from `monri.com`** to remain PCI-compliant —**you cannot self-host or bundle it**.

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

Replace ```<authenticity-token>``` with the value from your merchant dashboard.

Replace ```<client-secret>``` with the value obtained when creating a payment via your backend.

⚠️ When switching to production, ensure you're using your production ```authenticity_token``` and ```client_secret```.

## Step 2: Create your Payment Form Container

Create a DOM element where the ips-rs component will be injected.

```html
<div id="ips-rs-element"></div>
```

## Step 3: Initialize and Mount `ips-rs` Component

You can now create and mount the component. Optional styles can be passed depending on screen size:

```javascript
const isMobile = window.innerWidth <= 768;

// Create an instance of the ips-rs Components.
const ips = components.create("ips-rs", {
    trx_token: "<trx_token>",
    environment: isTestSystem ? "test" : "prod",
    // define styling options for ips-rs Components
    style: {
        container: {
            width: "100%",
            display: 'flex',
            flexDirection: 'row',
            maxWidth: "600px",
            margin: "0 auto",
            alignItems: "center",
            justifyContent: "center",
            gap: '15px'
        },
        descriptionRow: {
            display: "flex",
            gap: "1rem",
            marginBottom: isMobile ? "0rem" : "4rem",
            justifyContent: "space-between"
        },
        text: {
            display: "none"
        },
        logo: {
            alignSelf: "flex-start",
            width: "35vw",
            maxWidth: "120px",
            marginBottom: "0rem"
        },
        qrCodeContainer: {
            display: "flex",
            justifyContent: "center",
            marginBottom: "0rem"
        },
        regenerateBtn: {
            backgroundColor: "#f8f8f8",
            fontSize: "1.2rem"
        },
        timer: {
            textAlign: "center",
            marginTop: "1rem",
            fontFamily: "Myriad Pro",
            color: "#9396A6",
            fontSize: "0.9rem"
        },
        ifMobile: {
            display: "block",
            marginBottom: "0rem"
        },
        radioLabel: {
            display: "inline-flex",
            alignItems: "center",
            marginRight: "1rem"
        },
        radioInput: {
            scale: 1.2,
            margin: "0 0.5rem 0 0",
            padding: 0
        },
        bankSelect: {
            backgroundColor: "#FCF5FF",
            color: "#8132A7",
            borderRadius: '10px',
            borderColor: 'transparent',
            fontWeight: '400',
            cursor: 'pointer',
            fontFamily: 'Myriad Pro'
        },
        generateQRButton: {
            backgroundColor: '#FCF5FF',
            color: '#8132A7',
            fontWeight: '400',
            borderRadius: '8px',
            borderColor: 'transparent',
            fontSize: '0.9rem',
            padding: '0.3rem 0.9rem',
            transition: '0.3s ease-in-out',
            fontFamily: 'Myriad Pro',
            maxWidth: '150px',
            margin: '0 auto',
            display: 'block'
        },
        button: {
            fontSize: '1rem'
        },
        rightContainer: {
            display: "flex",
            flexDirection: "row"
        }
    }
});
// Add an instance of the Ips-Rs component into the `ips-rs-element` <div>.
ips.mount("ips-rs-element");
```

## Step 4: Optional - Listen to Payment Events

You can optionally listen to success or error events:

```js
ips.on('paymentSuccess', (result) => {
    console.log('Payment successful', result);
});

ips.on('paymentError', (error) => {
    console.error('Payment error', error);
});
```

| Option        | Description                                                         |
|---------------|---------------------------------------------------------------------|
| `trx_token`   | Token received when creating the transaction on backend             |
| `environment` | Either `'test'` or `'prod'`, depending on your system               |
| `style`       | Optional custom styles for component containers (see example above) |

## Notes

Ensure the container `#ips-rs-element` exists before calling mount.

Use media queries or window.innerWidth to adjust styles for mobile/desktop.

QR codes or bank options are rendered automatically inside the component.

IPS-RS supports real-time payments and is optimized for bank selection and QR scanning.