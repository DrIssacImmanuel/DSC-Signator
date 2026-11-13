# DSC Signator — Bulk PDF Digital Signature Tool

A Windows desktop app that signs every PDF in a folder with a USB DSC (Digital Signature Certificate) token. It runs as a single `.exe`, so the PC needs no Python.

---

## ⬇️ Download

**[Download BulkPDFDSCSigner.exe → Latest Release](https://github.com/DrIssacImmanuel/DSC-Signator/releases/latest/download/BulkPDFDSCSigner.exe)**

---

## How to use

1. Plug in the DSC token.
2. Run `BulkPDFDSCSigner.exe`. A file picker opens.
3. Select any PDF. The app lists every PDF in that folder. Tick **Include sub-folders** if you want those too.
4. Check the certificate under **Signature**. If the token was plugged in after the app started, click **Refresh**.
5. Click **Sign**. The token driver asks for the PIN, the same prompt you get in Adobe Acrobat.
6. Watch the **Status** column. Each file shows Signed, a skip reason, or an error.

The signed copy replaces the original file. Keep a backup if you need the unsigned version.

---

## What it does

- Puts a visible signature on page 1, in the top-right corner, 24 points in from the edges.
- The stamp reads "Digitally signed by <name on the certificate>" with the date and time of the PC.
- Works on rotated and cropped pages. The stamp stays upright in the visible top-right corner.
- Skips a PDF that already has a signature from the same certificate, so running it twice does not stamp twice.
- Skips password-protected and unreadable PDFs and says why.
- Asks for the PIN once, before it touches any file. If the PIN is wrong or you cancel, nothing changes and the app stops, so a bad PIN cannot be tried again on every file.
- Writes each signed file to a temporary copy first, then swaps it in. A failure halfway through a file leaves the original intact.

---

## How it finds the token

The app reads the certificate from the Windows certificate store, which is where the token driver (for example PROXKey) publishes it when the token is plugged in. Windows and the driver do the signing. This is the route Adobe Acrobat takes, so if Acrobat can sign with the token on that PC, this app should be able to as well.

If the certificate does not appear in the list, tick **My certificate is not in the list. Use the token driver (PKCS#11).** Then give the path to the driver DLL (for PROXKey, `C:\Windows\System32\Watchdata\PROXKey CSP India V3.0\WDPKCS.dll`) and type the PIN in the app.

---

## Requirements

- Windows 10 or 11, 64-bit
- A USB DSC token with its driver installed

---

## Tech stack

Built with Python, pyHanko, python-pkcs11, asn1crypto and Tkinter.
