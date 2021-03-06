# MMM-Snowboy

<p align="right">
  <a href="http://choosealicense.com/licenses/mit"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License"></a>
</p>

MMM-Snowboy is a customizable hotword detection module to activate any assistant of your [MagicMirror](https://github.com/MichMich/MagicMirror)

This module can listen any hotword like "Smart mirror" , "Jarvis" or "Alexa" (standard hotwords from Snowboys database)

## Installation and updates
To install and update MMM-Snowboy module, you can use automatic scripts. 

### Automatic installation
For automatic installation run this command and execute electron rebuild step:
  
```sh
cd ~/MagicMirror/modules/
git clone https://github.com/bugsounet/MMM-Snowboy
cd MMM-Snowboy
npm install
```

### Manual installation
MMM-Snowboy need some libraries 
`libmagic-dev libatlas-base-dev sox libsox-fmt-all build-essential`

```sh
sudo apt-get install libmagic-dev libatlas-base-dev sox libsox-fmt-all build-essential
cd ~/MagicMirror/modules/
git clone https://github.com/bugsounet/MMM-Snowboy
cd MMM-Snowboy
npm install
```
Don't execute automatic installation

`Do you want to execute automatic intallation ? [Y/n]`<br>
`Your choice: N`<br>

Don't execute electron rebuild

`Do you want to execute electron rebuild ? [Y/n]`<br>
`Your choice: N`<br> 

Now, do electron rebuild step manualy:
```sh
./node_modules/.bin/electron-rebuild
```


### Automatic update
If you have installed module already, run the following code to update your install:
```sh
cd ~/MagicMirror/modules/MMM-Snowboy
npm run update
```

### Full Snowboy rebuild
  * If you have some trouble with new a version of MagicMirror<br>
  * If you want install lasted version of `@bugsounet/snowboy` library
```sh
cd ~/MagicMirror/modules/MMM-Snowboy
npm run rebuild
```
## Update

**2020/05/27**: v1.2.0
  * Fix: Sample default notification

**2020/04/22**: v1.1.1
  * Fix: Cleaning old library (not needed)
  
**2020/04/21**: v1.1.0
  * ADD: use npm [@bugsounet/snowboy](https://github.com/bugsounet/snowboy) library
  * FIX: new Code for this library
  
**2020/04/11**: v1.0.1
  * FIX: Installer
  * ADD: Alexa
    
**2020/04/09**: v1.0.0
  * Initial Release

## Configuration
### Minimal configuration
```js
{
  module: 'MMM-Snowboy',
  config: {
    Frontend: false,
    Model: "smart_mirror"
  }
},
```
### Personalized configuration
this is the default configuration defined if you don't define any value

```js
{
  module: 'MMM-Snowboy',
  config: {
    debug: false,
    AudioGain: 2.0,
    Frontend: true,
    Model: "jarvis",
    Sensitivity: null,
    micConfig: {
      recorder: "arecord",
      device: "plughw:1"
    },
    onDetected: {
      notification: "SHOW_ALERT",
      parameters: {
        type: "notification",
        message: "Detected !",
        title: "MMM-Snowboy",
        timer: 10 * 1000
       }
    }
  }
},
```
### Options

- `debug` - turn on/off debug mode.

- `AudioGain` - set the gain of mic. Usually you don't need to set or adjust this value.

- `Frontend` -  set pre-processing of hotword detection. When you use only snowboy and smart_mirror, false is better. But with other models, true is better to recognize.

- `Model` - set the name of your detector. Available: "smart_mirror", "jarvis", "computer", "snowboy", "subex", "neo_ya", "hey_extreme", "view_glass"

- `Sensitivity` - Override default sensitivity value for applied model defined in `Model`. 
    * Value could be within a range from `0.0` to `1.0`.
    * Default sensitivity values for preconfigured models are:
      * smart_mirror: `0.5`
      * jarvis: `0.7`
      * computer: `0.6`
      * snowboy: `0.5`
      * subex: `0.6`
      * neo_ya: `0.7`
      * hey_extreme: `0.6`
      * view_glass: `0.7`
      * alexa: `0.6`

    * `null` will set default sensitivity.

- `recorder` - record program, `rec`, `arecord`, `sox`, `parec` is available.
    * On RaspberryPi or some linux machines, `arecord` is better.
    * On OSX, `rec` is better.
    * If you prefer to use `pulse audio`, `parec` would be available also.

- `device` - recording device (microphone) name of your environment. (e.g. "plughw:1")
    * Find proper device name by yourself. (arecord -l will be help on Raspberry Pi)

- `notification` - notification name to emit when the hotword is detected.

- `parameters` - payload to send with your notification.

 ### Notification received
 MMM-Snowboy can receive notification for start or stop listening
  * `SNOWBOY_START`: Start listening with your prefered hotkey
  * `SNOWBOY_STOP`: Stop Litening
  
 ### Notes
  * this module don't need position, because it don't use any visual
  * With npm install, you can generate a proper micConfig {} configuration.
  
 ### Snowboy
 This module use my personal [@bugsounet/snowboy](https://github.com/bugsounet/snowboy) library build for node and will be maintened<br>
 Original [snowboy@kitt-AI](https://github.com/Kitt-AI/snowboy) source will be unmaintened soon
