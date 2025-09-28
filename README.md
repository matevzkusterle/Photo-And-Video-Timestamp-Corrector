# 🗂️ Media Date Fixer

This repository contains a **Python script** for repairing and standardizing **timestamps of photos and videos** in archival collections. It is specifically designed for folders of mixed images and videos (JPG/JPEG, PNG, MP4) where original metadata may be missing, incorrect, or inconsistent with the folder structure.

---

## 📌 What It Does
The script performs **automated date correction** by applying a hierarchical set of rules:

1. **Folder-Level Priority**
   - If `date.txt` is present → all files adopt that exact date.  
   - Otherwise, the script extracts a year from the folder name (2000–2030).  
   - If no year is found → it processes files without enforcing a year.  

2. **Photos (JPG/JPEG/PNG)**
   - Reads `Date Taken` from EXIF (JPG) or metadata (PNG).  
   - If the year matches the folder → aligns only filesystem timestamps.  
   - If missing or mismatched → attempts to reuse a valid date from another photo in the folder with the correct year.  
   - If none exists → defaults to **15 June [folder year]**.  
   - If no folder year → aligns with available EXIF or another photo in the same folder.  

3. **Videos (MP4)**
   - Reads `Media Created` using ExifTool.  
   - If the year matches the folder → synchronizes **all internal video dates and filesystem timestamps**.  
   - If missing or mismatched → attempts to reuse a valid date from another video in the same folder with the correct year.  
   - If none exists → defaults to **15 June [folder year]**.  
   - If no folder year → aligns with existing metadata or another video in the folder.  

4. **Special Handling**
   - **Corrupt files** are logged but left untouched.  
   - **Non-media files** (TXT, DOC, etc.) are skipped automatically.  

---

## ✅ When To Use This Script
This script is particularly useful in the following scenarios:

- **Digital photo/video archives** with inconsistent or missing capture dates.  
- **Large family or institutional collections** where folder names indicate years but files themselves are unreliable.  
- **Migrated archives** (e.g., from old phones, cameras, or disks) where filesystem timestamps no longer reflect actual creation dates.  
- **Pre-backup cleanup** to ensure uniform and reliable date metadata before transferring to cloud storage or long-term archival systems.  

---

## ⚙️ Requirements
- **Windows OS** (uses `pywin32` for filesystem timestamp updates).  
- **ExifTool** (installed and accessible at the configured path).  
- **Python 3.8+** with the following libraries:
  - `Pillow`
  - `piexif`
  - `pywin32`

---

## 🚀 Usage
1. Clone this repository or download the script.  
2. Place your archival folders inside the root directory, e.g.:  

   ```
   Arhiv slik/
   ├── 2005 Holidays/
   ├── 2010 Family Trip/
   ├── 2020 Wedding/
   ```

3. Optionally add `date.txt` inside any folder if you want to enforce a precise date:  

   ```
   Sunday, 18 August 2024
   ```

4. Run the script:

   ```bash
   python fix_dates.py
   ```

5. The script will:
   - Process each folder.  
   - Adjust EXIF/video metadata where applicable.  
   - Synchronize filesystem creation/modified dates.  
   - Log any problematic files.  

---

## 📖 Example

Suppose you have a folder:

```
2015 Summer/
├── IMG_001.jpg   (missing EXIF)
├── IMG_002.jpg   (Date Taken: 2014-07-10)
├── VID_001.mp4   (Media Created: missing)
```

**Before running the script:**  
- `IMG_001.jpg` → No date.  
- `IMG_002.jpg` → Wrong year (2014, should be 2015).  
- `VID_001.mp4` → No metadata date.  

**After running the script:**  
- `IMG_001.jpg` → Inherits **15 June 2015**.  
- `IMG_002.jpg` → Corrected to **15 June 2015**.  
- `VID_001.mp4` → Uses the valid 2015 date from `IMG_001.jpg` or falls back to **15 June 2015**.  

---

## ⚠️ Notes & Limitations
- **Windows only** (due to direct filesystem date manipulation with `pywin32`).  
- EXIF updates are limited to **JPG/JPEG**; PNG metadata is not rewritten.  
- Always **back up your files** before running batch operations.  

---

## 📜 License
This project is released under the MIT License. See [LICENSE](LICENSE) for details.  
