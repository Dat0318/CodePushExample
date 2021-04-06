# CodePushExample
#### Document to make a sample for code push
link library: [microsoft
/
react-native-code-push](https://github.com/microsoft/react-native-code-push#how-does-it-work)<br>

link error:[Unable to resolve module code-push/script/acquisition-sdk](https://github.com/microsoft/react-native-code-push/issues/2060)<br>

link youtobe: [https://www.youtube.com/watch?v=Jo7AV5etOsA](https://www.youtube.com/watch?v=Jo7AV5etOsA)<br>

follow the link of document to create an account code push for create center for app [https://docs.microsoft.com/en-us/appcenter/distribution/codepush/rn-get-started](https://docs.microsoft.com/en-us/appcenter/distribution/codepush/rn-get-started)

init project
```
npm install --save react-native-code-push
```
then link project and config follow the above link
```
react-native link react-native-code-push
```
[link config](https://github.com/microsoft/react-native-code-push/blob/master/docs/setup-android.md)<br>
Install the App Center CLI: 
```
npm install -g appcenter-cli
```
first, create an account, you can sign in with github or gmail, ...
```
appcenter login or code-push login
if it is not run you can run code-push to see detail command line
```

create application in code push server
```
appcenter apps create -d MyApp-Android -o Android -p React-Native
appcenter apps create -d MyApp-iOS -o iOS -p Cordova
```
create deployment default for all staging and production for and app

```
code-push deployment add JoJoAndroid --default
```

and can get token of this app with environment,if you forgot can use this command line to get this information

```
code-push deployment ls JoJoAndroid -k
```

second, wrap application with code push libraries
```
import React from 'react';
import type { Node } from 'react';
import {
  SafeAreaView,
  StyleSheet,
  Text,
  View,
} from 'react-native';
import codePush from "react-native-code-push";

const App: () => Node = () => {

  return (
    <SafeAreaView>
        <View
          style={styles.sectionContainer}>
          <Text>Check your code push example</Text>
        </View>
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  sectionContainer: {
    flex: 1,
    justify-content: 'center',
    alignItem: 'center',
    backgroundColor: 'red',
  },
});

export default codePush(App)
```

check code,if it run you can build a apk file and then install in a device

change some style for app, and then push this change by this command line
and then you can check for your app it is installed

```
code-push release-react CodePushExample(App name) android -d Production
```

check command line and + platform and status of application

fix error
1 - In the node_modules/react-native-code-push/CodePush.js file, change the import path from "code-push/script/acquisition-sdk" to "code-push/src/script acquisition-sdk".

2 - In the node_modules/code-push/src/script/acquisition-sdk.ts file
and change file follow below

```
export module Http {
    export const Verb = {
        GET: "GET",
        HEAD: "HEAD",
        POST: "POST",
        PUT: "PUT",
        DELETE: "DELETE",
        TRACE: "TRACE",
        OPTIONS: "OPTIONS",
        CONNECT: "CONNECT",
        PATCH: "PATCH"
    }

    type VerbProps = keyof typeof Verb;
}
```