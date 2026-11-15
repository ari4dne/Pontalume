# Contributing to BLEam

Thanks for helping make BLEam better! Bug reports, ideas, and lamp profiles all help,
and every one gets read.

BLEam is made by one person in their spare time. I read every issue and reply as soon as I can.

## Ways to help

- 🐞 [Report a bug](#reporting-a-bug)
- 💡 [Share an idea or feedback](#sharing-ideas-and-feedback)
- 🎨 [Share a lamp profile](#submitting-a-lamp-profile)

Before opening an issue, please [search existing issues](https://github.com/ari4dne/BLEam/issues).
If someone has already reported it, a 👍 or a comment with your details helps just as much.

## Reporting a bug

[Open a bug report](https://github.com/ari4dne/BLEam/issues/new/choose) and include:

- **BLEam version** and **Windows version**
- **Teams version**: new Teams or classic, and the version number
- **Your light**: model, and which profile file you used
- **What happened**, and what you expected instead
- **A diagnostic export from BLEam**: open the **Debug Logs** tab, click **Export Logs**, then click
  **Reveal Exported Log** to open the folder with the file. The export covers up to the last 2 days.

> ⚠️ **Please check before you post.** BLEam tries to remove personal details from its logs,
> but that clean-up is basic. Before attaching a log or export, look through it and remove any
> **MAC addresses** (like `A4:C1:38:xx:xx:xx`), device serial numbers, or other unique IDs.

## Sharing ideas and feedback

Got an idea, or something that could work better?
[Open an idea or feedback issue](https://github.com/ari4dne/BLEam/issues/new/choose).
Tell me what you'd like BLEam to do and why it would help you.

## Submitting a lamp profile

BLEam talks to each light through a YAML lamp profile. Check the [supported lights list](profiles/SUPPORTED-LAMPS.md) first. If your light isn't supported yet,
you can make a profile yourself: the [custom lamp profile guide](guides/add-your-lamp.md) walks you through it.
The [profile template](profiles/template.yaml) explains every field in plain language, and [profile.schema.json](profiles/profile.schema.json) lets editors check your file as you type.

### Where profiles go

- **Unbranded or clone lights:** `profiles/generic/<advertised-ble-name>.yaml`,
  named by the Bluetooth name the light shows when you scan for it
- **Name-brand lights:** `profiles/<brand>/<brand>-<model>.yaml`

File names are lowercase, use hyphens instead of spaces, and end in `.yaml`. One light per file.

### Before you submit

- ✅ You've **tested it with a real light**
- ✅ You've given the **light's name and model**
- Optional: where you bought it, if you'd like to help others find lights that work. It can reveal where you live, so share only what you're comfortable with.
- ✅ It contains **no MAC addresses, serial numbers, or other device IDs**
- ✅ If you'd like credit, you've added a top-level line `author: Your Name or @github-handle` to your profile. Add it by hand: BLEam has no author field, and it drops this line if you re-save the profile in the app, so add it last.

### Two ways to submit

1. **Pull request:** add your file under `profiles/` and open a PR.
2. **No git? No problem.** Use the
   [Submit a lamp profile](https://github.com/ari4dne/BLEam/issues/new/choose) issue form,
   paste your YAML, and I'll add it for you, with credit.

Profiles are shared under [CC0 1.0](profiles/LICENSE). By submitting one, you agree to release it
under CC0 so anyone can use it freely.

## Security and privacy issues

Found something that could put users' privacy or security at risk? Please **don't** open a public issue.
[Report it privately](https://github.com/ari4dne/BLEam/security/advisories/new) instead,
so it can be fixed before it's widely known.

## Language

English is easiest for me, but please write in whatever language you're comfortable with.
I'll translate other languages with AI tools. Translations aren't always accurate,
so it may be harder for me to help as well as I'd like.

## Code of conduct

Please be kind and respectful. This project follows the [Code of Conduct](CODE_OF_CONDUCT.md).
To report a problem, use [private reporting](https://github.com/ari4dne/BLEam/security/advisories/new).
