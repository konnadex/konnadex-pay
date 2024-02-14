# Konnadex Web SDK

Konnadex Pay is a software development kit that allows for ease of crypto payment integration on the web. Accept crypto USDT payments using Binanace smart chain (BSC), Ethereum and Polygon blockchain.

## Usage

Currently, anyone can use konnadex SDK via a simple hyperlink integration on a new or existing web page.

### Installing

Using CDN:

```js
<script src="https://cdn.jsdelivr.net/gh/konnadex/konnadex-pay@main/index.min.js"></script>
```

### Example

After the konnadex script has been loaded, a global `konnadexCheckout` object is injected into the global `window` object for ease of availability.

##### Creating an instance

```js
const pay = new KonnadexCheckout({
  key: "KDX_PUBK_TEST_9juOi233pYQUax0vB5wudw+H32SZttKUIyfZh/7xQZWiPbI1", // Use your konnadex key
  reference: String(Math.round(new Date()/1000)), // Use your actual payment reference code
  env: "DEVELOPMENT", // this supports "DEVELOPMENT" or "PRODUCTION"
  currency: "NGN",
  amount: "2000.42",
  theme: 'light',
  metadata: {
    email: "jd@doe.com",
    fullname: "John Doe",
    description:"",
    phone: ""
  },
  onSuccess: ()=>{},
  onError: ()=>{},
  onClose: ()=>{},
});
```

##### Setup event handlers and Open Konnadex Pay

Emit config data, prepare UI dialog for transactions and open the dialog

```js
pay.initializePay();
```

### Instance Configuration

konnadex is initialized with a configuration object which is required to setup and open up the konnadex dialog. See below for specifications on the configuration object.

```js
{
  key: "KDX_PUBK_TEST_9juOi233pYQUax0vB5wudw+H32SZttKUIyfZh/7xQZWiPbI1",
  reference: "test-test-ref",//unique
  metadata: {
    email: "jd@doe.com",
    fullname: "John Doe",
    description:"",
  },
  theme: 'light',
  env:"PRODUCTION",
  currency: "NGN",
  amount: "2000.42",

  // `onSuccess` callBack function on transaction successful
  onSuccess: function(transactionData){}, // no-default, optional, function

   // `onClose` callBack function on modal close
  onClose: function(closeEvent){}, // no-default, optional, function

   // `onError` callBack function on transaction successful
  onError: function(error){}, // no-default, optional, function
  // `transfer` Allow third party wallet transfers

  transfer: true, // default false, not required, boolean

}
```

### Supported Networks and token

| Network             | ChainId | USDT 
| ------------------- | ------- | ---- |
| Ethereum            | 1       |  ✅  |
| Binance Smart Chain | 56      |  ✅  |
| Polygon Mainnet     | 137     |  ✅  |
| Mumbai              | 80001   |  ✅  |
| BSC Testnet         | 97      |  ✅  |
| Goerli Testnet      | 5       |  ✅  |


### Full Example

Create an HTML file and paste this script below and get the bag.

```html
<!DOCTYPE html>
<meta name="viewport" content="width=device-width, initial-scale=1" />
<html>
  <head>
    <meta charset="utf-8" />
    <title>Getting Started</title>
    <script src="https://cdn.jsdelivr.net/gh/konnadex/konnadex-pay@main/index.min.js"></script>
  </head>

  <body>
    <div id="pay-widget-wrapper">
      Welcome to my website,pay for the item now.
      <button id="button">Pay Now</button>
    </div>
    <script>
      const pay = new KonnadexCheckout({
        key: "KDX_PUBK_TEST_9juOi233pYQUax0vB5wudw+H32SZttKUIyfZh/7xQZWiPbI1",
        reference: "test-test-ref",
         metadata: {
          email: "jd@doe.com",
          fullname: "John Doe",
          description:"",
        },
        theme: 'light',
        env: "PRODUCTION || DEVELOPMENT",
        currency: "NGN",
        amount: "2000.42",
        onSuccess: success,
        onError: error,
        onClose,
      });

      function success(data) {
        console.log(data);
      }

      function error(data) {
        console.log(data);
      }

      function onClose(data) {
        console.log(data);
      }
      const button = document.querySelector("#button");

      button.addEventListener("click", function () {
        pay.initializePay();
      });
    </script>
  </body>
</html>
```
