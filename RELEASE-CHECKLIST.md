# The pre-release security checklist for iOS and Mac developers

A practical list to run through before you hit **Archive**, upload to TestFlight or App Store Connect, or deploy the backend your app talks to. Copy it into your release PR, or bookmark it.

Items marked **⚡ SHIPSAFE** are checked automatically by [SHIPSAFE](https://apps.apple.com/us/app/shipsafe-release-readiness/id6808833747?mt=12), with the file, the line and the fix. The rest are worth a manual look.

---

## 1. Secrets and keys

Anything compiled into your `.ipa` or `.app` can be extracted by anyone who downloads it. `strings` is enough.

- [ ] No API keys hardcoded in Swift files, `Info.plist`, `.xcconfig`, or JSON config. **⚡ SHIPSAFE** (OpenAI, Stripe live, AWS, GitHub, Google, Slack, private keys)
- [ ] No `.env`, `credentials.json` or `service-account.json` committed to the repo. **⚡ SHIPSAFE**
- [ ] Paid third-party APIs (OpenAI, Stripe secret, etc.) are called from **your server**, not from the app. The app holds no secret key.
- [ ] `GoogleService-Info.plist` keys are restricted to your bundle ID in the Google Cloud console. They are not secret, but unrestricted keys get abused.
- [ ] Any key that was ever committed has been **rotated**, not just deleted. Git history keeps it.

## 2. Leftovers from development

- [ ] No `console.log`, `debugger`, `var_dump` or other debug hooks left in backend and web code. **⚡ SHIPSAFE**
- [ ] No Swift `print` / `NSLog` that dumps tokens, user data or full responses. Use `Logger` with `privacy: .private`.
- [ ] No `TODO` / `FIXME` left on code paths that matter for this release. **⚡ SHIPSAFE**
- [ ] No debug flags, dev-only endpoints, or `DEBUG = true` in production config. **⚡ SHIPSAFE**
- [ ] Staging and localhost base URLs are behind `#if DEBUG`, never in Release builds.
- [ ] Test accounts, test buttons and "skip paywall" shortcuts are removed or compiled out.

## 3. App Store and App Review basics

- [ ] `PrivacyInfo.xcprivacy` is present and declares the required-reason APIs you and your SDKs use.
- [ ] App Transport Security has no blanket `NSAllowsArbitraryLoads` unless you can justify it.
- [ ] Entitlements match what the app actually does. Unused capabilities invite rejection.
- [ ] Every permission prompt (`NS…UsageDescription`) says clearly why you need it.
- [ ] The demo account and review notes for App Review are current and work.
- [ ] The Support URL and Privacy Policy URL load and are up to date.

## 4. Your backend

Most apps ship with a server, a dashboard, a webhook endpoint or cloud functions. That is where breaches usually start.

- [ ] Every admin and data-changing route checks authentication and authorization. **⚡ SHIPSAFE** (attack-surface map)
- [ ] Error responses don't leak stack traces or internal details in production. **⚡ SHIPSAFE**
- [ ] Production config is production: debug mode off, secure cookies, sane CORS. **⚡ SHIPSAFE**
- [ ] User input is validated before it reaches the database or a shell. **⚡ SHIPSAFE**
- [ ] Rate limits exist on login, signup, password reset and anything that costs you money per call.

## 5. Dependencies

- [ ] Every package manifest has a committed lockfile. **⚡ SHIPSAFE**
- [ ] No wildcard, `latest`, or git-branch version specs in production dependencies. **⚡ SHIPSAFE**
- [ ] Swift packages are pinned to a version or exact revision you have reviewed.

## 6. Database

- [ ] Migrations in this release contain no unguarded `DROP`, `TRUNCATE` or mass `DELETE`. **⚡ SHIPSAFE**
- [ ] You have a tested backup from before the migration runs.

## 7. Before you press the button

- [ ] Run a full release check and keep the report with the release. **⚡ SHIPSAFE** (PDF / HTML export)
- [ ] Compare against the previous release: did anything new appear? **⚡ SHIPSAFE** (scan history)

---

### Run most of this list in one click

SHIPSAFE scans your project folder locally on your Mac and turns the ⚡ items above into a scored, evidence-backed report. No account, no upload, no AI calls.

[![Download on the Mac App Store](https://img.shields.io/badge/Mac_App_Store-Download-0D96F6?style=for-the-badge&logo=apple&logoColor=white)](https://apps.apple.com/us/app/shipsafe-release-readiness/id6808833747?mt=12)

Something missing from this list? [Open an issue](https://github.com/ilyasaalmadani/shipsafe-macos/issues/new/choose). Good suggestions get added here, and often become new SHIPSAFE checks.
