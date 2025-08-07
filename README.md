# Fix Media Dates

This script fixes incorrect "Created" and "Modified" dates for photos and videos in your media archive. It goes through all folders and updates file dates based on the most reliable source available.

## 🔧 What It Does

For every folder inside `Arhiv slik`, it checks each photo and video file and updates the following:

- **Photos**: Uses **"Date Taken"** from EXIF data.
- **Videos**: Uses **"Media Created"** timestamp.
- **Filesystem Dates**: Updates "Created" and "Modified" dates to match the correct date.

If the correct date is missing or doesn’t match the folder year, it uses fallback rules to set a reasonable date.

## 📁 Folder Rules

Each folder name may contain a year (like `Photos 2020`). That year is used to verify or correct the dates of files inside the folder.

### 1. If there is a `date.txt` file in the folder:
- Its date (like `Sunday, 18 August 2024`) is used for all photos and videos in that folder.
- It also updates:
  - "Date Taken" (photos)
  - "Media Created" (videos)
  - Filesystem "Created" and "Modified" dates

### 2. If there's no `date.txt`:
- Photos get their date from EXIF **"Date Taken"**
- Videos get their date from **"Media Created"**

### 3. If the file's year doesn’t match the folder year:
- All dates (EXIF, Media Created, Created, Modified) are set to **June 15** of the folder's year.

### 4. If the file has no metadata at all:
- Uses the folder year and sets dates to **June 15** of that year.

## ✅ Other Rules

- Only processes `.jpg`, `.jpeg`, and `.mp4` files
- Skips other files (like PDFs, RAW, etc.)
- Processes files alphabetically
- Does **not** space files over multiple days
- Does **not** move or delete any files
- Tries to fix broken EXIF without moving files to a "corrupt" folder

## 📌 Requirements

- **Windows only** (uses Windows-specific APIs)
- Python packages needed:
  - `pywin32`
  - `Pillow`
  - `piexif`

Install with:

```bash
pip install pywin32 Pillow piexif
