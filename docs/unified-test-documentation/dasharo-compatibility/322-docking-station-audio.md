# Dasharo Compatibility: Docking station audio

## Test cases common documentation

**Test setup**

1. Proceed with the
    [Generic test setup: firmware](../../generic-test-setup#firmware).
1. Proceed with the
    [Generic test setup: OS installer](../../generic-test-setup#os-installer).
1. Proceed with the
    [Generic test setup: OS installation](../../generic-test-setup#os-installation).
1. Proceed with the
    [Generic test setup: OS boot from disk](../../generic-test-setup#os-boot-from-disk).
1. The docking station connected to the USB-C port.

## DAU001.001 Audio recognition (Ubuntu 22.04)

**Test description**

This test aims to verify that the external headset is properly recognized
after plugging in the 3.5 mm jack into the docking station.

**Test configuration data**

1. `FIRMWARE` = Dasharo
1. `OPERATING_SYSTEM` = Ubuntu 22.04

**Test setup**

1. Proceed with the
    [Test cases common documentation](#test-cases-common-documentation) section.

**Test steps**

1. Power on the DUT.
1. Boot into the system.
1. Log into the system by using the proper login and password.
1. Plug in a headset jack into the docking station.
1. When the `Select Audio Device` menu appears, select what type of external
    device has been connected to the laptop (headset).
1. Open a terminal window and execute the following command:

```bash
amixer -c 0 contents | grep -A 2 'Front Headphone Jack'
```

1. Disconnect the headset from the laptop.
1. Execute the following command again:

```bash
amixer -c 0 contents | grep -A 2 'Front Headphone Jack'
```

**Expected result**

1. The output of the first command should not be empty and contains the line:

```text
: values=on
```

1. The output of the second command should not be empty and contains the line:

```text
: values=off
```

## DAU001.002 Audio recognition (Windows 11)

**Test description**

This test aims to verify that the external headset is properly recognized
after plugging in the 3.5 mm jack into the docking station.

**Test configuration data**

1. `FIRMWARE` = Dasharo
1. `OPERATING_SYSTEM` = Windows 11

**Test setup**

1. Proceed with the
    [Test cases common documentation](#test-cases-common-documentation) section.

**Test steps**

1. Power on the DUT.
1. Boot into the system.
1. Log into the system by using the proper login and password.
1. Plug in a headset jack into the docking station
1. After the `Which device did you plug in` menu appearing, select what type
    of external device has been connected to the laptop (headset).
1. Find the `Speakers` icon in the bottom right part of the screen and click
    it using the right mouse button and then using the left mouse button
    click `Open Sound Settings`.
1. Locate `Input` section and click on the `Device properties` option.
1. In `Device properties` window select option `Additional device properties`.
1. Locate in `General` the section field named `Jack Information`.
1. Close the window `Microphone properties`.
1. Disconnect a headset from the laptop.
1. Select again the `Addtional device properties` option and locate again
    field named `Jack information`.

**Expected result**

1. `Jack Information` field in the first case should show the position
    `Front Panel 3.5 mm Jack`.
1. After disconnecting a headset from the laptop and checking again
    option `Addtional device properties` field `Jack Information` should not
    contain the phrase `Front Panel 3.5 mm Jack`.

## DAU002.001 Audio playback (Ubuntu 22.04)

**Test description**

This test aims to verify that the audio subsystem is able to playback audio
recordings by using the external headset speakers connected to the docking
station.

**Test configuration data**

1. `FIRMWARE` = Dasharo
1. `OPERATING_SYSTEM` = Ubuntu 22.04

**Test setup**

1. Proceed with the
    [Test cases common documentation](#test-cases-common-documentation) section.

**Test steps**

1. Power on the DUT.
1. Boot into the system.
1. Log into the system by using the proper login and password.
1. Plug in a headset jack into the docking station.
1. Open a terminal window and execute the following command:

```bash
pactl set-sink-mute alsa_output.pci-0000_00_1f.3.analog-stereo  0
pactl set-sink-volume alsa_output.pci-0000_00_1f.3.analog-stereo 65535
speaker-test
```

**Expected result**

Sound should be played from the external speakers.

## DAU002.002 Audio playback (Windows 11)

**Test description**

This test aims to verify that the audio subsystem is able to playback audio
recordings by using the external headset speakers connected to the docking
station.

**Test configuration data**

1. `FIRMWARE` = Dasharo
1. `OPERATING_SYSTEM` = Windows 11

**Test setup**

1. Proceed with the
    [Test cases common documentation](#test-cases-common-documentation) section.

**Test steps**

1. Power on the DUT.
1. Boot into the system.
1. Log into the system by using the proper login and password.
1. Plug in a headset jack into the docking station.
1. Find the `Speakers` icon in the bottom right part of the screen and click
   it using the left mouse button to open volume menu.
1. In the volume menu, click the rightmost part of it and note the reult.

**Expected result**

Sound should be played from the external speakers.

## DAU003.001 Audio capture (Ubuntu 22.04)

**Test description**

This test aims to verify that the audio subsystem is able to capture audio
from external headset connected to the docking station.

**Test configuration data**

1. `FIRMWARE` = Dasharo
1. `OPERATING_SYSTEM` = Ubuntu 22.04

**Test setup**

1. Proceed with the
    [Test cases common documentation](#test-cases-common-documentation) section.

**Test steps**

1. Power on the DUT.
1. Boot into the system.
1. Log into the system by using the proper login and password.
1. Plug in a headset jack into the docking station.
1. Open a terminal window and execute the following command:

```bash
arecord -f S16_LE -d 10 -r 16000 /tmp/test-mic.wav
```

1. Make some noise for the headset. For example, say something.
1. Execute the following command:

```bash
aplay /tmp/test-mic.wav
```

1. Execute the following command:

```bash
arecord -f S16_LE -d 10 -r 16000 /tmp/test-mic-1.wav
```

1. Make some noise for the DUT. For example tap a few times in the laptop casing.
1. Execute the following command:

```bash
aplay /tmp/test-mic.wav
```

**Expected result**

1. During playback of the first recording, all noise that was made for headset
    should be clearly heard.
2. During playback of the second recording, all noise that was made for DUT
    should be quiet or not heard.

## DAU003.002 Audio capture (Windows 11)

**Test description**

This test aims to verify that the audio subsystem is able to capture audio
from external headset connected to the docking station.

**Test configuration data**

1. `FIRMWARE` = Dasharo
1. `OPERATING_SYSTEM` = Windows 11

**Test setup**

1. Proceed with the
    [Test cases common documentation](#test-cases-common-documentation) section.

**Test steps**

1. Power on the DUT.
1. Boot into the system.
1. Log into the system by using the proper login and password.
1. Plug in a headset jack into the docking station.
1. Find the `Speakers` icon in the bottom right part of the screen and click
    it using the right mouse button and then using the left mouse button
    click `Open Sound Settings`.
1. Locate the `Test your microphone` section and observe it.
1. Create some noise for the headset to capture and note the result.
    For example, say something.
1. Create some noise for the DUT. For example tap a few times in the laptop
    casing.

**Expected result**

1. Audio level bar located in the `Test your microphone` should raise when
    some noise have been created for the headset.
1. Audio level bar located in the `Test your microphone` should not raise when
    some noise have been created for the DUT.
