# codeike-github
## https://github.com/codeike27-afk/codeike-github.git
这是
`png.py`
的内容
```python
#!/usr/bin/env python3
# -*- coding : utf-8 -*-

import os

# PNG file signature header (first 8 bytes of valid PNG)
PNG_MAGIC_BYTES = b"\x89PNG\r\n\x1a\n"

def is_png_by_signature(file_path: str) -> bool:
    """Check if a file is a PNG by reading its header bytes, ignore extension"""
    try:
        with open(file_path, "rb") as f:
            header = f.read(8)
            return header == PNG_MAGIC_BYTES
    except (PermissionError, IsADirectoryError, OSError):
        # Skip unreadable files/folders
        return False

def scan_folder_for_png(root_directory: str) -> list[str]:
    """Recursively scan directory, return list of all PNG file full paths"""
    found_png_files = []
    
    # Walk through all subfolders and files
    for dirpath, _, filenames in os.walk(root_directory):
        for filename in filenames:
            full_file_path = os.path.abspath(os.path.join(dirpath, filename))
            if is_png_by_signature(full_file_path):
                found_png_files.append(full_file_path)
                print(f"Found PNG: {full_file_path}")
    return found_png_files

def save_paths_to_txt(file_path_list: list[str], output_txt: str = "png_file_list.txt"):
    """Write all found PNG paths to a text file"""
    with open(output_txt, "w", encoding="utf-8") as out_file:
        for path in file_path_list:
            out_file.write(path + "\n")
    print(f"\nScan complete! Total PNG files found: {len(file_path_list)}")
    print(f"Path list saved to: {os.path.abspath(output_txt)}")

if __name__ == "__main__":
    # -------------------------- CONFIG --------------------------
    # Replace this with your target folder to scan (Windows format)
    # Example: r"C:\Users\YourName\Pictures" or r"D:\Media\Files"
    SCAN_TARGET_FOLDER = r"C:\Users\Public\Pictures"
    # ------------------------------------------------------------

    # Run scan
    png_path_list = scan_folder_for_png(SCAN_TARGET_FOLDER)
    
    # Save list to text file
    save_paths_to_txt(png_path_list)
```
