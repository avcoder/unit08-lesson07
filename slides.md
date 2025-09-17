---
# You can also start simply with 'default'
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: /assets/intro.jpg
# some information about your slides (markdown enabled)
title: Software Development | Foundations
info: |
  ## Software Development | Foundations
# apply unocss classes to the current slide
class: text-left
drawings:
  persist: false
transition: slide-left
mdc: true
---

# React Native
Mobile Development: Unit 08 - Lesson 07

- [ ] Fetch JSON via: useEffect, RTK Query
- [ ] Zustand
- [ ] Continue playing with expo APIs: Maps, 

<div class="abs-br m-6 text-xl">
  <a href="https://github.com/slidevjs/slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

<!--
-->

---
transition: slide-left
---

# Recap

- lab tmrw
- fyi: next week Tues
1. To deploy to stores, Get a developer account:
   - Apple: $99 per year
   - Google: one time fee $25
   - business account: must provide proof
   - individual account: if you charge for your app, your personal address will be made public
- Recommendation: if you charge for your app (or even in-app purchases) use business account so you can use a PO box for your address
- Difference: Must pay $25 to Google when ready to deploy to stores vs Must pay $99 to Apple just to generate certificates to run on physical device
2. Deploy to App Store either via: Xcode, Transporter app, `eas submit` > creates app on App Store Connect
  - and/or Upload to Google Play Console, along with screenshots

---
transition: slide-left
---

# Splash screen

- Once you are using a developing build and not Expo Go, you can now customize the splash screen and app icon.  All we need to do is configure the updated assets in app.json, prebuild, rebuild.
- Can create app icon via tools like Figma etc. but need to be a specific size
  - see https://www.figma.com/community/file/1155362909441341285/expo-app-icon-splash
- Splash screen must be `1284 x 2778` which will be displayed when app first launches
  - Replace existing `assets/splash.png` with your new Figma one
- App icon in iOS: `1024 x 1024` png, no transparency
  - Replace `assets/icon.png`
- App icon in Android `1024 x 1024` png, should have either transparency or solid background
  - Replace `assets/adaptive-icon.png`
- Update app name in package.json under expo > name
- Prebuild via `npx expo prebuild --platform ios --clean` (or replace ios with android)
- Rebuild with `npx expo run:ios` (or replace ios with android)

---
transition: slide-left
---

# Install a UI framework for React-Native

- Create a new React-Native project `npx create-expo-app helloworld`
- Installing either:
   - https://reactnativepaper.com/
   - https://reactnativeelements.com/
   
---
transition: slide-left
---

# Video Recording
Record and play videos  

- `npx expo install expo-video`
- see https://docs.expo.dev/versions/latest/sdk/video/

```tsx
import { useEvent } from 'expo';
import { useVideoPlayer, VideoView } from 'expo-video';

const videoSource =
  'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4';

export default function VideoScreen() {
  const player = useVideoPlayer(videoSource, player => {
    player.loop = true;
    player.play();
  });

  const { isPlaying } = useEvent(player, 'playingChange', { isPlaying: player.playing });
...
<VideoView style={styles.video} player={player} allowsFullscreen allowsPictureInPicture />
   ...
   onPress={() => { isPlaying ? player.pause() : player.play() }}
```


---
transition: slide-left
---

# Media Library Access

- `npx expo install expo-media-library`
- see https://docs.expo.dev/versions/latest/sdk/media-library/
```tsx
import * as MediaLibrary from 'expo-media-library';

export default function App() {
   const [permissionResponse, requestPermission] = MediaLibrary.usePermissions();
...
  async function getAlbums() {
    if (permissionResponse.status !== 'granted') {
      await requestPermission();
    }
    const fetchedAlbums = await MediaLibrary.getAlbumsAsync({
      includeSmartAlbums: true,
    });
    setAlbums(fetchedAlbums);
  }
```

---
transition: slide-left
---

# Speech Recognition & Text-to-Speech

- `npx expo install expo-speech`
- see https://docs.expo.dev/versions/v52.0.0/sdk/speech/

```tsx
import * as Speech from 'expo-speech';

export default function App() {
  const speak = () => {
    const thingToSay = '1';
    Speech.speak(thingToSay);
  };

  return (
    <View style={styles.container}>
      <Button title="Press to hear some words" onPress={speak} />
    </View>
  );
}
```

---
transition: slide-left
---

# Sensors 

