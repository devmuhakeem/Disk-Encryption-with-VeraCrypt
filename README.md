# Disk Encryption with VeraCrypt

A hands-on lab building an encrypted volume with VeraCrypt — creating a file-based encrypted container, mounting it as a virtual drive, copying a file into it, and dismounting it to confirm the entire volume (including file names and structure) becomes inaccessible without the password.

## Scenario
Full disk/volume encryption protects more than file contents — done properly, it hides file names, folder structure, free space, and metadata too. This lab built an encrypted container with VeraCrypt and verified that behavior directly, by mounting it, storing a file, then dismounting and confirming nothing remained visible.

## What I did

### 1. Created an encrypted volume with the VeraCrypt wizard
- Selected **Create an encrypted file container** (a container file, not a full physical disk)
- Volume location: saved as `My Volume` on the desktop
- Volume size: 5 MB (small, for demonstration)
- Password: a strong, volume-specific password (separate from any system login)
- Filesystem: FAT, default cluster size
- Moved the mouse randomly for 30+ seconds during the Random Pool / Header Key / Master Key generation step — a genuine entropy source for the encryption keys, not a cosmetic step
- Clicked Format — VeraCrypt produced the `My Volume` container file

### 2. Mounted the volume and tested it
- In VeraCrypt's main window: selected drive letter `I:`, pointed it at `My Volume`, clicked Mount
- Entered the volume password — `I:` appeared in Windows as a normal, browsable drive
- Created a test text file, wrote content into it, and copied it directly into the mounted `I:` drive — the copy operation behaved identically to copying to any normal folder

### 3. Dismounted and confirmed the security property
- Clicked **Dismount** in VeraCrypt — the `I:` drive disappeared entirely from "This PC"
- Only the original `My Volume` file remained on the desktop, with no visible indication of its contents, file names, or structure

## Key takeaways
- Full disk/volume encryption covers the entire filesystem (file names, folder structure, free space, metadata) — not just file contents the way encrypting individual files does
- Hiding metadata is a different, stronger security property than hiding content alone — an attacker with access to a dismounted volume can't even confirm what, if anything, is stored inside
- The mouse-movement entropy step is genuinely functional, not cosmetic — true randomness is hard for a computer to generate alone, and weak entropy undermines strong-looking encryption
- Password strength is the real determining factor in whether the volume resists an offline cracking attempt — the same lesson as WPA2: sound cryptography, but the password does the actual work
- A mounted encrypted volume behaving exactly like a normal drive (not requiring special handling to use) is what makes encryption something people will actually use consistently rather than work around

## Tools
VeraCrypt

---
*Completed in an isolated training lab environment on a provisioned Windows VM.*
