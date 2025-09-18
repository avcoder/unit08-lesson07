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
- [ ] Continue playing with expo APIs: Maps, StoreReview, etc.

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

# Exercise: Fetch JSON

- see https://thecatapi.com/ OR https://thedogapi.com/
- use useEffect to fetch JSON and display results

## Exercise 2

- attempt to refactor such that we fetch via [RTK Query](https://redux-toolkit.js.org/rtk-query/overview)

---
transition: slide-left
---

# Zustand
State Manager

- see https://zustand.docs.pmnd.rs/getting-started/introduction


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
transition: slide-left
---

# Leave a Review

- https://docs.expo.dev/versions/latest/sdk/storereview/

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

# SQLite

- see https://docs.expo.dev/versions/latest/sdk/sqlite/

---
transition: slide-left
---

# SMS

- see https://docs.expo.dev/versions/latest/sdk/sms/

---
transition: slide-left
---

# ImagePicker

- see https://docs.expo.dev/versions/latest/sdk/imagepicker/

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

# Homework

- Start working on your Mobile Assignment 
- Start working on your Capstone planning project
