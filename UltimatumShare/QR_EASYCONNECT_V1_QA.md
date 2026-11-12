# Ultimatum QR Easy Connect V1 — QA protocol

**Status: QA ONLY (2026-11-12), not publicly released.**

Android candidate: `2.0.16` / `versionCode 27`, `com.ultimatum.flashshare`. Windows Companion QA build contains **Pair by QR · Easy**. Existing public Windows release `windows-companion-v1.0.0` is unchanged.

## Real-device flow
1. Connect Android and Windows to the same **trusted** private LAN.
2. Windows QA Companion → **Pair by QR · Easy**; select the correct private IPv4. The QR expires after 2 minutes.
3. On Android, use the bright green home action **WINDOWS PC · CONNECT / SCAN QR** → **SCAN WINDOWS QR · CONNECT**.
4. Look near the **top of PC Connect** for the pending computer. Tap **APPROVE & CONNECT**. Scanning alone must **not** grant access.
5. Confirm Windows says Connected; send and receive small files in both directions. Compare actual files.
6. Test **Deny**, expired QR, invalid QR, firewall restriction, multiple network cards, hotspot, and fallback **Find phone / Use copied link**.
7. Confirm no regressions in Pro gating, history, existing devices or background transfer.

## Release gates
- Android APK and AAB must be signed by the **existing original upload certificate**. No new keystore and no app-data wipe.
- Confirm code 27 is **not already used in Google Play** before AAB upload.
- Windows installer Authenticode currently `NotSigned`; do not misstate publisher signing.
- **Security caveat:** Current local HTTP and QR LAN handoff have **no transport encryption**. The QR contains a temporary desktop IP, port and nonce, while Android sends the session credential over the private LAN; use trusted LAN only. Android Phone Approval remains mandatory.
- **Do not publish** a new GitHub installer, change the website verified download checksum, or tell users that QR works until real-device QA PASS.
- After QA PASS: publish versioned Windows GitHub Release with verified installer hash, update **both** official Windows download pages and add **real** screenshot instructions, upload Play AAB, then inform users.

Never commit private source configuration, passwords, upload keystore or any security token.