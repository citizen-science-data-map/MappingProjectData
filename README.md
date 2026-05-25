# WAI Wanaka Data Uploader

Local staff tool for converting Excel datasets to GeoJSON and syncing updates to GitHub.

## What this app does

1. Upload or clear environmental datasets (including GYFW).
2. Convert Excel data to GeoJSON using existing Python conversion logic.
3. Sync GeoJSON files to GitHub via API (no local `git` commands required).
4. Open the map with repository/commit parameters for direct verification.

## Current architecture

1. **Upload page**: `http://127.0.0.1:5000/`
2. **Sync settings page**: `http://127.0.0.1:5000/settings`
3. **Map page**: `http://127.0.0.1:5000/map`
4. **GeoJSON output**: `Data/geoJSONs/*.geojson`
5. **GitHub sync method**: GitHub Contents API (`PUT /repos/{owner}/{repo}/contents/{path}`)

## Requirements

1. Windows machine.
2. Internet access to GitHub.
3. GitHub Personal Access Token (PAT) with:
   - Repository access to target repository.
   - `Contents: Read and write`.
4. For source run only:
   - Python 3.11+
   - Dependencies in `requirements.txt`

## Run: packaged EXE

1. Start:
   
   WaiWanakaUploader.exe`
2. Keep the full folder together:`
3. Open browser:
   - `http://127.0.0.1:5000/`

Windows dedicated guide:

- `README_WINDOWS.md`

## Build macOS app bundle

macOS package cannot be built on Windows. Build on a Mac using:

1. `chmod +x scripts/build_macos.sh`
2. `./scripts/build_macos.sh`

Output:

1. `dist/WaiWanakaUploader.app`
2. `dist/WaiWanakaUploader-mac-YYYYMMDD-HHMM.zip`

Detailed steps:

- `README_MAC_BUILD.md`

## First-time setup (For this step, I have already saved, so you don't need to worry.)

1. Go to `http://127.0.0.1:5000/settings`.
2. Fill:
   - `GitHub owner`
   - `Repository name`
   - `Branch` (usually `main`)
   - `Path prefix` (optional)
   - `GitHub token (PAT)`
3. Optional: check **Save token locally on this computer** (trusted devices only).
4. Click **Save GitHub Settings**.

Saved settings file:

- `C:\wai_project\github_sync_config.json`

## Staff workflow

1. Open upload page: `http://127.0.0.1:5000/`
2. Choose action:
   - `Upload and convert data`
   - `Clear selected dataset GeoJSON`
3. Select dataset (`All datasets` or single dataset).
4. Keep **Auto sync updated GeoJSON to GitHub** enabled.
5. Submit.
6. Check run log for:
   - `Synced to GitHub: ...`
   - `GitHub commit: <sha>`
7. Click **Open map** and verify data.

## Data flow

1. Staff uploads Excel.
2. Backend saves file to `uploads/`.
3. Converter processes selected dataset(s).
4. GeoJSON written to `Data/geoJSONs/`.
5. App syncs GeoJSON to GitHub repository.
6. Map reads GitHub-hosted GeoJSON and displays updated points.

## Troubleshooting

1. `GitHub sync failed: owner/repo/token are required.`
   - Save settings again in `/settings`.

2. `403 Resource not accessible by personal access token`
   - Token is missing write access.
   - Recreate/update PAT with `Contents: Read and write`.

3. Upload works locally but map does not update
   - Confirm `GitHub commit: ...` appears in run log.
   - Re-open map from app and refresh.

4. App opens but no page loads
   - Confirm process is running.
   - Check `http://127.0.0.1:5000/` directly.

## Security notes

1. Do not save PAT on shared/public computers.
2. Revoke PAT immediately if compromised.
3. Prefer a dedicated organization/service account for data publishing.
