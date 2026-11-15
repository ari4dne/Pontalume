# BLEam — feedback & community profiles

This repo is for **feedback on BLEam, a Windows app from the Microsoft Store**.
Use it to report bugs, suggest ideas, and share lamp profiles.

**Coming soon to the Microsoft Store.**

## What BLEam does

BLEam shows your Microsoft Teams presence on a Bluetooth RGB light, so anyone nearby can see at a glance whether you're free, busy or on a call. It works with work and personal accounts, tracks your presence locally, and needs no sign-in, no cloud and no admin setup. It works out of the box with the Tzumi multi color light bar and the Oiyn smart table lamp, and you can add other lights with a profile from the community or one you make yourself.

## Report a bug or share feedback

1. Read the [contributing guidelines](CONTRIBUTING.md).
2. Search [existing issues](https://github.com/ari4dne/BLEam/issues). It may already be reported.
3. [Open a new issue](https://github.com/ari4dne/BLEam/issues/new/choose) and pick a template.

You'll need a free GitHub account. **Never post personal info in an issue**, including your light's MAC address.

## Lamp profiles

BLEam talks to each light through a YAML lamp profile. Community profiles live in [`profiles/`](profiles/):

- `profiles/generic/`: unbranded and clone lights, named by the light's advertised Bluetooth name
- `profiles/<brand>/`: name-brand lights

BLEam works out of the box with two inexpensive lights: the Tzumi multi color light bar and the Oiyn smart table lamp. More lights work through profiles on GitHub, some from the community, and you can add other lights with a custom profile. See the [supported lights list](profiles/SUPPORTED-LAMPS.md) for lights that have a profile.

Some profiles are marked **untested**, which means nobody has confirmed them on real hardware yet. All profiles are provided as is, with no warranty, express or implied.

**Light not listed?** Make your own with the [custom lamp profile guide](guides/add-your-lamp.md), then share it.
Open a pull request, or use the **Submit a lamp profile** issue form if you don't use git.
See [Submitting a lamp profile](CONTRIBUTING.md#submitting-a-lamp-profile).

Profiles are licensed [CC0 1.0](profiles/LICENSE).

---

BLEam is an independent app. It isn't made by, affiliated with or endorsed by Microsoft, Tzumi or Oiyn. Microsoft Teams is a trademark of the Microsoft group of companies. Other product names belong to their owners.
