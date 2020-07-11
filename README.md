# react-native-image-colors

![Platform](https://img.shields.io/badge/platform-ios%20%7C%20android-green)
![TypeScript](https://img.shields.io/badge/typescript-typed-blue)
[![NPM Badge](https://img.shields.io/npm/v/react-native-image-colors)](https://www.npmjs.com/package/react-native-image-colors)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-%23ff69b4)

Fetch prominent colors from an image.

<p align="center" >
  <img
    width="250px"
    src="https://github.com/osamaq/react-native-image-colors/raw/master/assets/example1.png"
    alt="Example 1"
  />
  <img
    width="250px"
    src="https://github.com/osamaq/react-native-image-colors/raw/master/assets/demo1.png"
    alt="Demo 1 Android"
  />
  <img
    width="250px"
    src="https://github.com/osamaq/react-native-image-colors/raw/master/assets/demo1_ios.png"
    alt="Demo 1 iOS"
  />
  <img
    width="250px"
    src="https://github.com/osamaq/react-native-image-colors/raw/master/assets/demo2.png"
    alt="Demo 2 Android"
  />
  <img
    width="250px"
    src="https://github.com/osamaq/react-native-image-colors/raw/master/assets/demo2_ios.png"
    alt="Demo 2 iOS"
  />
</p>

This module is a wrapper around the [Palette](https://developer.android.com/reference/androidx/palette/graphics/Palette) class on Android and [UIImageColors](https://github.com/jathu/UIImageColors) on iOS.

## Installation

```
$ npm install react-native-image-colors
```

or

```
$ yarn add react-native-image-colors
```

### Android

Rebuild the app.

### iOS

Install the pod, then rebuild the app.

`npx pod-install`

(**Important for RN < 0.62 users**: if you face a compilation error while building, your Xcode project likely does not support Swift which this package requires. You can fix this by either **a)** Creating a blank dummy swift file using Xcode or **b)** [Following steps 1,2,3 here](https://github.com/facebook/flipper/blob/4297b3061f14ceca4d184aa3eebd0731b5bf20f5/docs/getting-started.md#for-pure-objective-c-projects).

## Usage

Start by importing the module

```js
import ImageColors from "react-native-image-colors"
```

🎨 Fetch colors

```js
const colors = await ImageColors.getColors(URI, config)
```

### URI

Can be a URL or a local asset.

- URL:

  [`https://i.imgur.com/O3XSdU7.jpg`](https://i.imgur.com/O3XSdU7.jpg)

- Local file:

  ```js
  const catImg = require("./images/cat.jpg")
  ```

### config (android)

| Property       | Description                                                                                                                                                 | Type      | Required | Default     |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- | -------- | ----------- |
| `dominant`     | Get the dominant color.                                                                                                                                     | `boolean` | No       | `false`     |
| `average`      | Get the average color.                                                                                                                                      | `boolean` | No       | `false`     |
| `vibrant`      | Get the vibrant color.                                                                                                                                      | `boolean` | No       | `false`     |
| `darkVibrant`  | Get the dark vibrant color.                                                                                                                                 | `boolean` | No       | `false`     |
| `lightVibrant` | Get the light vibrant color.                                                                                                                                | `boolean` | No       | `false`     |
| `darkMuted`    | Get the dark muted color.                                                                                                                                   | `boolean` | No       | `false`     |
| `lightMuted`   | Get the light muted color.                                                                                                                                  | `boolean` | No       | `false`     |
| `muted`        | Get the muted color.                                                                                                                                        | `boolean` | No       | `false`     |
| `fallback`     | If a color property couldn't be retrieved, it will default to this hex color string (**note**: shorthand hex will not work e.g. `#fff` ❌ vs `#ffffff` ✅). | `string`  | No       | `"#000000"` |
| `pixelSpacing` | How many pixels to skip when iterating over image pixels. Higher means better performance (**note**: value cannot be lower than 1).                         | number    | No       | `5`         |

### config (iOS)

| Property   | Description                                                                                                                                                 | Type                                                   | Required | Default     |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ | -------- | ----------- |
| `fallback` | If a color property couldn't be retrieved, it will default to this hex color string.                                                                        | `string`                                               | No       | `"#000000"` |
| `quality`  | Highest implies no downscaling and very good colors, but it is very slow. See [UIImageColors](https://github.com/jathu/UIImageColors#uiimagecolors-objects) | `'lowest'` <br> `'low'` <br> `'high'` <br> `'highest'` | No       | `"low"`     |

### Result (android)

On android, you will only get the color properties you marked as `true` in the config object, plus a `platform` key to help you figure out that this is the android result type.

| Property       | Type     |
| -------------- | -------- |
| `dominant`     | `string` |
| `average`      | `string` |
| `vibrant`      | `string` |
| `darkVibrant`  | `string` |
| `lightVibrant` | `string` |
| `darkMuted`    | `string` |
| `lightMuted`   | `string` |
| `muted`        | `string` |
| `platform`     | `string` |

### Result (iOS)

On iOS, you will always get all of the following properties regardless of what you pass to the config object, plus the respective platform key.

| Property     | Type     |
| ------------ | -------- |
| `background` | `string` |
| `primary`    | `string` |
| `secondary`  | `string` |
| `detail`     | `string` |
| `platform`   | `string` |

### Example

```js
const coolImage = require("./cool.jpg")

const colors = await ImageColors.getColors(coolImage, {
  average: true,
  fallback: "#228B22",
})

if (colors.platform === "android") {
  // Access android properties
  // e.g.
  const averageColor = colors.average
} else {
  // Access iOS properties
  // e.g.
  const backgroundColor = colors.background
}
```

### Notes

- There is an [example](https://github.com/osamaq/react-native-image-colors/tree/master/example) react-native project.
