# react-native-image-colors

![Platform](https://img.shields.io/badge/platform-ios%20%7C%20android-green)
![TypeScript](https://img.shields.io/badge/typescript-typed-blue)
[![NPM Badge](https://img.shields.io/npm/v/react-native-image-colors)](https://www.npmjs.com/package/react-native-image-colors)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-%23ff69b4)

Fetch prominent colors from an image using a URL.

<p align="center" >
  <img
    width="250px"
    src="https://github.com/osamaq/react-native-image-colors/raw/master/assets/example1.png"
    alt="Example 1"
  />
  <img
    width="250px"
    src="https://github.com/osamaq/react-native-image-colors/raw/master/assets/demo1.png"
    alt="Demo 1"
  />
  <img
    width="250px"
    src="https://github.com/osamaq/react-native-image-colors/raw/master/assets/demo2.png"
    alt="Demo 2"
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
const colors = await ImageColors.getColors(URL, config)
```

### URL

e.g.

[`https://i.imgur.com/O3XSdU7.jpg`](https://i.imgur.com/O3XSdU7.jpg)

### config (android)

| Property       | Description                                                                                                                                                                                                                    | Type      | Required |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------- | -------- |
| `dominant`     | Get the dominant color if true.                                                                                                                                                                                                | `boolean` | No       |
| `average`      | Get the average color if true.                                                                                                                                                                                                 | `boolean` | No       |
| `vibrant`      | Get the vibrant color if true.                                                                                                                                                                                                 | `boolean` | No       |
| `darkVibrant`  | Get the dark vibrant color if true.                                                                                                                                                                                            | `boolean` | No       |
| `lightVibrant` | Get the light vibrant color if true.                                                                                                                                                                                           | `boolean` | No       |
| `darkMuted`    | Get the dark muted color if true.                                                                                                                                                                                              | `boolean` | No       |
| `lightMuted`   | Get the light muted color if true.                                                                                                                                                                                             | `boolean` | No       |
| `muted`        | Get the muted color if true.                                                                                                                                                                                                   | `boolean` | No       |
| `defaultColor` | If a color property couldn't be retrieved, it will default to this hex color string. If this parameter is not passed, `#000000` will be used (**_important_**: shorthand hex will not work e.g. `#fff` ❌ **vs** `#ffffff` ✅) | `string`  | No       |

### config (iOS)

| Property       | Description                                                                                                                                   | Type     | Required |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
| `defaultColor` | If a color property couldn't be retrieved, it will default to this hex color string. If this parameter is not passed, `#000000` will be used. | `string` | No       |

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
const colors = await ImageColors.getColors(this.URL, {
  average: true,
  defaultColor: "#000000",
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

- The `background` property in the iOS result and the `average` property in the android result are usually similar colors.
- There is an [example](https://github.com/osamaq/react-native-image-colors/tree/master/example) react-native project.
