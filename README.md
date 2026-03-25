[![npm version](https://badge.fury.io/js/%40benschac%2Freact-native-awesome-gallery.svg)](https://badge.fury.io/js/%40benschac%2Freact-native-awesome-gallery)

## Support

If you love using React Native Awesome Gallery and would like to show your appreciation, you can support the project by buying me a coffee. Your support helps me keep the project alive and continuously improving. Every little bit counts!


<div style="text-align: center;">
  <h1 align="center">React Native Awesome Gallery</h1>
  <h3 align="center">Photos gallery powered by Reanimated v4 and react-native-gesture-handler</h3>
</div>

<table style='width:100%;'>
  <tr>
    <td><h4 align='center'>Basic usage</h4></td>
     <td><h4 align='center'>With toolbar</h4></td>
     <td><h4 align='center'>Loop</h4></td>
  </tr>
  <tr>
    <td><img width="100%" height="480" src="example-basic.gif" alt="Gallery basic usage"></td>
    <td><img width="100%" height="480" src="example-toolbar.gif" alt="Gallery with toolbar"></td>
    <td><img width="100%" height="480" src="example-loop.gif" alt="Gallery loop"></td>
  </tr>
 </table>

## Supported features

- Zoom to scale
- Double tap to scale
- Native iOS feeling (rubber effect, decay animation on pan gesture)
- RTL support
- Fully customizable
- Both orientations (portrait + landscape)
- Infinite list
- Supports both iOS and Android.

## Installation

> **_Note:_** This package targets Reanimated 4 and the React Native New Architecture.

First follow the installation instructions for
[React Native Reanimated](https://docs.swmansion.com/react-native-reanimated/)
and [react-native-gesture-handler](https://docs.swmansion.com/react-native-gesture-handler/).

Make sure your app also installs `react-native-worklets` and follows the
official
[Reanimated 4 installation guide](https://docs.swmansion.com/react-native-reanimated/docs/fundamentals/getting-started/).

```sh
yarn add @benschac/react-native-awesome-gallery
```

Expo SDK 55 is supported by the example app in this repository. More generally,
make sure your Expo SDK and React Native version are compatible with the official
[Reanimated 4 support matrix](https://docs.swmansion.com/react-native-reanimated/docs/guides/compatibility/)
and New Architecture requirements.

## Usage

Check out an [example folder](./example) for example with Expo Image

```js
import Gallery from '@benschac/react-native-awesome-gallery';

// ...

const images = ['https://image1', 'https://image2'];

return (
  <Gallery
    data={images}
    onIndexChange={(newIndex) => {
      console.log(newIndex);
    }}
  />
);
```

## Props

| Prop                             | Description                                                                                                                                                                     | Type                                                                                             | Default                                                                |
|----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| data                             | Array of items to render                                                                                                                                                        | `T[]`                                                                                            | `undefined`                                                            |
| renderItem?                      | Callback func which can be used to render custom image component, e.g `FastImage`. NOTE: You have to call `setImageDimensions({width, height})` parameter after image is loaded | `(renderItemInfo: {item: T, index: number, setImageDimensions: Function}) => React.ReactElement` | `undefined`                                                            |
| keyExtractor?                    | Callback func which provides unique keys for items                                                                                                                              | `(item: T, index: number) => string or number`                                                   | Takes `id` or `key` or `_id` from `Item`, otherwise puts `Item` as key |
| initialIndex?                    | The initial image index                                                                                                                                                         | `number`                                                                                         | `0`                                                                    |
| onIndexChange?                   | Is called when index of active item is changed                                                                                                                                  | `(newIndex: number) => void`                                                                     | `undefined`                                                            |
| numToRender?                     | Amount of items rendered in gallery simultaneously                                                                                                                              | `number`                                                                                         | `5`                                                                    |
| emptySpaceWidth?                 | Width of empty space between items                                                                                                                                              | `number`                                                                                         | `30`                                                                   |
| doubleTapScale?                  | Image scale when double tap is fired                                                                                                                                            | `number`                                                                                         | `3`                                                                    |
| doubleTapInterval?               | Time in milliseconds between single and double tap events                                                                                                                       | `number`                                                                                         | `500`                                                                  |
| maxScale?                        | Maximum scale user can set with gesture                                                                                                                                         | `number`                                                                                         | `6`                                                                    |
| pinchEnabled?                    | Is pinch gesture enabled                                                                                                                                                        | `boolean`                                                                                        | `true`                                                                 |
| swipeEnabled?                    | Is pan gesture enabled                                                                                                                                                          | `boolean`                                                                                        | `true`                                                                 |
| doubleTapEnabled?                | Is double tap enabled                                                                                                                                                           | `boolean`                                                                                        | `true`                                                                 |
| disableTransitionOnScaledImage?  | Disables transition to next/previous image when scale > 1                                                                                                                       | `boolean`                                                                                        | `false`                                                                |
| hideAdjacentImagesOnScaledImage? | Hides next and previous images when scale > 1                                                                                                                                   | `boolean`                                                                                        | `false`                                                                |
| disableVerticalSwipe?            | Disables vertical swipe when scale == 1                                                                                                                                         | `boolean`                                                                                        | `false`                                                                |
| disableSwipeUp?                  | Disables swipe up when scale == 1                                                                                                                                               | `boolean`                                                                                        | `false`                                                                |
| loop?                            | Allows user to swipe infinitely. Works when `data.length > 1`                                                                                                                   | `boolean`                                                                                        | `false`                                                                |
| onScaleChange?                   | Is called when scale is changed                                                                                                                                                 | `(scale: number) => void`                                                                        | `undefined`                                                            |
| onScaleChangeRange?              | Shows range of scale in which `onScaleChange` is called                                                                                                                         | `{start: number, end: number}`                                                                   | `undefined`                                                            |
| containerDimensions?             | Dimensions object for the View that wraps gallery.                                                                                                                              | `{width: number, height: number}`                                                                | value returned from `useWindowDimensions()` hook.                      |
| style?                           | Style of container                                                                                                                                                              | `ViewStyle`                                                                                      | `undefined`                                                            |

## Events

| Prop                                                             | Description                                                                                                                    | Type       |
|------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|------------|
| onSwipeToClose()                                                 | Fired when user swiped to top/bottom                                                                                           | `Function` |
| onTranslationYChange(translationY: number, shouldClose: boolean) | `'worklet';` Fired when user is swiping vertically to close the gallery                                                        | `Worklet`  |
| onTap()                                                          | Fired when user tap on image                                                                                                   | `Function` |
| onDoubleTap(toScale: number)                                     | Fired when user double tap on image                                                                                            | `Function` |
| onLongPress()                                                    | Fired when long press is detected                                                                                              | `Function` |
| onScaleStart(scale: number)                                      | Fired when pinch gesture starts                                                                                                | `Function` |
| onScaleEnd(scale: number)                                        | Fired when pinch gesture ends. Use case: add haptic feedback when user finished gesture with `scale > maxScale` or `scale < 1` | `Function` |
| onPanStart()                                                     | Fired when pan gesture starts                                                                                                  | `Function` |

## Methods

```js
import Gallery, { GalleryRef } from '@benschac/react-native-awesome-gallery';

// ...

const ref = useRef<GalleryRef>(null);
```

| Prop     | Description               | Type                                             |
|----------|---------------------------|--------------------------------------------------|
| setIndex | Sets active index         | `(newIndex: number, animated?: boolean) => void` |
| reset    | Resets scale, translation | `(animated?: boolean) => void`                   |

## License

MIT
