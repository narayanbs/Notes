Install android studio
Configure and initialize emulator

start the emulator using the cli . 
```bash
# list the configured simulators
emulator -list-avds
# choose one and start
emulator -avd Pixel_XL_API_33
```

Install and use expo
```bash

npm install -g expo-cli
npx create-expo-app WeatherApp
npm start 
```
choose a (android) and the app will be loaded in the emulator. or Install expo-go client from the play store and use it for testing 

If you don't want to use expo and want to use react native cli then 
```bash
npx react-native start --> for metro
npx react-native run-android
```

##### Editor Configurations

Install eslint and prettier. Use configurations provided in WeatherApp 
```bash
npm install eslint --save-dev
npx eslint --init
npm install @react-native-community/eslint-config --save-dev
npm install --save-dev --save-exact prettier
```