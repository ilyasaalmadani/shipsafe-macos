<div align="center">

<img src="media/icon.png" width="128" alt="SHIPSAFE app icon">

# SHIPSAFE

**Release readiness for your code. The last check before you hit Archive, push to production, or submit.**

A native Mac app that scans your project locally for the mistakes that slip into releases: leaked API keys, debug config, unguarded admin routes, risky dependencies, destructive migrations. Every finding comes with the file, the line, and the fix.

[![Download on the Mac App Store](https://img.shields.io/badge/Mac_App_Store-Download-0D96F6?style=for-the-badge&logo=apple&logoColor=white)](https://apps.apple.com/us/app/shipsafe-release-readiness/id6808833747?mt=12)

![macOS 13+](https://img.shields.io/badge/macOS-13%2B-black?logo=apple)
![Apple silicon](https://img.shields.io/badge/Apple_silicon-native-black)
![148 checks](https://img.shields.io/badge/checks-148-6E56CF)
![No uploads](https://img.shields.io/badge/source_upload-never-2EA44F)
![No AI calls](https://img.shields.io/badge/AI_calls-none-2EA44F)

<img src="media/shipsafe-demo.gif" width="320" alt="SHIPSAFE 30-second demo">

[Watch the full 30-second demo (MP4)](media/shipsafe-demo-30s.mp4)

</div>

---

## Friday, 5:58 PM

You're about to ship. The build is green. The tests pass.

And somewhere in your repo there's still a `sk_live_` Stripe key, an `OPENAI_API_KEY` hardcoded in a Swift file "just for testing", a `DEBUG = true` in the backend config, and an `/admin` route with no auth check.

Tests don't catch these. Code review often doesn't either. **SHIPSAFE does, in seconds, on your Mac.**

## Why Apple developers use it

Most Apple apps don't ship alone. There's the app, and there's usually a backend, a web dashboard, a webhook server, or a set of cloud functions behind it. SHIPSAFE reviews the whole project folder before release.

- **Catch keys before they ship inside your app binary.** OpenAI, Stripe live, AWS, GitHub, Google and Slack keys, plus private keys and committed `.env` / `credentials.json` / `service-account.json` files. It reads `.swift`, `.plist`, `.xcconfig`, JSON, YAML and every other text file. A key compiled into an `.ipa` or `.app` can be pulled out by anyone who downloads it.
- **Find what you left in "for now."** Debug output, development-only flags, TODO and FIXME markers, test shortcuts, verbose error pages that leak stack traces.
- **See your backend's attack surface.** Every route, whether it's public, authenticated or admin, and which ones change data with no protection.
- **Check your dependencies.** Missing or unpinned lockfiles, risky version specs, supply-chain signals across your manifests.
- **Stop destructive migrations.** `DROP`, unguarded deletes and schema changes that can wipe production data.
- **Your code never leaves your Mac.** No account, no upload, no telemetry, no AI calls. Under NDA or working on an unreleased app? That's the point.

## What you get

| | |
|---|---|
| **Release-readiness score** | One score out of 100 and a clear release status for the whole project. |
| **Evidence-backed findings** | Grouped by severity, searchable and filterable, each with the exact file and line. |
| **Explanations written for humans** | For every one of the 148 checks: why it matters, what to verify, how to fix it. |
| **Attack-surface map** | Routes, protection level, sensitive and admin endpoints. |
| **Dependency posture** | Manifests, lockfiles, risky specs, supply-chain signals. |
| **Scan history** | A readiness trend per project, so you can see each release get safer. |
| **Professional report** | Open in-app or export as PDF or HTML. Hand it to your team, your client or your reviewer. |
| **Mac-native workflow** | Reveal in Finder, open in your editor, copy a finding as Markdown, keyboard shortcuts, light and dark mode. |

## Screenshots

| | |
|---|---|
| ![Overview](media/screenshots/1-overview.jpg) | ![Release readiness score](media/screenshots/2-score.jpg) |
| **Pick a folder, or try the bundled sample** | **Release readiness score and severity breakdown** |
| ![Findings](media/screenshots/3-findings.jpg) | ![Attack surface](media/screenshots/4-attack-surface.jpg) |
| **Every finding with evidence and a fix** | **Attack-surface map of your routes** |
| ![Scan history](media/screenshots/5-history.jpg) | ![Report](media/screenshots/6-report.jpg) |
| **Readiness trend across scans** | **Shareable PDF / HTML report** |

## Try it in under a minute

1. [Get SHIPSAFE on the Mac App Store](https://apps.apple.com/us/app/shipsafe-release-readiness/id6808833747?mt=12).
2. Click **Try the Sample Project**. It's a small Node.js service with planted issues and fake secrets.
3. Read the findings, then point SHIPSAFE at your own project folder.

SHIPSAFE only reads your project. It never modifies it.

## Where it fits

Run it:

- before you **Archive** and upload a build to App Store Connect or TestFlight,
- before you **deploy** the backend your app talks to,
- before you **hand over** a project to a client,
- before you **open-source** a repo that used to be private.

## FAQ

**Does it upload my code anywhere?**
No. Scans run entirely on your Mac inside a sandboxed engine. There is no account, no telemetry and no network call to any AI service. Scan history stays in the app's own container.

**What languages and stacks does it understand?**
Secret detection runs on every text file, including Swift, plist, xcconfig, JSON and YAML. Leftover-code checks cover Swift, Kotlin, Java, JavaScript/TypeScript, Python, PHP, Ruby, Go, Rust and web files. Route, dependency and database checks go deepest on JavaScript/TypeScript backends (Node.js, Express and similar).

**Does it guarantee App Review approval or a secure app?**
No. SHIPSAFE is a release-review assistant. Automated findings can include false positives or miss context. Review the evidence and make the final call yourself.

**Requirements?**
An Apple silicon Mac running macOS 13 or later.

**Is the source code here?**
No. SHIPSAFE is a commercial app. This repository holds the demo, screenshots and the place to talk to us.

## Feedback, bugs and feature requests

Open an [issue](../../issues/new/choose). Tell us which check you'd like next, a false positive you hit, or the stack you want covered. Every request is read.

If SHIPSAFE caught something before you shipped it, a ⭐ on this repo helps other developers find it.

## Links

- Mac App Store: https://apps.apple.com/us/app/shipsafe-release-readiness/id6808833747?mt=12
- Website: https://shipsafe.lagirame.id
- Privacy policy: https://shipsafe.lagirame.id/privacy

---

<div align="center">

Ilyas A. Almadani · PT Jiji Labs Digital<br>
© 2026 PT Jiji Labs Digital. All rights reserved.

</div>
