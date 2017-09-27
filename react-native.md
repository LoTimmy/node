![](https://i.imgur.com/cIsXb7G.png)

```
shell> mas install 497799835

shell> brew cask install java
shell> brew cask install android-sdk
shell> brew cask install android-studio
```

```
shell> sdkmanager "system-images;android-25;google_apis;x86_64"

shell> avdmanager create avd -n test -k "system-images;android-25;google_apis;x86_64"
Auto-selecting single ABI x86_64========] 100% Fetch remote repository...
Do you wish to create a custom hardware profile? [no]

shell> avdmanager list avd

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

![](https://facebook.github.io/react-native/releases/0.23/img/AndroidSDK1.png)
![](https://facebook.github.io/react-native/releases/0.23/img/AndroidSDK2.png)

---

#### :books: 參考網站：
- https://facebook.github.io/react-native/
- https://facebook.github.io/react-native/releases/0.23/docs/android-setup.html
- https://developer.android.com/studio/command-line/avdmanager.html
- https://developer.android.com/studio/command-line/sdkmanager.html

---

### Hello World

`index.ios.js`
`index.android.js`

```js
import React, { Component } from "react";
import { AppRegistry, Text } from "react-native";

export default class HelloWorldApp extends Component {
  render() {
    return <Text>Hello world!</Text>;
  }
}

AppRegistry.registerComponent("AwesomeProject", () => HelloWorldApp);
```

---

```js
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

AppRegistry.registerComponent("AwesomeProject", () => Bananas);
```
---

```js
import React, { Component } from "react";
import { AppRegistry, StyleSheet, Text, View } from "react-native";

export default class AwesomeProject extends Component {
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

AppRegistry.registerComponent("AwesomeProject", () => AwesomeProject);
```
