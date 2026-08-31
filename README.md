# DSC Signator — Bulk PDF Digital Signature Tool

A Windows desktop app to digitally sign multiple PDF files in bulk using a USB DSC (Digital Signature Certificate) token. No Python installation required.

---

## ⬇️ Download

**[Download BulkPDFDSCSigner.exe → Latest Release](https://github.com/DrIssacImmanuel/DSC-Signator/releases/latest/download/BulkPDFDSCSigner.exe)**

---

## How to Use

1. **Run** `BulkPDFDSCSigner.exe` — fully portable, no installation needed
2. **Screen 1 — Select Folders**: Browse and add one or more folders containing PDFs to sign (sub-folders are included automatically)
3. **Screen 2 — Authenticate**: Insert your USB DSC token and enter your PIN
4. **Screen 3 — Progress**: Watch live file-by-file progress — app closes automatically after 15 seconds on success

---

## Requirements

- Windows 10 / 11 (64-bit)
- A USB DSC token with its PKCS#11 driver installed (provided by your token manufacturer)

---

## What It Does

- Recursively finds all PDF files in selected folders
- Places a digital signature stamp (bottom-right corner, Page 1) with your certificate name and IST timestamp
- Signs files **in-place** using PKCS#7 detached signature format (Adobe-compatible)
- Reads signer name directly from the certificate on the token

---

## Tech Stack

Built with Python · pyHanko · python-pkcs11 · cryptography · pypdf · Tkinter  
Packaged as a standalone Windows executable via PyInstaller
