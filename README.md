# GDPRMeteorit
GDPR Meteoritis a sample way to implement GDPR to you project

## Getting Started
### Step 1. Add the JitPack repository to your build file 
Add it in your root build.gradle at the end of repositories:

```
	allprojects {
		repositories {
			...
			maven { url 'https://www.jitpack.io' }
		}
	}
```
### Step 2. Add the dependency
 Add this tow lines to your Module dependency
```
dependencies {
		implementation 'com.github.ixiDev:Meteorit:v0.1'
		implementation 'com.google.android.ads.consent:consent-library:1.0.3'
	}
```

## How To use

```
        setContentView(R.layout.activity_main);
        ....
        new GDPRMeteorit()
                .withContext(this)
                .withPrivacyUrl("https://www.example.com/privacy") // your privacy url
                .withPublisherIds("pub-xxxxxxxxxxxxxxxx") // your admob account Publisher id 
                .withTestMode() // remove this on real project
                .check();
    ...
    
```
### How to Load Ads 
#### Banner ads

```
....

 AdRequest.Builder builder = new AdRequest.Builder()
                .addTestDevice(AdRequest.DEVICE_ID_EMULATOR);
        GDPRMeteorit.Request request = GDPRMeteorit.getRequest();
        if (request == GDPRMeteorit.Request.NON_PERSONALIZED) {
            // load non Personalized ads
            Bundle extras = new Bundle();
            extras.putString("npa", "1");
            builder.addNetworkExtrasBundle(AdMobAdapter.class, extras);
        } // else do nothing , it will load PERSONALIZED ads
        adView.loadAd(builder.build());
	
.....
	
```
#### Interstitail ads

```
      interstitialAd.setAdUnitId("ca-app-pub-3940256099942544/1033173712");
        AdRequest.Builder builder = new AdRequest.Builder()
                .addTestDevice(AdRequest.DEVICE_ID_EMULATOR);
        GDPRMeteorit.Request request = GDPRMeteorit.getRequest();
        if (request == GDPRMeteorit.Request.NON_PERSONALIZED) {
            // load non Personalized ads
            Bundle extras = new Bundle();
            extras.putString("npa", "1");
            builder.addNetworkExtrasBundle(AdMobAdapter.class, extras);
        }
        interstitialAd.loadAd(builder.build());
        interstitialAd.show();

```
