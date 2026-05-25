# Build macOS version

## 1. Prepare source on Mac

1. Copy this repository to your Mac.
2. Open Terminal and go to project folder.

## 2. Run one-command build

```bash
chmod +x scripts/build_macos.sh
./scripts/build_macos.sh
```

## 3. Build output

After successful build:

1. App bundle:
   - `dist/WaiWanakaUploader.app`
2. Release zip:
   - `dist/WaiWanakaUploader-mac-YYYYMMDD-HHMM.zip`

## 4. Notes

1. If Gatekeeper blocks the app, right-click app and choose **Open** once.
2. For distribution outside your own devices, add Apple code signing + notarization in a separate step.

## 5. Build with GitHub Actions

You can build `.app` directly in GitHub:

1. Open repository **Actions** tab.
2. Run workflow: **Build macOS App**.
3. After run completes, download artifact:
   - `WaiWanakaUploader.app`
   - `WaiWanakaUploader-mac-<run>-<sha>.zip`

This workflow uploads artifacts only. It does not commit binaries into the repository.
