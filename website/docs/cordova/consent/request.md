---
title: Request User Consent
sidebar_label: Request Consent
slug: /cordova/consent
---

## Installation

```shell
cordova plugin add cordova-plugin-consent
```

## Usage

```js
document.addEventListener('deviceready', async () => {
  if (cordova.platformId === 'ios') {
    const status = await consent.trackingAuthorizationStatus()
    /*
      trackingAuthorizationStatus:
      0 = notDetermined
      1 = restricted
      2 = denied
      3 = authorized
    */
    const statusNew = await consent.requestTrackingAuthorization()
  }

  const consentStatus = await consent.getConsentStatus()
  if (consentStatus === consent.ConsentStatus.Required) {
    await consent.requestInfoUpdate()
  }

  const formStatus = await consent.getFormStatus()
  if (formStatus === consent.FormStatus.Available) {
      const form = await consent.loadForm()
      form.show()
  }
}, false)
```

## Forward consent

If a user has consented to receive only non-personalized ads, pass `npa="1"` when creating the ad, e.g.

```js {3}
new admob.BannerAd({
  adUnitId: 'ca-app-pub-xxx/yyy',
  npa: '1',
})
```

The `npa` parameter is applicable to [`BannerAd`](./api/classes/bannerad), [`InterstitialAd`](./api/classes/interstitialad), [`RewardedAd`](./api/classes/rewardedad), [`RewardedInterstitialAd`](./api/classes/rewardedinterstitialad).

## References

- [TrackingAuthorizationStatus](./api/enums/trackingauthorizationstatus.md)
- [UMP SDK for Android](https://developers.google.com/admob/ump/android/quick-start)
- [UMP SDK for iOS](https://developers.google.com/admob/ump/ios/quick-start)
- [AppTrackingTransparency Framework](https://developer.apple.com/documentation/apptrackingtransparency)
