# matrix-midi-xy 
> A Pu(rr) Data patch to transform XY blob-tracking to Midi CC channels

![matrix_midi_xy](https://user-images.githubusercontent.com/9277107/85239127-990a8c00-b475-11ea-837a-e4c3b1fd49d3.png)

## 🐯 Overview 

Extendeding the original [Pure Data patch](https://github.com/eTextile/Matrix/tree/master/Software/Puredata_SLIP-OSC) for the [eTextile multi-touch matrix sensor](https://matrix.etextile.org/) this patch both unpacks the blob extracted from the SLIP-OSC connection, and now it interpolates the XY values based on each UID (generally fingers) and outputs them across multiple MIDI CC channels.

## 🎼 Features 

- Unpack blob data.
- XY values for 3 UIDs `(default: 0 - 2 )`
- 6 MIDI CC Channels `(default: 0 - 5)`
- Linear interpolation `(default: XY[0 - 60] -> MIDI[1 - 127])`

## 🎚️ Instructions

### MIDI Bus

We're going to need a virtual MIDI device in order to route the output from Pure Data to a DAW or other software.

The setup varies depending on your operating system. Ableton have a great guide for both Windows and macOS.

https://help.ableton.com/hc/en-us/articles/209774225-How-to-setup-a-virtual-MIDI-bus

Once you've setup a virtual MIDI device, be sure to have it selected whenever you open Pure Data.

![select-midi](https://user-images.githubusercontent.com/9277107/85240305-0cfb6300-b47b-11ea-9464-45ee7c91eb74.png)


### Pure Data

1. The patch attempts to establish a connection with the eTextile Matrix using a **virtual COM port**. object. There are no assumptions made about which port the e256 Matrix is available on, so be sure to adjust `open #` where "#" is your COM port. 
    - ![com-port](https://user-images.githubusercontent.com/9277107/85240724-729c1f00-b47c-11ea-8041-65af24575a3c.gif)
    - Select `devices` to view available COM ports.
    - Enter **Edit Mode**
        - To toggle edit mode, the user can select the function by clicking “Edit” menu and selecting Edit mode.
        - Alternative `Command + E` (Mac OS X). or `Ctrl + E` (Win).
        - Update **Open** object with correct value.

2. You're now ready to trigger the `ON/OFF` object to establish a connection with the e256 Matrix.
    - ![e265-start](https://user-images.githubusercontent.com/9277107/85240851-14237080-b47d-11ea-9087-bc7319e844f4.gif)
    - The embedded _e256_SLIP-OSC_input_ sub-patch handles communication with the e256 Matrix via SLIP encoded OSC. There are 3 UI objects to adjust for **calibration**, **on/off** and **threshold** adjustment.

3. The UID 0 1 2 sub-patches should light-up with data whenever the e265 is touched.
    - ![uid-play-2](https://user-images.githubusercontent.com/9277107/85240615-1c2ee080-b47c-11ea-9bf5-ea6e4e08bad4.gif)
    - You can adjust the range of the XY/MIDI interpolation by entering **Edit Mode** (described above) and alternating the values for either objects.

4. It's now time to load-up a DAW or any software capable of receiving MIDI and you're away! 🛫☁️
- ![midi-kontakt](https://user-images.githubusercontent.com/9277107/85240483-b5112c00-b47b-11ea-9a13-898bcd9efe03.gif)


## 💿 Requirements

#### Recommended
- [Purr Data](https://agraef.github.io/purr-data/)
    - Jonathan Wilkes’ Purr Data based on Ico Bukvic’s Pd-l2ork, which in turn is a fork of Hans-Christoph Steiner’s Pd-extended.

#### Optional Alternative
 - [Pure Data](http://puredata.info/downloads)
    - Miller S. Puckette's "vanilla" distribution of Pd is perfect.
 - [Externals](https://puredata.info/docs/faq/how-do-i-install-externals-and-help-files)
    - `comport`, for Virtual COMs
    - `mrpeach`, for SLIP encoding
    - `OSC`, for OSC packing

