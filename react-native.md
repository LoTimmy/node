![](https://i.imgur.com/cIsXb7G.png)

```
shell> mas install 497799835

shell> brew cask install java8
shell> brew cask install android-studio
```

```
shell> avdmanager list avd

shell> ${ANDROID_SDK_ROOT}/tools/emulator -help
shell> ${ANDROID_SDK_ROOT}/tools/emulator -list-avds

shell> tools/emulator @Nexus_5X_API_27
shell> tools/emulator @test
```

```
shell> brew install node
shell> brew install watchman

shell> npm install -g react-native-cli
shell> yarn global add react-native-cli

shell> react-native init MyApplication
shell> cd MyApplication
shell> react-native run-ios
shell> react-native run-android
```

`~/.bashrc`
`~/.bash_profile`

```
export ANDROID_HOME=~/Library/Android/sdk
export ANDROID_SDK_ROOT=$ANDROID_HOME

PATH="~/Library/Android/sdk/tools:~/Library/Android/sdk/platform-tools:${PATH}"
export PATH
```

#### :books: 參考網站：
- https://facebook.github.io/react-native/
- https://facebook.github.io/react-native/releases/0.23/docs/android-setup.html
- https://developer.android.com/studio/command-line/avdmanager.html
- https://developer.android.com/studio/command-line/sdkmanager.html
- https://facebook.github.io/react-native/docs/running-on-device.html
- https://developer.android.com/studio/command-line/variables.html

---

```js
"use strict";
import React, { Component } from "react";
import { AppRegistry, Image } from "react-native";

export default class Bananas extends Component {
  render() {
    let pic = {
      uri:
        "https://upload.wikimedia.org/wikipedia/commons/d/de/Bananavarieties.jpg"
    };
    return <Image source={pic} style={{ width: 193, height: 110 }} />;
  }
}

AppRegistry.registerComponent("MyApplication", () => Bananas);
```

---

`index.js`
```js
import {AppRegistry} from "react-native";
import App from "./App";

AppRegistry.registerComponent("AwesomeProject", () => App);
```

```
To run your app on iOS:
   cd /Users/apple/Documents/MyApplication
   react-native run-ios
   - or -
   Open ios/MyApplication.xcodeproj in Xcode
   Hit the Run button
To run your app on Android:
   cd /Users/apple/Documents/MyApplication
   Have an Android emulator running (quickest way to get started), or a device connected
   react-native run-android
```

---

```js
"use strict";
import React, { Component } from "react";
import { AppRegistry, StyleSheet, Text, View } from "react-native";

export default class MyApplication extends Component {
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.welcome}>Welcome to React Native!</Text>
        <Text style={styles.instructions}>
          To get started, edit index.android.js
        </Text>
        <Text style={styles.instructions}>
          Double tap R on your keyboard to reload,{"\n"}
          Shake or press menu button for dev menu
        </Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#F5FCFF"
  },
  welcome: {
    fontSize: 20,
    textAlign: "center",
    margin: 10
  },
  instructions: {
    textAlign: "center",
    color: "#333333",
    marginBottom: 5
  }
});

AppRegistry.registerComponent("MyApplication", () => MyApplication);
```
---

```
import { View, Text, Image } from 'react-native'
import { Card, ListItem, Button } from 'react-native-elements'
```
---

```
shell> yarn add react-native-vector-icons --save && react-native link react-native-vector-icons
shell> yarn add react-native-elements
```

```js
"use strict";
import React, {Component} from "react";
import {Platform, StyleSheet, Text, View} from "react-native";
import {Button} from "react-native-elements";
import {Icon} from "react-native-elements";

<Icon name="rowing" />
<Icon name="g-translate" color="#00aced" />
<Icon name="sc-telegram" type="evilicon" color="#517fa4" />
<Icon
  reverse
  name="ios-american-football"
  type="ionicon"
  color="#517fa4"
/>


<Button title="BUTTON" />

<Button raised icon={{ name: "cached" }} title="BUTTON WITH ICON" />

<Button
  raised
  icon={{ name: "home", size: 32 }}
  buttonStyle={{ backgroundColor: "red", borderRadius: 10 }}
  textStyle={{ textAlign: "center" }}
  title={`Welcome to\nReact Native Elements`}
/>
```

#### :books: 參考網站：
- https://react-native-training.github.io/react-native-elements/Installation/default_installation/
- https://github.com/react-native-training/react-native-elements
- https://react-native-training.github.io/react-native-elements/API/buttons/

---

```js
import { StyleSheet } from "react-native";
var styles = StyleSheet.create({
  container: {
    borderRadius: 4,
    borderWidth: 0.5,
    borderColor: "#d6d7da"
  },
  title: {
    fontSize: 19,
    fontWeight: "bold"
  },
  activeTitle: {
    color: "red"
  }
});
```

#### :books: 參考網站：
- https://facebook.github.io/react-native/docs/stylesheet.html

---

```
shell> yarn add react-native-google-static-map
```

```js
"use strict";
import GoogleStaticMap from "react-native-google-static-map";

var locationProps = {
  latitude: "25.079264",
  longitude: "121.482652",
  zoom: 16,
  size: { width: 300, height: 550 },
  apiKey: ""
};

export default class MyApplication extends Component {
  render() {
    return <GoogleStaticMap style={styles.map} {...locationProps} />;
  }
}

AppRegistry.registerComponent("MyApplication", () => MyApplication);
```

#### :books: 參考網站：
- https://github.com/yelled3/react-native-google-static-map

---

```js
"use strict";
import React, { Component } from "react";
import { AppRegistry, Text, View } from "react-native";

class Blink extends Component {
  constructor(props) {
    super(props);
    this.state = { showText: true };

    // Toggle the state every second
    setInterval(() => {
      this.setState(previousState => {
        return { showText: !previousState.showText };
      });
    }, 1000);
  }

  render() {
    let display = this.state.showText ? this.props.text : " ";
    return <Text>{display}</Text>;
  }
}

export default class BlinkApp extends Component {
  render() {
    return (
      <View>
        <Blink text="I love to blink" />
        <Blink text="Yes blinking is so great" />
        <Blink text="Why did they ever take this out of HTML" />
        <Blink text="Look at me look at me look at me" />
      </View>
    );
  }
}

AppRegistry.registerComponent("MyApplication", () => BlinkApp);
```
---

```js
class MyView extends Component {
  constructor(props) {
    super(props);
  }
  handleClick(e) {}
  render() {
    return;
  }
}
```

---

```js
import React, { Component } from "react";
import { AppRegistry, Text, View } from "react-native";

class Greeting extends Component {
  render() {
    return <Text>Hello {this.props.name}!</Text>;
  }
}

export default class LotsOfGreetings extends Component {
  render() {
    return (
      <View style={{ alignItems: "center" }}>
        <Greeting name="Rexxar" />
        <Greeting name="Jaina" />
        <Greeting name="Valeera" />
      </View>
    );
  }
}

AppRegistry.registerComponent("MyApplication", () => LotsOfGreetings);
```
```
class CustomButton extends React.Component {
  // ...
}

CustomButton.defaultProps = {
  color: 'blue'
};

  render() {
    return <CustomButton /> ; // props.color will be set to blue
  }

```

---

`MyScene.js`
```js
import React, { Component } from "react";
import { View, Text } from "react-native";

export default class MyScene extends Component {
  static propTypes = {
    title: React.PropTypes.string
  };
  static defaultProps = {
    title: "MyScene"
  };

  render() {
    return (
      <View>
        <Text>Hi! My name is {this.props.title}.</Text>
      </View>
    );
  }
}
```

```js
import React, { Component } from 'react';
import { AppRegistry, Text, View } from "react-native";

import MyScene from './MyScene';

class YoDawgApp extends Component {
  render() {
    return (
      <MyScene />
    )
  }
}

AppRegistry.registerComponent('MyApplication', () => YoDawgApp);
```

---

```js
import DeviceInfo from "react-native-device-info";

{DeviceInfo.getUniqueID()}
{DeviceInfo.getManufacturer()}
{DeviceInfo.getBrand()}
{DeviceInfo.getModel()}
{DeviceInfo.getDeviceId()}
{DeviceInfo.getSystemName()}
{DeviceInfo.getSystemVersion()}
{DeviceInfo.getDeviceName()}
{DeviceInfo.getUserAgent()}
{DeviceInfo.getDeviceLocale()}
{DeviceInfo.getDeviceCountry()}
{DeviceInfo.getTimezone()}
```

#### :books: 參考網站：
- https://github.com/rebeccahughes/react-native-device-info



---


```
shell> adb devices
shell> adb kill-server
shell> adb start-server
```
```
List of devices attached
6675dfa	device
```


---

`MyApplication/android/app/src/main/res`
`MyApplication/ios/MyApplication.xcodeproj`






---

`Create React Native App`

```
shell> yarn global add create-react-native-app
shell> create-react-native-app MyApplication
shell> cd MyApplication
shell> npm start
shell> yarn start
shell> yarn run ios
shell> yarn run android

shell> npm install -g exp
```

```
import React from "react";
import {StyleSheet, Text, View} from "react-native";

export default class App extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>Open up App.js to start working on your app!</Text>
        <Text>Changes you make will automatically reload.</Text>
        <Text>Shake your phone to open the developer menu.</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center"
  }
});
```

```
import {Ionicons} from "@expo/vector-icons";
import {Image} from "react-native";

<Ionicons name="md-checkmark-circle" size={32} color="green" />
```

```js
import React, {Component} from "react";
import {Text, View, StyleSheet} from "react-native";
import {Image} from "react-native";
import {Constants} from "expo";

// You can import from local files
import AssetExample from "./components/AssetExample";

// or any pure javascript modules available in npm
import {Card} from "react-native-elements"; // 0.17.0

export default class App extends Component {
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.paragraph}>
          Change code in the editor and watch it change on your phone! Save to
          get a shareable url.
        </Text>
        <Card title="Local Modules">
          <AssetExample />
        </Card>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center",
    paddingTop: Constants.statusBarHeight,
    backgroundColor: "#ecf0f1"
  },
  paragraph: {
    margin: 24,
    fontSize: 18,
    fontWeight: "bold",
    textAlign: "center",
    color: "#34495e"
  }
});
```

- https://play.google.com/store/apps/details?id=host.exp.exponent
- https://itunes.apple.com/us/app/expo-client/id982107779?mt=8
- https://docs.expo.io/versions/latest/guides/building-standalone-apps.html




```js
import React from "react";
import { Image, StyleSheet, View, StatusBar } from "react-native";
import { StyleSheet, Text, View } from "react-native";
import { StyleSheet, Text, TouchableOpacity, View } from "react-native";
import { Image, StyleSheet, View, StatusBar } from "react-native";
import { Text, View, TouchableOpacity } from "react-native";
import { Camera, Permissions } from "expo";
import { BlurView } from "expo";
import { BlurView } from "expo";
import { Contacts } from "expo";
import { Asset, AppLoading } from "expo";
import { Button, StyleSheet, Text, View } from "react-native";
import { AuthSession } from "expo";
import { BarCodeScanner, Permissions } from "expo";
import Expo from "expo";
import { Accelerometer } from "expo";
import {
  AdMobBanner,
  AdMobInterstitial,
  PublisherBanner,
  AdMobRewarded
} from "expo";

import { Image, Text, View } from "react-native";

```

---

Running your app on Android devices 

1. Enable Debugging over USB 
2. Plug in your device via USB 

```
$ adb devices
List of devices attached
emulator-5554 offline   # Google emulator
14ed2fcc device         # Physical device

List of devices attached
VCLVUC4DAUPZHIGY	device
```

```
shell> react-native init MyApplication
shell> cd MyApplication
shell> react-native run-android
shell> react-native run-android --deviceId VCLVUC4DAUPZHIGY
```




- [running-on-device](https://facebook.github.io/react-native/docs/running-on-device.html)