- `npx expo install expo-sensors`
- See [docs](https://docs.expo.dev/versions/latest/sdk/sensors/) for available sensors:
   - Accelerometer
   - Barometer
   - Device Motion
   - Gyroscope
   - Magnetometer

---
transition: slide-left
---

# Geolocation

- `npx expo install expo-location`
- see https://docs.expo.dev/versions/latest/sdk/location/

```tsx
import * as Location from 'expo-location';

export default function App() {
  const [location, setLocation] = useState<Location.LocationObject | null>(null);

  useEffect(() => {
    async function getCurrentLocation() {
      
      let { status } = await Location.requestForegroundPermissionsAsync();
      if (status !== 'granted') {
        setErrorMsg('Permission to access location was denied');
        return;
      }

      let location = await Location.getCurrentPositionAsync({});
      setLocation(location);
    }

    getCurrentLocation();
  }, []);
```
---
transition: slide-left
---

# Network Info
Provides access to the device's network such as its IP address, MAC address, and airplane mode status

- `npx expo install expo-network`
- see https://docs.expo.dev/versions/v52.0.0/sdk/network/

## NetInfo
allows you to get information about connection type and connection quality.

- `npx expo install @react-native-community/netinfo`
- see https://docs.expo.dev/versions/v52.0.0/sdk/netinfo/

---
transition: slide-left
---

# Maps

- `npx expo install react-native-maps`
- see https://docs.expo.dev/versions/latest/sdk/map-view/
```tsx
import MapView from 'react-native-maps';

export default function App() {
  return (
    <View style={styles.container}>
      <MapView style={styles.map} />
    </View>
  );
}
```

- [Register](https://console.developers.google.com/apis) a Google Cloud API project and enable the Maps SDK


---
transition: slide-left
---

# 3rd party packages

- [react-native-game-engine](https://www.npmjs.com/package/react-native-game-engine)
   - Gives you a basic game engine to build simple 2D games.
   - Create a Flappy Bird or Pong clone
- [react-native-vision-camera](https://www.npmjs.com/package/react-native-vision-camera)
   - Access the device camera with superpowers (faster, more extensible).
   - Make a fun camera filter app like Snapchat lenses
- [react-native-gesture-handler](react-native-gesture-handler)
   - Adds gesture capabilities like swipe, pinch, drag.
- [flash-list](https://www.npmjs.com/package/@shopify/flash-list)
   - high-performance lists (superior to FlatList for large data)
- [lottie-react-native](https://www.npmjs.com/package/lottie-react-native)
   - parses Adobe After Effects animations exported as JSON and renders them natively

---
transition: slide-left
---

# Confetti
react-native-confetti-cannon

- `npx expo install react-native-confetti-cannon`
- https://www.npmjs.com/package/react-native-confetti-cannon

```tsx
import { ... Dimensions } from "react-native";
import { ... useRef } from "react";
import ConfettiCannon from "react-native-confetti-cannon";

export default function CounterScreen() {
   const confettiRef = useRef<any>();
...
confettiRef?.current?.start(); // run this perhaps in an onPress handler somewhere
...
<ConfettiCannon
  ref={confettiRef}
  count={50}
  origin={{ x: Dimensions.get("window").width / 2, y: -30 }}
  autoStart={false}
  fadeOut={true}
/>
```



---
layout: image-right
transition: slide-left
image: /assets/dan.png
backgroundSize: 444px 300px
class: text-left
---

# 10 minute break

🍦 Cool Tips, Trends and Resources:
- 🪏 [Why we ditched Next.js](https://northflank.com/blog/why-we-ditched-next-js-and-never-looked-back)
- ⚡ [content-visibility: auto](https://cekrem.github.io/posts/content-visibility-auto-performance/)
- 🎭 [React for Two Computers](https://www.youtube.com/watch?v=ozI4V_29fj4)
- ⚛️ [JSX Over the Wire = RSC](https://overreacted.io/jsx-over-the-wire/)
- 🍎 [new MAC setup](https://www.swyx.io/new-mac-setup)


<br>
<hr>
<br>

- 🧪 [Enter anonymous lab questions](https://docs.google.com/forms/d/e/1FAIpQLSevvGARdHQikso-uLqFCO481MABKE5HofuSrlzEPMNQ2ZLykw/viewform?usp=dialog)
- ℹ️ [Course feedback survey](https://circuitstream.typeform.com/to/ZoyYk7px#course_id=SoftwareAN&instructor=9514)


---
transition: slide-left
---

# Guest Speaker: Dion Tu

- When Dion arrives around 8:15pm EST, please turn on your cameras
- check out his work experience: https://www.linkedin.com/in/diontu/
- He has graciously given us 20 to 30 minutes of Q&A
- Ask him anything 



---
transition: slide-left
---

# Homework

- Start working on your Mobile Assignment 
- Start working on your Capstone planning project

---
transition: slide-left
---

# Lab
Create one of the following as a react-native mobile app or choose your own idea

- Maze Game: Use accelerometer to move a ball around a maze
- Compass app: Use magnetometer to show real-time compass direction
- Step Counter: Approximate steps based on accelerometer spikes
- Build a voice memo app
- Make a "soundboard" for sound effects or Build a record & playback feature
- Create a photo booth
- OR do at least 1 "Getting Started" from [this list](https://unit06-lesson06.netlify.app/14) or [here](https://unit04-lesson05.netlify.app/16)
