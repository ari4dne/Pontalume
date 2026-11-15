# BLEam quick start

Connect your light to BLEam and see your Microsoft Teams presence on it.

## Before you start

- You need a light that has a working profile. Check the [supported lights list](../profiles/SUPPORTED-LAMPS.md). Not on the list? See [Add your lamp to BLEam](add-your-lamp.md).
- Plug in your light if it needs power, and turn it on.
- Disconnect it from its own app. A light usually talks to one app at a time, so close the lamp's phone app, or turn Bluetooth off on your phone.

## Connect your light

1. Open BLEam and go to the **Devices** tab.
2. Make sure Bluetooth is on for your PC. The badge at the top left reads **Bluetooth is ready** when it is. If it isn't, click **Bluetooth Settings** in BLEam (or open the Windows Settings app) and turn Bluetooth on.
3. Click **Scan Devices** and wait a few seconds.
4. Find your light under **Discovered nearby** and select it.
5. Scroll down and choose its profile from the drop-down.
6. Click **Connect**.

Once connected, your light shows under **Known devices** with a green **Connected** badge. The **Dashboard** tab shows your current Teams presence and the color your light is showing.

## If it doesn't work

- Light not in the list: check that it's on, close to the PC and disconnected from its own app, then scan again.
- Light connects but shows the wrong colors, or no colors: you may have picked the wrong profile. Forget the light, scan again and choose another profile.
- Still stuck: the **Debug Logs** tab shows what BLEam is doing. See the [contributing guidelines](../CONTRIBUTING.md) for how to report a problem.

## Next

- [Fine-tune your light's colors](fine-tune-colors.md)
- [Add your own lamp](add-your-lamp.md)
