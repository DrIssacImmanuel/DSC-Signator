# How to use DSC Signator

This guide takes you from the download to a folder of signed PDFs. It takes about five minutes the first time.

## Before you start

- A Windows 10 or Windows 11 PC.
- Your USB DSC token, with its driver installed. If you can already sign in Adobe Acrobat on this PC, the driver is fine.
- A copy of the PDFs. The app replaces each file with its signed version, so try it on a copy of a small folder first.

## 1. Download

1. Open the [latest release](https://github.com/DrIssacImmanuel/DSC-Signator/releases/latest).
2. Under **Assets**, click **BulkPDFDSCSigner.exe**. Or use the [direct download link](https://github.com/DrIssacImmanuel/DSC-Signator/releases/latest/download/BulkPDFDSCSigner.exe).
3. The file lands in your **Downloads** folder. It is about 44 MB.

Your browser may say the file "isn't commonly downloaded". In Edge, open the three-dot menu next to the download, choose **Keep**, then **Show more** and **Keep anyway**. In Chrome, choose **Keep**.

There is nothing to install. The `.exe` is the whole app. You can move it to the Desktop or any folder you like.

## 2. Get past SmartScreen

The first time you double-click the file, Windows shows a blue box that says **Windows protected your PC**.

1. Click **More info**. It is a small link under the text.
2. Check that the app name is `BulkPDFDSCSigner.exe`.
3. Click **Run anyway**.

Windows shows this box because the file has no paid code-signing certificate, so Microsoft does not know the publisher yet. It does not mean Windows found anything wrong. You only see it the first time.

If there is no **Run anyway** button, your office PC blocks unknown apps. Ask your IT administrator to allow the file.

## 3. Pick the folder

Plug in the token before you go on.

1. The app opens with a folder picker. Choose the folder that holds your PDFs and click **Select Folder**.
2. The **Folders** panel lists every PDF it found, including the ones in sub-folders.
3. If some PDFs sit two or more folders deep, a notice names those folders. Click **Exclude** if you do not want them signed.
4. Click **Continue**.

## 4. Choose the signature

1. The **Signature** panel shows the certificate on your token, with the name, the issuer and the expiry date. Click it to select it.
2. If no certificate shows, check the token is plugged in and click **Refresh**.
3. Pick the corner of page 1 for the stamp. Top right is the default.
4. Click the **Sign** button. It shows how many PDFs it will sign.

## 5. Enter the PIN

Your token's own PIN box opens, the same one you see in Adobe Acrobat. Type the PIN there and confirm.

The PIN is checked once, before any file is touched. If the PIN is wrong or you cancel, the app stops and no file changes. It does not retry the PIN on each file, so one mistake costs one attempt and does not block the token.

## 6. Let it run

The **Sign** panel shows each file as it is signed. Leave the token plugged in until it finishes.

Each file ends with one of these:

- **Signed**: done.
- **Skipped**: the file already has your signature, is password-protected, or cannot be read. The app says which.
- **Failed**: something went wrong with that one file. The original is left as it was.

When the run ends, click **Open folder and close**. The folder opens and the app quits.

## 7. Check a file

Open one signed PDF in Adobe Acrobat Reader. Page 1 has a stamp with your name and the date and time. Click the stamp, or open the Signatures panel, to see the signature details.

If Acrobat says the signer's identity is unknown, Acrobat does not trust your certificate authority yet. That is an Acrobat setting on the PC of whoever opens the file. The signature itself is still intact.

## If something goes wrong

**No certificate found.** Unplug the token, plug it in again, wait ten seconds and click **Refresh**. If it still does not show, click **Use the token driver** on the Signature panel, give the path to your token's driver DLL (for PROXKey: `C:\Windows\System32\Watchdata\PROXKey CSP India V3.0\WDPKCS.dll`) and type the PIN in the box there.

**"The token PIN is wrong."** Nothing was signed. Click Sign and try again, carefully. Most tokens block after a few wrong PINs in a row.

**"The token is blocked."** Too many wrong PINs. Use your token's own admin tool or contact the company that issued the DSC to unblock it.

**The window looks plain, not glassy.** The PC does not have the Microsoft Edge WebView2 runtime, so the app opened its classic window. It signs the same way. Windows 11 includes WebView2, and on Windows 10 you can install it from Microsoft.

**A file was signed twice.** It should not happen. The app skips any PDF that already carries a signature from the same certificate.

## Privacy

The app works only on your PC. It does not connect to the internet, and it never sees your PIN, because the token's driver asks for it. Your private key stays on the token.
