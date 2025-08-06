README - Photo & Video Timestamp Corrector
==========================================

Python Version: 3.10+

------------------------------------------
📌 OVERVIEW
------------------------------------------

This Python script scans a photo/video archive located in my local folder:

    c:\Users\kuste\Desktop\project\Arhiv slik

It automatically fixes incorrect **"Created"**, **"Modified"**, and **"Date Taken"** metadata for photos and videos.

Use this when your photos and videos are out of order due to wrong file system dates, especially after copying files between devices.

------------------------------------------
🎯 WHAT IT DOES
------------------------------------------

For each folder inside `Arhiv slik`, the script:

1. ✅ Reads a date from `date.txt` (if it exists).
2. ✅ Updates all `.jpg`, `.jpeg` photos:
     - Sets EXIF "Date Taken"
     - Sets "Created" and "Modified" file times
3. ✅ Updates all `.mp4` videos:
     - Sets "Created" and "Modified" file times
4. ✅ If `date.txt` is missing:
     - Tries to read actual metadata from photos/videos
     - If nothing found, tries to extract a year from the folder name (2000–2030)
5. ✅ Leaves all other files untouched

------------------------------------------
📁 INPUT FORMAT
------------------------------------------

Each folder may contain:

- Photos: `.jpg`, `.jpeg`
- Videos: `.mp4`
- Optional: `date.txt` file, in this format:

    Sunday, ‎18 ‎August ‎2024

Note: The script removes invisible characters from the `date.txt` line automatically.

------------------------------------------
🔧 REQUIREMENTS
------------------------------------------

Install required Python packages before running:

    pip install pillow pywin32 piexif hachoir

Packages used:
- `pillow` – for reading EXIF from images
- `piexif` – for modifying image EXIF data
- `pywin32` – for setting Windows file timestamps
- `hachoir` – for reading "media created" from `.mp4` files

------------------------------------------
▶️ HOW TO RUN
------------------------------------------

1. Place the script in your project folder.

2. Open a terminal and run:

    python fix_timestamps.py

3. The script will scan all folders inside:

    c:\Users\kuste\Desktop\project\Arhiv slik

4. Progress will be printed to the console for each folder and file.

------------------------------------------
⚠️ NOTES
------------------------------------------

- Only `.jpg`, `.jpeg`, and `.mp4` files are modified.
- Other files (e.g. `.png`, `.pdf`, `.docx`) are ignored.
- "Date Taken" is only editable for JPEG images, not PNG or HEIC.
- "Media Created" inside videos is not modified (only filesystem timestamps).
- Always back up your archive before running bulk metadata updates.

------------------------------------------
✅ STATUS
------------------------------------------

✔ Fully working
✔ Supports nested folders
✔ Uses multiple fallback methods for missing dates
✔ Tested on Windows 11


