# react-native-compass-heading

## This is a mod to original `react-native-compass-heading` to give an accuracy value for android also, which is missing in the original repo.

### Accuracy is now detected by Android Java code and may alter from 0..3 where 0 is the poorest one and 3 the best one.

<img src="android.png" width="40%"> <img src="ios.png" width="40%">

credits - https://github.com/vnil/react-native-simple-compass

## Installation

`$ npm install git+https://github.com/micoFinlandes/react-native-compass-heading.git`

`$ cd ios/ && pod install && cd ..`

## Usage
```javascript
import React, {useState, useEffect} from 'react';
import {Image, StyleSheet} from 'react-native';
import CompassHeading from 'react-native-compass-heading';

const App = () => {
  const [compassHeading, setCompassHeading] = useState(0);

  useEffect(() => {
    const degree_update_rate = 3;

    // accuracy on android will be hardcoded to 1
    // since the value is not available.
    // For iOS, it is in degrees
    CompassHeading.start(degree_update_rate, {heading, accuracy} => {
      setCompassHeading(heading);
    });

    return () => {
      CompassHeading.stop();
    };
  }, []);

  return (
    <Image
      style={[
        styles.image,
        {transform: [{rotate: `${360 - compassHeading}deg`}]},
      ]}
      resizeMode="contain"
      source={require('./compass.png')}
    />
  );
};

const styles = StyleSheet.create({
  image: {
    width: '90%',
    flex: 1,
    alignSelf: 'center',
  },
});

export default App;
```
