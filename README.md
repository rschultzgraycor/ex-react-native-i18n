# ex-react-native-i18n for ExponentJS
Integrates [I18n.js](https://github.com/fnando/i18n-js) with React Native and ***Exponent***. Uses the device's locale as default.
<br/>
<br/>

## Automatic setup
`$ npm install ex-react-native-i18n --save`

or

`$ yarn add ex-react-native-i18n`

## Usage
```javascript
import I18n from 'react-native-i18n'


class Demo extends React.Component {
  // Async call to init the locale
  async componentWillMount() {
    await I18n.initAsync();
  }
  render () {
    return (
      <Text>{I18n.t('greeting')}</Text>
    )
  }
}

// Enable fallbacks if you want `en-US` and `en-GB` to fallback to `en`
I18n.fallbacks = true

I18n.translations = {
  en: {
    greeting: 'Hi!'
  },
  fr: {
    greeting: 'Bonjour!'
  }
}
```

This will render `Hi!` for devices with the English locale, and `Bonjour!` for devices with the French locale.

### Fallbacks
When fallbacks are enabled (which is generally recommended), `i18n.js` will try to look up translations in the following order (for a device with `en_US` locale):
- en-US
- en

**Note**: iOS locales use underscored (`en_US`) but `i18n.js` locales are dasherized (`en-US`). This conversion is done automatically for you.
```js
I18n.fallbacks = true

I18n.translations = {
  'en': {
    greeting: 'Hi!'
  },
  'en-GB': {
    greeting: 'Hi from the UK!'
  }
}
```
For a device with a `en_GB` locale this will return `Hi from the UK!'`, for a device with a `en_US` locale it will return `Hi!`.

### Device's locale
You can get the device's locale with the `RNI18n` native module:
```js
import I18n from 'react-native-i18n'
const deviceLocale = I18n.locale
```

Returns `en-US`.


### I18n.js documentation
For more info about I18n.js methods (`localize`, `pluralize`, etc) and settings see [its documentation](https://github.com/fnando/i18n-js#setting-up).
