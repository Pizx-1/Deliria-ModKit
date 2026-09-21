# Deliria Modding — Setup Guide

## Initial Setup

1. **Own and have Deliria installed.**
   You'll need roughly **30 GB** of free disk space (custom engine + intermediate build files).

2. **Link your Epic Games and GitHub accounts.**
   If you haven't done so already, [follow these instructions on linking your Epic Games and GitHub accounts.](https://www.epicgames.com/help/account-c-45487929/linked-accounts-c-38854402/how-do-i-link-my-unreal-engine-account-with-my-github-account-a13858315). If you don't do this, the below custom engine link will return a 404 not found.
   
4. **Install the custom UE5.6 engine build.**
   - Install close to the drive root (long paths can break the build)
   - Avoid spaces anywhere in the install path
   - Use an SSD/NVMe, not an HDD

5. **Install Visual Studio 2022** with the **MSVC v14.38 toolchain** selected — required to open the project at all.

6. **Clone (don't zip-download) the `DeliriaModKit` repo.**
   Cloning via git makes it easy to pull future updates; a zip download doesn't.

7. **Set your game install path.**
   Open `GameInstallDirectory.txt` and paste in your Deliria install path — the folder containing `Deliria-Win64-Shipping.exe`.

8. **Switch the engine version.**
   Right-click `Deliria.uproject` → **Switch Unreal Engine version**, and point it at the folder containing the custom engine's `Engine` folder.

9. **Open `Deliria.uproject`.**
   First launch compiles a few plugins — expect 2–10 minutes depending on your hardware.

10. **Confirm content is visible in the Content Browser.**
   Everything here is **read-only** — the editor may let you edit values, but nothing saves back to the cooked package.

   > See [Exporting Content for Mods] for how to get an editable, uncooked copy of assets.

---

## Regenerating After a Game Update

Whenever Deliria updates, your mod kit needs to be regenerated against the new game version:

1. **Run `update.bat`** in the Automation folder.
   This regenerates the `.jmap`, `.usmap`, headers, and asset registry in one pass.

2. **Check the script's Steam path if it fails.**
   `update.bat` looks for Steam at a default location (`C:\Program Files (x86)\Steam\...`). If your Steam library is installed elsewhere, update the path in the script before assuming something else is wrong.

3. **If the editor fails to launch afterward** (for example, a shader-related access violation), do a full wipe of:
   - `Saved/`
   - `Intermediate/`
   - `DerivedDataCache/`

   then try opening the project again. This clears out stale cache state, which is a common cause of post-update launch failures.

4. **If problems persist, do a fresh checkout of the project** rather than continuing to debug a possibly-corrupted copy.
