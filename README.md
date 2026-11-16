# DSC Signator — Bulk PDF Digital Signature Tool

A Windows desktop app that signs every PDF in a folder with a USB DSC (Digital Signature Certificate) token. It runs as a single `.exe`, so the PC needs no Python.

---

## ⬇️ Download

**[Download BulkPDFDSCSigner.exe → Latest Release](https://github.com/DrIssacImmanuel/DSC-Signator/releases/latest/download/BulkPDFDSCSigner.exe)**

---

## How to use

The app has three panels. A folder picker opens when it starts.

1. **Folders.** Pick the folder that holds the PDFs. The app lists every PDF in it and in its sub-folders. If it finds PDFs two or more levels down, a notice names those folders and lets you exclude them.
2. **Signature.** Check the certificate, and choose which corner of page 1 gets the stamp (top right by default). If the token was plugged in after the app started, click **Refresh**.
3. **Sign.** The token driver asks for the PIN in its own prompt, the same one you get in Adobe Acrobat. Then the app signs the files and shows the result for each one. When it finishes, **Open folder and close** opens the folder and quits.

The signed copy replaces the original file. Keep a backup if you need the unsigned version.

The moon button at the top right switches to a dark theme. The app remembers your choice.

---

## The stamp

- Page 1, in the corner you chose. The stamp and its margins scale with the page, so it looks the same on A4, on large scans and on small scans. The top margin equals the side margin.
- It shows the name on the certificate in large type, then "Digitally signed by …" with the date and time of the signature, inside a thin border with a pale green tick behind the text.
- On rotated scans the stamp stays upright in the corner you see on screen.

---

## Safety

- The token checks the PIN once, before any file is touched. A wrong or cancelled PIN stops the run and nothing changes, so a bad PIN is never retried on every file.
- A PDF that already has a signature from the same certificate is skipped, so running the app twice does not stamp twice.
- Password-protected and unreadable PDFs are skipped, and the app says why.
- Each file is written to a temporary copy first, then swapped in. A failure halfway through a file leaves the original intact.

---

## How it finds the token

The app reads the certificate from the Windows certificate store, where the token driver (for example PROXKey) publishes it when the token is plugged in. Windows and the driver do the signing. Adobe Acrobat works the same way, so if Acrobat can sign with the token on that PC, this app should too.

If the certificate does not appear, click **Use the token driver** on the Signature panel. Give the path to the driver DLL (for PROXKey, `C:\Windows\System32\Watchdata\PROXKey CSP India V3.0\WDPKCS.dll`) and type the PIN.

---

## Requirements

- Windows 10 or 11, 64-bit
- A USB DSC token with its driver installed
- The Microsoft Edge WebView2 runtime for the glass window. Windows 11 includes it. Without it, the app opens a plainer classic window that does the same job.

---

## Tech stack

Built with Python, pyHanko, pywebview, python-pkcs11, asn1crypto and Tkinter.
