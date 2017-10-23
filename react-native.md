![](https://i.imgur.com/cIsXb7G.png)

```
shell> mas install 497799835

shell> brew cask install java
shell> brew cask install java8
shell> brew cask install android-sdk
shell> brew cask install android-studio
```

```
shell> touch ~/.android/repositories.cfg
shell> sdkmanager --list
shell> sdkmanager "system-images;android-25;google_apis;x86_64"
shell> sdkmanager "system-images;android-24;default;x86"

shell> avdmanager create avd -n test -k "system-images;android-25;google_apis;x86_64"
Auto-selecting single ABI x86_64========] 100% Fetch remote repository...
Do you wish to create a custom hardware profile? [no] no

yes

shell> avdmanager create avd -n test -k "system-images;android-24;default;x86"

shell> avdmanager list avd

shell> touch ~/.android/advancedFeatures.ini
HVF = off

shell> emulator -help
shell> emulator -list-avds
shell> emulator @test
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
export PATH="/usr/local/share/android-sdk/emulator:$PATH"
export ANDROID_SDK_ROOT=/usr/local/share/android-sdk
export ANDROID_HOME=/usr/local/share/android-sdk
```

#### :books: 參考網站：
- https://facebook.github.io/react-native/
- https://facebook.github.io/react-native/releases/0.23/docs/android-setup.html
- https://developer.android.com/studio/command-line/avdmanager.html
- https://developer.android.com/studio/command-line/sdkmanager.html
- https://facebook.github.io/react-native/docs/running-on-device.html

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
shell> yarn add react-native-elements
```

```js
"use strict";
import { Text, Avatar, Button } from "react-native-elements";

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


















