# React Native Authorize.net for Expo SDK v49

- Fetch token by sending card details to `AcceptSDK` for iOS and Android.

#### Android

Package is using auto-linking

#### iOS

Package is using autolinking with Cocoapods

```
pod install
```

## Request

#### Required arguments:

    LOGIN_ID : "login_id of authorize.net in which the card will be added."
    CLIENT_KEY : "client_key of authorize.net in which the card will be added."
    CARD_NO : "card no"
    EXPIRATION_MONTH : "expiration month of the card."
    EXPIRATION_YEAR : "expiration year of the card."
    CVV_NO : "cvc no of the card."

## Response

    DATA_DESCRIPTOR = "card data descriptor"
    DATA_VALUE = "card data value"

`please note: this will be used to add card on server using Accept.js from auhorize.net`

## Usage

```js
import RNAuthorizeNet from '/module/path'` 
```

```js

// note: object properties must be exactly like they are shown here
const isProduction = process.env.NODE_ENV === 'production'; // true | false
const cardValues = {
  LOGIN_ID: 'XXXX', // AUTH.NET LOGIN_ID
  CLIENT_KEY: 'XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX', // AUTH.NET PUBLIC/CLIENT KEY
  CARD_NO: '4111111111111111',
  CVV_NO: '000',
  EXPIRATION_MONTH: '11',
  EXPIRATION_YEAR: '23',
};

/**
 * Authorizes a credit card transaction using Authorize.Net AcceptJS Native Module
 *
 * @param {Object} cardValues - An object containing card info and auth.net credentials.
 * @param {boolean} isProduction - A flag indicating whether the production environment should be used.
 * @param {Function} callback - A callback function to handle the response.
 *                             It receives an object with properties: success, data, and error.
 * @returns {void}
 */

RNAuthorizeNet.getTokenWithRequestForCard(
  cardValues,
  isProduction,
  function (response: any) {
    const { success, data, error } = response;
    if (success) {
      console.log('Success:', data);
      // Access individual properties in data as needed
    } else {
      console.log('Error:', error);
      // Access error properties in error as needed
    }
  }
);
```

### Original Author

- [Peter Machowski](mailto:peter@reliantid.com)

### Contributor

- [Anthony Coffey](https://linktr.ee/coffeycodes)
