<p align="center">
  <img width="600" height="200" width="400" src="https://payherestorage.blob.core.windows.net/payhere-resources/www/images/PayHere-Logo.png">
</p>


## Features

- Works in front end JS frameworks
- Making one time payments with Checkout API
- Making Recurrent payments with Recurring API (monthly, daily. annually)
- Get payments data of your Payhere account using Retrieval API
- Linking customers payment info with your app for making future payments at any time without customer intervention

## How to use

### Initialization

First initialize Payhere in the entry point of your Single Page App, by specifying the merchant ID and the account type as follows.

```js

// Sandbox 
Payhere.init("12xxxxx",AccountCategory.SANDBOX)

// Live
Payhere.init("12xxxxx",AccountCategory.LIVE)
```

### Checkout

```js

function onPayhereCheckoutError(errorMsg) {
  alert(errorMsg)
}
  
function checkout() {
  const customer = new Customer({
    first_name: "Demo",
    last_name: "User",
    phone: "+94771234567",
    email: "user@example.com",
    address: "No. 50, Highlevel Road",
    city: "Panadura",
    country: "Sri Lanka",
  })

  const checkoutData = new CheckoutParams({
    returnUrl: 'http://localhost:3000/return',
    cancelUrl: 'http://localhost:3000/cancel',
    notifyUrl: 'http://localhost:8080/notify',
    order_id: '112233',
    itemTitle: 'Demo Item',
    currency: CurrencyType.LKR,
    amount: 100
  })

  const checkout = new PayhereCheckout(customer,checkoutData,onPayhereCheckoutError)
  checkout.start()
}
```

### Subscription

```js

function onPayhereSubscriptionError(errorMsg) {
  alert(errorMsg)
}

function initSubscription() {
  try {
    const customer = new Customer({
      first_name: "Demo",
      last_name: "User",
      phone: "+94771234567",
      email: "user@example.com",
      address: "No. 50, Highlevel Road",
      city: "Panadura",
      country: "Sri Lanka",
    })

    const subscriptionData = new SubscriptionParams({
      returnUrl: 'http://localhost:3000/return',
      cancelUrl: 'http://localhost:3000/cancel',
      notifyUrl: 'http://localhost:8080/notify',
      order_id: '112234',
      itemTitle: 'Demo Item',
      recurrence: new Month(1),
      duration: new Month(12),
      currency: CurrencyType.LKR,
      amount: 100
    })
          
    const subscription = new PayhereSubscription(customer,subscriptionData,onPayhereSubscriptionError)
    subscription.start()
  } catch(err){
    console.log(err)
  }
}
```

### Preapproval

```js

function preApprove() {
  const customer = new Customer({
    first_name: "Demo",
    last_name: "User",
    phone: "+94771234567",
    email: "user@example.com",
    address: "No. 50, Highlevel Road",
    city: "Panadura",
    country: "Sri Lanka",
  })

  const preappParams = new PreapprovalParams({
    returnUrl: 'http://localhost:3000/return',
    cancelUrl: 'http://localhost:3000/cancel',
    notifyUrl: 'https://dfc84fd10430.ngrok.io/preapprove-notify',
    order_id: '112235',
    itemTitle: 'Demo Item',
    currency: CurrencyType.LKR
  })
  
  const preapp = new PayherePreapproval(customer,preappParams,(err) => alert(err))
  preapp.start()
}
```

