# Add your lamp to Pontalume

This guide shows you how to make a *profile* to allow Pontalume to talk to your light. Please read the entire guide once before doing it so you know what you are embarking on. If you think this is beyond your technical abilities, you can ask a tech savvy friend to see if she can help you.

This is the advanced route. You capture the light's Bluetooth traffic from an Android phone with `adb`, read the commands in Wireshark, and write them into a YAML file. If your light is in the [supported lights list](../profiles/SUPPORTED-LAMPS.md), import its profile instead. Notes for readers new to this are at the [end](#new-to-this).

> **No guarantee.** Profiles, and this guide, are provided as is, with no warranty of any kind, express or implied. Use them at your own risk.

## Will my light work?

Not every light can work with Pontalume, and some never will. The current version of Pontalume sends fixed bytes with your red, green and blue values (and optionally brightness) filled in, and nothing more. Lights that need more may work in a future version. Your light is probably not supported if:

- one byte in each command changes in a way you can't tie to red, green, blue or brightness (a checksum),
- the bytes look scrambled and change when you repeat the same action (encryption),
- the commands are text, not plain bytes, or
- the light only keeps working if something is sent to it every few seconds.

You can only tell once you have a capture (Step 2).

## What you need

- The light, working with its own Android app.
- An Android phone and a USB cable.
- A Windows PC with `adb` ([platform-tools](https://developer.android.com/tools/releases/platform-tools)), [Wireshark](https://www.wireshark.org/) and Pontalume.

## Step 1: Get the template

In Pontalume, go to **Settings**, **Write profile template** and click **Create**. Pontalume writes `template.yaml` to your profiles folder (`Documents\Pontalume\Profiles`). Copy the file and rename the copy. Its comments describe every field. The same file is in the repo as [template.yaml](../profiles/template.yaml), and [profile.schema.json](../profiles/profile.schema.json) lets an editor like VS Code check your file as you type.

## Step 2: Capture the light's commands

There are many versions of Android and tools. It is impossible to offer a comprehensive guide for the steps that follow, so please take this as a general guide. Menus differ between phones and Android versions. If a step doesn't match yours, search online for your phone model with "enable Bluetooth HCI snoop log" or "adb bugreport".

1. Enable developer options and USB debugging ([note 1](#note-1-developer-options-and-usb-debugging)).
2. Switch off or move away other Bluetooth devices. The capture contains every device the phone talks to.
3. Turn on **Enable Bluetooth HCI snoop log**, then switch the phone's Bluetooth off and on. This starts a clean capture that includes the moment the app connects.
4. Open the light's own app and connect. Do the following in order, about five seconds apart, and write the order down:
   1. off, on,
   2. red, green, blue,
   3. if the app has brightness: half-bright red, then brightness lowest, then highest.
5. Switch the snoop log off. Connect the phone by USB and accept the prompt.
6. Run ([note 2](#note-2-adb-and-the-command-prompt)):

   ```
   adb devices
   adb bugreport lamp.zip
   ```

7. Open the zip and search for the Bluetooth log: usually `btsnoop_hci.log` or `hci_snoop` plus a timestamp, commonly under `FS/data/misc/bluetooth/logs`. The location differs by phone, and some bug reports don't include it.

## Step 3: Read the capture

Open the log in Wireshark and filter on `btatt` ([note 3](#note-3-wireshark-basics)). Find the packets the phone writes to the light (*Write Request* or *Write Command*).

- The written bytes, in the order of your actions, are the light's commands.
- Each write targets a handle. Near the start of the capture the phone discovers the light's services: map the handle to its **characteristic UUID** and its **service UUID**.

An AI assistant can do this reading for you without the log leaving your PC. Don't upload the capture. Instead, ask the assistant to write a script (Python, say) that you run locally on the log. It should list the service and characteristic UUIDs and the bytes the phone wrote to the light, in order. You get what you need, and everything stays on your machine.

Mind the privacy: the raw log lists the other Bluetooth devices near your phone, with their addresses. Don't share the capture, or paste unfiltered output from it, anywhere. Delete the capture when you're done. Never post a Bluetooth address, serial number or other device ID.

## Step 4: Write the profile

Compare the red, green and blue writes. Replace the bytes that carry the color with `{R:X2}`, `{G:X2}` and `{B:X2}`. If red was `AA FF 00 00 BB`, green `AA 00 FF 00 BB` and blue `AA 00 00 FF BB`:

```yaml
customCommands:
  colorCommand: AA{R:X2}{G:X2}{B:X2}BB
```

Rules:

- Plain hexadecimal: no `0x`, no `:` or `-`, no text ([note 4](#note-4-hex-and-uuids)).
- `{BR:X2}` is brightness; `{B:X2}` is always blue.
- `brightnessCommand` is optional and takes only `{BR:X2}`. Pontalume fills brightness in as 0 to 255, so leave the command out if the light's range ends at 100.
- `wakeCommand` is optional, is sent once when the light connects, and takes no placeholders.

Fill in the rest from the template: `name`, both UUIDs, and a color for all ten presence states (`Unknown`, `Available`, `Busy`, `DoNotDisturb`, `Away`, `BeRightBack`, `InACall`, `InAMeeting`, `Offline`, `PresenceUnknown`). The names are case-sensitive and none can be omitted.

## Step 5: Import and test

In Pontalume: **Settings**, **Profiles**, **Import profile**, **Import**, then pick the file. Pontalume says at once whether the profile was imported or could not be read. If it could not, the **Debug Logs** tab names each problem. Fix them and import again.

Then connect the light and choose the new profile, as in the [quick start](quick-start.md). Check every color on the light, including a mid-tone. Swapped colors or washed-out mid-tones point to a different channel order or scale than you captured.

## Step 6: Share it (optional)

- Test it with a real light first.
- Say the light's name and model. Where you bought it is optional: add it if you want to help others find lights that work, but it can reveal where you live, so share only what you're comfortable with.
- Make sure the file has no MAC addresses, serial numbers or other device IDs.
- For credit, add the line `author: Your Name or @github-handle` at the top level of the file, and add it last, once the profile works. Pontalume has no author field, so it drops the line if you re-save the profile in the app.

Name and place the file as in [Submitting a lamp profile](../CONTRIBUTING.md#submitting-a-lamp-profile), then open a pull request, or use the **Submit a lamp profile** form under [Open a new issue](https://github.com/ari4dne/Pontalume/issues/new/choose) if you don't use git. Profiles are shared under [CC0 1.0](../profiles/LICENSE).

## Need help?

Open an [issue](https://github.com/ari4dne/Pontalume/issues/new/choose) and pick a template. Leave out Bluetooth addresses and device IDs.

## New to this?

Short notes for the steps above.

### Note 1: Developer options and USB debugging

Open the phone's **Settings**, then **About phone**, and tap **Build number** seven times. A new **Developer options** entry appears in Settings (often under **System**). Open it and turn on **USB debugging**. The snoop log switch, **Enable Bluetooth HCI snoop log**, is in the same screen.

### Note 2: adb and the command prompt

`adb` is a small program from Google. Download **platform-tools** from the link above and unzip it to a folder. Open that folder in File Explorer, click the address bar, type `cmd` and press Enter. A command prompt opens in that folder, and `adb devices` works there. The first time, the phone asks whether to trust the PC: accept.

### Note 3: Wireshark basics

Use **File, Open** to load the log. Type `btatt` into the bar at the top (the display filter) and press Enter: only the light's command traffic stays visible. A *handle* is a number that stands for one characteristic of the light. A write to handle `0x0012` and a discovery packet that lists handle `0x0012` with a UUID tell you which characteristic that is.

### Note 4: Hex and UUIDs

Hex is a way of writing bytes with the digits 0 to 9 and letters A to F, two characters per byte (`FF` is 255). A UUID is a long label with dashes, such as `0000ffd5-0000-1000-8000-00805f9b34fb`. Short ones like `ffd5` expand to that form by filling in the rest.
