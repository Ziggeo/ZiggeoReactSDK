## Ziggeo's React component v2
(For documentation on v1, see [here](https://github.com/Ziggeo/react-ziggeo/tree/master/docs/v1))

We have a demo project [here](https://github.com/Ziggeo/react-ziggeo/tree/master/demo) for you to clone.

## Video Recorder

```$xslt
import React from 'react'
import {ZiggeoRecorder} from 'react-ziggeo'
...
    // after react-ziggeo 4.0.0 version hooks are applied, but class Component also supportis
    // Correct way to access to recorder/player instance is:
    const [recorder, setRecorder] = useState(null);

    useEffect(() => {
        if (recorder) {
            // DO stuff here
            recorder.on("any_event", function (rec) { ... }, recorder);
            recorder.get("attribute_name");
        }

    }, [recorder]);
   
    // Embedding (player/recorder instance) will be the first argument
    const handleRecorderRecording = (embedding) => {
        console.log('Recorder onRecording');
    };

    const handleRecorderUploading = (embedding) => {
        console.log('Recorder uploading');
    };

    ...
 
    <ZiggeoRecorder
        apiKey={API_KEY}
        video={VIDEO_TOKEN}
        height={180}
        width={320}
        onRecording={handleRecorderRecording}
        onUploading={handleRecorderUploading}
    />
 
...
```
[All Built-in Recorder Events](https://github.com/Ziggeo/react-ziggeo/#available-events-for-recorder)

##### Available `event listeners` for Recorder

```react2html
   
  - onPlaying
  - onPaused
  - onAttached
  - onLoaded
  - onEnded
  - onSeek 
  - onError
  - onManuallySubmitted
  - onUploaded
  - onUploadSelected
  - onRecording
  - onUploading
  - onRerecord
  - onCountdown
  - onProcessing
  - onProcessed
  - onRecordingProgress
  - onUploadProgress
  - onAccessForbidden
  - onAccessGranted
  - onCameraUnresponsive
  - onVerified
  - onNoCamera
  - onNoMicrophone
  - onRef
```
### Recorder option Screen Recorder
Screen Capture is currently supported by Firefox, Chrome and Opera.
- Firefox: Direct support -- no extensions or plugins required
- Chrome + Opera: use extension builder located in your application manager

Note: By default Ziggeo Chrome/Opera extension will be set.
[For more info](https://ziggeo.com/features/screen-recording), in this url you also can find how to set your own extensions

```
    <ZiggeoRecorder
        apiKey={API_KEY}
        allowscreen={true}
        allowrecord={false} // Optional you can even set it to true
        allowupload={false} // Optional you can even set it to true
        
        // starting from version 3.6.1 extensions no more required
        chrome_extension_id={YOUR_CHROME_EXTENSION_ID}
        chrome_extension_install_link={YOUR_CHROME_EXTENSION_INSTALLATION_LINK}
        opera_extension_id={YOUR_OPERA_EXTENSION_ID}
        opera_extension_install_link={YOUR_OPERA_EXTENSION_INSTALLATION_LINK}
        ...
    />
```

## Video Player

```$xslt
import React from 'react'
import {ZiggeoPlayer} from 'react-ziggeo'
 
...

    const [player, setPlayer] = useState(null);

    useEffect(() => {
        if (player) {
            // DO stuff here
            player.on("attached", function (embedding) {}, player);
        }
    }, [player]);
...  
    const phandlePlaying = (embedding) => {
        console.log('it\'s playing, your action here');
    };
 
    const phandlePaused = (embedding) => {
        console.log('it\'s paused, your action when pause');
    };
 
...
    <ZiggeoPlayer
      apiKey={'your api key provided by ziggeo'}
      video={'Video Token'}
      theme={'modern'}
      themecolor={'red'}
      skipinitial={false}
      onPlaying={handlePlaying}
      onPaused={handlePaused}
      ...
    />
...
```
[All Built-in Player Events](https://github.com/Ziggeo/react-ziggeo/#available-events-for-player)

##### Available `events listeners` for Player
```react2html
   
   - onPlaying
   - onPaused
   - onAttached
   - onLoaded
   - onEnded
   - onError
   - onSeek 
   - onRef
```

#### Extensions

##### Get Recorder Instance and invoke `methods`
Add attribute `onRef={ref => (this.child = ref)}` to obtain access to recorder instances and their methods.

```javascript
    <ZiggeoRecorder
        apiKey={apiToken}
        onRef={ref => (this.child = ref)}
        // With Hooks: onRef={ref => (setChild(ref))}
    />
```

##### Get Player Instance and invoke `methods`
Add attribute `onRef={ref => (this.child = ref)}` to obtain access to player instances and their methods.

```javascript
    <ZiggeoPlayer
        apiKey={apiToken}
        video={videoToken}
        onRef={ref => (this.child = ref)}
        // With Hooks: onRef={ref => (setChild(ref))}
    />
```

## Component Options
```javascript
    preventReRenderOnUpdate={boolean} // default is true
```

## Notes
By default, components prevent re-rendering the UI with the option `preventReRenderOnUpdate`, to overwrite this.
```javascript
    <ZiggeoRecorder
        preventReRenderOnUpdate={false}
    />
```


#### Additional Parameters

React SDK supports all of the following events and parameters:
- [Ziggeo Available Parameters](https://ziggeo.com/docs/sdks/javascript/browser-integration/parameters)
- [Ziggeo Available Embedding Events](https://ziggeo.com/docs/sdks/javascript/browser-interaction/events)
- [Application-wide Embedding Events](https://ziggeo.com/docs/sdks/javascript/browser-interaction/application-embedding-events#javascript-revision=stable)

#### Changelog:
- v4.0.0 Upgraded ziggeo-client SDK to `~2.35.4` fixed bugs, added more new features `multistream` with options drag-and-drop and resize. In player now settings are manageable via methods.
- v3.6.0 Upgraded ziggeo-client SDK to `~2.35.0` fixed bugs, added more new features `multistream` with options drag-and-drop and resize. In player now settings are manageable via methods.
- v3.5.2 Upgraded ziggeo-client SDK to `~2.34.8` fixed bugs.
- v3.5.1 Upgraded ziggeo-client SDK to `~2.34.5` with new features. Stream Merge ( Like: Screen + Camera), Pausable WebRTC Recorder, Thumbnail generation.
- v3.4.0 Upgraded ziggeo-client SDK to `~2.33.0` version, to fix only-audio bug
- v3.3.0 Added `embedding` argument for each event [Application-wide Embedding Events](https://ziggeo.com/docs/sdks/javascript/browser-interaction/application-embedding-events#javascript-revision=stable)
- v3.2.0 Upgraded ziggeo-client SDK to `2.32.7` pre-release version, to fix `FF >62` `TypeError: Argument 1 is not valid for any of the 1-argument overloads of URL.createObjectURL`
- v3.1.0 Added `ready_to_play` embedding event to Player and made minor structure changes
- v3.1.1 Fixed webpack/babel polyfill issue, 'Also fixed Identifier 'e' has already been declared' related bug
- v3.0.0 Upgraded to Ziggeo R31 stable version
    -- Added locale support. Example: `locale={'de'}`
    -- Added auth support `auth={true}`
    -- Added possibility to set out `flashUrl={'flash-url'}`
- v2.5.1 babel was upgraded to version 7.*
- v2.4.1 added application option manageability `webrtc_on_mobile` & `webrtc_streaming_if_necessary`, by default both are `false` <br/>
- v2.4.0 added application option manageability `webrtc_streaming`, by default `false` <br/>
