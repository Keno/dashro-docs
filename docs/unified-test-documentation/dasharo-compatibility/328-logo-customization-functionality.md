# Dasharo Compatibility: Logo customization functionality

## Test cases common documentation

**Test setup**

1. Proceed with the
    [Generic test setup: firmware](../../generic-test-setup/#firmware).
1. Proceed with the
    [Generic test setup: OS installer](../../generic-test-setup/#os-installer).
1. Proceed with the
    [Generic test setup: OS installation](../../generic-test-setup/#os-installation).
1. Proceed with the
    [Generic test setup: OS boot from disk](../../generic-test-setup/#os-boot-from-disk).
1. Make yourself familiar with
    [Logo customization procedure](../../common-coreboot-docs/custom_logo.md)

## LCM001.001 Replace logo in existing image and flashing firmware

**Test description**

This test aims to verify whether replacing the logo in the existing image is
possible and, whether after flashing the DUT with the new image, the new logo
will be shown properly.

**Test configuration data**

1. `FIRMWARE` = Dasharo
1. `OPERATING_SYSTEM` = Ubuntu 22.04

**Test setup**

1. Proceed with the
    [Test cases common documentation](#test-cases-common-documentation) section.
1. Current Dasharo firmware dedicated for the platform.

**Test steps**

1. Power on the DUT.
1. Boot into the system.
1. Log into the system by using the proper login and password.
1. Based on the
    [dedicated documentation](../../common-coreboot-docs/custom_logo.md#replace-logo-in-an-existing-image)
    replace the logo in an existing image.
1. Flash the firmware by using the internal programmer and `flashrom` tool. If
    DUT is already flashed with the Dasharo firmware, the following command
    should be used:

    ```bash
    flashrom -p internal -w [path-to-binary] --fmap -i RW_SECTION_A
    ```

    Otherwise, the following command should be used:

    ```bash
    flashrom -p internal -w [path-to-binary] --ifd -i bios
    ```

1. Reboot DUT.

**Expected result**

During the DUT booting process, custom logo should appear on the screen.

## LCM002.001 Build image with custom logo and flashing firmware

**Test description**

This test aims to verify whether building an image with the custom logo is
possible and, whether after flashing the DUT with the new image, the new logo
will be shown properly.

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
1. Based on the
    [dedicated documentation](../../common-coreboot-docs/custom_logo.md#build-image-with-custom-logo)
    build firmware with the custom logo.
1. Flash the firmware by using the internal programmer and `flashrom` tool. If
    DUT is already flashed with the Dasharo firmware and only the logo should
    be replaced, the following command should be used:

    ```bash
    sudo flashrom -p internal --fmap -i BOOTSPLASH -w [path]
    ```

    If also the procedure of Dasharo firmware updating should be performed,
    the following command should be used:

    ```bash
    flashrom -p internal -w [path-to-binary] --fmap -i RW_SECTION_A
    ```

    In any other cases, the following command should be used:

    ```bash
    flashrom -p internal -w [path-to-binary] --ifd -i bios
    ```

1. Reboot DUT.

**Expected result**

During the DUT booting process, custom logo should appear on the screen.

## LCM003.001 Attempt to flash firmware with improper image

**Test description**

This test aims to verify whether the attempt to flash the DUT with firmware
with an improper logo is possible but will result in a fallback to the default
logo.

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
1. Based on the
    [dedicated documentation](../../common-coreboot-docs/custom_logo.md#build-image-with-custom-logo)
    build firmware with the logo, that that does not meet the
    [Quality criteria](../../common-coreboot-docs/custom_logo.md#prerequisites).
1. Flash the firmware by using the internal programmer and `flashrom` tool. If
    DUT is already flashed with the Dasharo firmware and only the logo should
    be replaced, the following command should be used:

    ```bash
    sudo flashrom -p internal --fmap -i BOOTSPLASH -w [path]
    ```

    If also the procedure of Dasharo firmware updating should be performed,
    the following command should be used:

    ```bash
    flashrom -p internal -w [path-to-binary] --fmap -i RW_SECTION_A
    ```

    In any other cases, the following command should be used:

    ```bash
    flashrom -p internal -w [path-to-binary] --ifd -i bios
    ```

1. Reboot DUT.

**Expected result**

During the DUT booting process, the default logo should appear on the screen.
