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

`note: these values will be used to add card on server using Accept.js from authorize.net`

## Usage

### Import

```js
import { NativeModules } from 'react-native';
const { RNAuthorizeNet } = NativeModules;
```

### Implementation

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
 * @returns {Promise} A promise that resolves with the payment token or rejects with an error
 */

RNAuthorizeNet.getTokenWithRequestForCard(cardValues, isProduction)
  .then(response => {
    console.log(response);
  })
  .catch((error: any) => {
    if (Platform.OS === 'ios') {
      const { code, message } = error;
      const alertMsg: string = `${message}\n\nError Code: ${code}`;
      Alert.alert('Error', alertMsg, [{ text: 'OK' }], {
        cancelable: false,
      });
    } else if (Platform.OS === 'android') {
      const { userInfo } = error;
      const { ERROR_TEXT, ERROR_CODE } = userInfo;
      const alertMsg: string = `${ERROR_TEXT}\n\nError Code: ${ERROR_CODE}`;
      Alert.alert('Error', alertMsg, [{ text: 'OK' }], {
        cancelable: false,
      });
    }
  });
```

`Note: The error handling is different on each platform`

The above implementation worked for me on both platforms. I hope this example code saves someone the countless hours it took me to promisify Peter's original code and get error handling working as expected.

### Original Author

- [Peter Machowski](mailto:peter@reliantid.com)

### Contributor

- [Anthony Coffey](https://linktr.ee/coffeycodes)
