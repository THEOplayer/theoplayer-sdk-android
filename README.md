# THEOplayerSDK

THEOplayer is the universal video player solution created by THEO Technologies. It enables you to quickly deliver content playback on Android, Android TV and Fire TV.

## Prerequisites

-   A valid THEOplayer license. Request yours via our [THEOportal](https://portal.theoplayer.com).

## Included features

THEOplayerSDK consists of modular features. This package includes only the basic features: DASH, HLS, LL-HLS and UI.
Additional feature sets will be provided in the future.

Alternatively, you can make your own custom build via our [THEOportal](https://portal.theoplayer.com).

## Installation

In your **project** level `build.gradle` file add the Jitpack repository:

```
allprojects {
    repositories {
        google()
        mavenCentral()
        maven { url 'https://jitpack.io' }
    }
}
```

In your **module** level `build.gradle` file add the THEOplayer dependency:

```
implementation 'com.theoplayer.theoplayer-sdk-android:basic-minapi16:+'
implementation 'com.theoplayer.theoplayer-sdk-android:basic-minapi21:+'
implementation 'com.theoplayer.theoplayer-sdk-android:basic-androidTV:+'
implementation 'com.theoplayer.theoplayer-sdk-android:basic-fireTV:+'
```
Notes:

* The `+` will fetch the latest released version of THEOplayer SDK.
* Android Studio will recommend replacing the `+` with the exact version of THEOplayer.
* Versions earlier than 2.83.0 (release 2021.1.3) are not available on the public Jitpack registry.
Earlier versions are available through our [THEOportal](https://portal.theoplayer.com).

## Usage

### 1. Instantiation

The UI element of THEOplayer is called `THEOplayerView` and it can be instantiated in 2 different ways:

#### Using the layout.xml

```xml
<com.theoplayer.android.api.THEOplayerView
    android:id="@+id/theoPlayerView"
    android:layout_width="match_parent"
    android:layout_height="400dp" />
```
And then in the Activity/Fragment reference to it using

```java
THEOplayerView theoPlayerView = findViewById(R.id.theoPlayerView);
```

#### Using the constructor API ####

In the Activity/Fragment

```java
THEOplayerConfig playerConfig = new THEOplayerConfig.Builder()
    .chromeless(false)
    .build();
THEOplayerView theoPlayerView = new THEOplayerView(this, playerConfig);
```

### 2. Calling lifecycle events

```java
@Override
protected void onPause() {
    super.onPause();
    theoPlayerView.onPause();
}

@Override
protected void onResume() {
    super.onResume();
    theoPlayerView.onResume();
}

@Override
protected void onDestroy() {
    super.onDestroy();
    theoPlayerView.onDestroy();
}
```

### 3. Using the player

```java
Player theoPlayer = theoPlayerView.getPlayer();
```

#### Creating and setting a source

```java
TypedSource typedSource = new TypedSource.Builder()
    .src(getString(R.string.defaultSourceUrl))
    .build();

SourceDescription sourceDescription = new SourceDescription.Builder()
    .sources(typedSource)
    .poster(getString(R.string.defaultPosterUrl))
    .build();

theoPlayer.setSource(sourceDescription.build());
```

### 4. Adding listeners to THEOplayer basic playback events.

```java
theoPlayer.addEventListener(PlayerEventTypes.PLAY, event -> Log.i(TAG, "Event: PLAY"));
theoPlayer.addEventListener(PlayerEventTypes.PLAYING, event -> Log.i(TAG, "Event: PLAYING"));
theoPlayer.addEventListener(PlayerEventTypes.PAUSE, event -> Log.i(TAG, "Event: PAUSE"));
theoPlayer.addEventListener(PlayerEventTypes.ENDED, event -> Log.i(TAG, "Event: ENDED"));
theoPlayer.addEventListener(PlayerEventTypes.ERROR, event -> Log.i(TAG, "Event: ERROR, error=" + event.getErrorObject().getMessage()));
```

That's it! You should now have a working player in your application.

## Documentation

The documentation for THEOplayer is located on our [documentation website](https://docs.theoplayer.com).
For an example on how to setup THEOplayer, take a look at our [Getting started guide](https://docs.theoplayer.com/getting-started/01-sdks/02-android/00-getting-started.md).

## Support

If you are having issues installing or using the package, first look for existing answers on our [documentation website](https://docs.theoplayer.com/),
and in particular our [FAQ](https://docs.theoplayer.com/faq/00-introduction.md).

You can also contact our technical support team by following the instructions on our [support page](https://docs.theoplayer.com/faq/00-introduction.md).
Note that your level of support depends on your selected [support plan](https://www.theoplayer.com/supportplans).

## License

The contents of this package are subject to the [THEOplayer license](https://www.theoplayer.com/terms).