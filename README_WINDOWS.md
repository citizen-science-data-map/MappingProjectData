# WAI Wanaka Windows Guide

This file is the Windows-specific guide for deployment, updates, and troubleshooting of the EXE version.

## 1. Requirements

1. Windows 10/11 (64-bit)
2. Internet access to GitHub (for GeoJSON sync)
3. GitHub PAT with `Contents: Read and write`

## 2. How to run

### Run packaged EXE

1. Start:
   - `WaiWanakaUploader.exe`
2. Keep the whole folder together:
3. Open in browser:
   - `http://127.0.0.1:5000/`



## 3. First-time GitHub setup)( For this step, I have already saved, so you don't need to worry.)

Open:
- `http://127.0.0.1:5000/settings`

Fill in:
1. `GitHub owner`
2. `Repository name`
3. `Branch` (usually `main`)
4. `Path prefix` (usually empty)
5. `GitHub token (PAT)`

Save settings, then return to the upload page.

## 4. Daily upload workflow

1. Open `http://127.0.0.1:5000/`
2. Select an Excel file (`.xlsx`)
3. Select dataset scope (`All datasets` or a single dataset like GYFW)
4. Click **Upload and Convert**
5. Confirm success messages in the run log
6. Click **Open map** and verify map data

## 5. Common issues

1. `401 Bad credentials`
   - PAT is invalid or lacks permission. Generate a new PAT and save again.
2. Map does not update
   - Check upload log for `GitHub commit` / `Synced to GitHub`.
3. EXE starts but page is unreachable
   - Check port conflicts and test directly with `http://127.0.0.1:5000/`.

## 6. Release recommendations

1. Distribute the full `dist\WaiWanakaUploader\` folder as a zip.
2. Do not distribute only `WaiWanakaUploader.exe`.
3. Do not persist PAT on shared/public computers.
