# Pontalume supported lamps

Which lamps each profile in `profiles/generic/` is meant to control.

**Every generic profile listed here is untested.** None has been confirmed on real hardware by the maintainer. Entries come from public write-ups by other people; "driven by a source" means that source's author controlled that exact lamp. Profiles are provided as is, with no warranty, express or implied. If you test one, please tell us in a pull request or issue so the untested label can come off.

Don't see your light? See [Add your lamp to Pontalume](../guides/add-your-lamp.md).

## [elk-bledom.yaml](generic/elk-bledom.yaml): ELK-BLEDOM / Lotus Lamp X (untested)

| Brand / model | How to recognise it | Status |
|---|---|---|
| Tyute MELK-OA10 (USB 5 V RGB lamp) | Bluetooth name `MELK-OA10   5F` (spaces included) | Untested; driven by a source (lotus-lamp) |
| Generic 12 V ELK-BLEDOM strip controller | Name `ELK-BLEDOM`; aura LED app | Untested; driven by a source (arduino12), no brand named |
| Keepsmile standing ambient light (Amazon B0DHSC78P2) | Magic Lantern app | Untested; one forum post (home-assistant/core #145934), driven from an ESP32 |
| duoCo-app LED sign advertising `ELK-BLEDOM` | Name `ELK-BLEDOM`; duoCo app | Untested; one write-up (Josh Spicer), no brand named |
| Strips/lamps run by Lotus Lamp X, Lantern Lotus or duoCo Strip apps | Names starting `ELK-`, `MELK-`, `BLEDOM` | Untested; family match only, model not verified |
| Other names listed by the elkbledom README: ELK-BLEDOB, ELK-BLEDDM, ELK-BTC, ELK-BULB, ELK-BULB2, ELK-LAMPL, MELK-OC10, MELK-OF10, MELK-OG10, MELK-OA21, JACKYLED, XROCKER | Bluetooth name | Untested; names only, nobody has tried them |

Caveats: Check the first colour on each new lamp, since a JACKYLED capture shows a controller that may swap channels. `LEDBLE` names are ambiguous between this protocol and Triones. Some MELK strips reportedly need two init writes. Per Rxflex, devices whose name contains `ELK-*` may encrypt writes, which a hex-only profile can't send. Only the MELK-OA10 is a named, purchasable model with complete data. Windows links can drop after 3–10 writes.

## [yongnuo-yn360.yaml](generic/yongnuo-yn360.yaml): Yongnuo YN360 III Pro (untested)

| Brand / model | How to recognise it | Status |
|---|---|---|
| Yongnuo YN360 III Pro (handheld photo/video light) | Not stated by the source | Untested; driven by a source (yn360-ble) |
| Other Yongnuo YN360 models | Not known | Untested; may share the protocol |

Caveats: needs acknowledged (write-with-response) writes, which the schema can't request yet. One client at a time, so close the Yongnuo app. A handheld photo light, not a room lamp.

## [triones.yaml](generic/triones.yaml): Triones / HappyLighting (untested)

| Brand / model | How to recognise it | Status |
|---|---|---|
| Triones-branded RGB(W) bulbs and strips | Name `Triones`; HappyLighting app | Untested; colour and power frames match saberlight and a Home Assistant forum thread, UUIDs match saberlight and pytrionesmqtt; no model named |
| Happy Lighting | HappyLighting app | Untested; same |
| Other names Home Assistant lists (LEDnet, BLE-LED, LEDBLE, LEDBlue, Dream, QHM, AP; Magic Blue, Zengge, Zerproc) | Bluetooth name | Not tied to this protocol; several protocols share these names |

Caveats: no model is named, so don't expect any specific product to work. The controller gives no timely acknowledgement.

## [ks03.yaml](generic/ks03.yaml): Keepsmile KS03 (untested)

| Brand / model | How to recognise it | Status |
|---|---|---|
| Keepsmile LED strips | Name `KS03~` plus a suffix | Untested; two sources (a packet write-up and the cheshire library) agree on UUIDs, frame layout and power bytes but disagree on colour channel scale (0-255 vs 0-100); neither is a hardware test; no model number |

Caveat: Keepsmile strips named `KS03-` (dash) use a different protocol and are not covered.

## Not yet covered

- Govee H6127, Immersion H6199, H6001 bulb and H617A/H617E strips: they need an XOR checksum byte the profile format can't express yet. The claim that the H6001 is also sold as Minger H6001 is unverified.
- Daybetter RGB strips: need a CRC16 checksum.
- BJ_LED strips (MohuanLED app): RGB frame and write characteristic known, but no page gives the service UUID.
- FINDN strips (MR STAR, SYMPHONY LIGHT apps; name `GATT--DEMO`): only hue/saturation frames found.
