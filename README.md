```import { Meta, Props } from '@storybook/addon-docs/blocks';```

<Meta title="Library/CameraX" />

Camera View module

## Install

-   With yarn

```

yarn add @momo-kits/camerax

```

-   With npm

```

npm install @momo-kits/camerax

```

## Import

```js
import CameraX from '@momo-kits/camerax';
```

## Props

| Props         | Value                                                  | Description                            |  Note                                                                                       |
|---------------|--------------------------------------------------------|----------------------------------------|---------------------------------------------------------------------------------------------|
| style         | *View Style*                                           |                                        |                                                                                             |
| cameraType    | CaemraX.TYPE_FRONT / CameraX.TYPE_BACK                 | Control front/back camera              |  default: CameraX.TYPE_FRONT                                                                |
| onCaptured    | callback<br/> {nativeEvent: { width, height, uri}}     | Capture result after call **capture**  |  **width**: (str) img width<br/>**height**: (str) img height<br/>**uri**: (str) image uri   |
| barCodeTypes  | Array[CameraX.BAR_CODES.***barCodeType***]             | List for bar code to scan              |  **barCodeType** see below                                                                  |
| onBarCodeRead | callback<br/> { nativeEvent: Array[{ data, type }] }   | Event bar code read                    |  **data**: (str) code data<br/>**type**: CameraX.BAR_CODES.***barCodeType***<br/>           |
| torchMode     | CameraX.TORCH_OFF / CameraX.TORCH_ON                   | Control torch on/off                   |                                                                                             |

Notes:
* After reading success, `onBarCodeRead` will trigger once with an empty-array param when no bar code found
* barCodeType:
- UPC_E
- CODE39
- EAN13
- EAN8
- CODE93
- CODE128
- PDF417
- QR
- AZTEC
- INTERLEAVED2OF5
- DATAMATRIX

Android only
- UPC_EAN
- CODABAR
- MAXICODE
- RSS14
- RSSEXPANDED
- UPC_A

iOS only
- CODE39MOD43
- ITF14


## Commands

| Commands  | Description           | Note                                               |
|-----------|-----------------------|----------------------------------------------------|
| capture() | Trigger capture image | Capture result is returned in **onCaptured** event |
| stop()    | Pause camera          |                                                    |
| start()   | Unpause camera        |                                                    |

## Example

```js
import React from 'react';
import CameraX from '@momo-kits/camerax';

const ref = useRef();

const onPressCapture = () => {
    ref.current?.capture();
};

const onPressStart = () => {
    ref.current?.start();
};

const onPressStop = () => {
    ref.current?.stop();
};

const onBarCodeRead = ({ nativeEvent }) => {
    const { barCodes } = nativeEvent;
    barCodes.forEach( ({ data, type }) => {
      // do some stuff
    })
};

const onCaptured = ({ nativeEvent }) => {
    const { width, height, uri } = nativeEvent;
    // do some stuff
};

<CameraX
    style={styles.camera}
    ref={ref}
    onBarCodeRead={onBarCodeRead}
    onCaptured={onCaptured}
    cameraType={CameraX.TYPE_BACK}
    barCodeTypes={[CameraX.BAR_CODES.QR]}
    torchMode={CameraX.TORCH_ON}
/>
```
