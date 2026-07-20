# Modding Difficulty

## PAK File Naming

When adding modded PAK files, they must follow the naming convention below:

- Prefix: `res`
- Suffix: `.pak`
- Format: `res.pak`, `res1.pak`, `res2.pak`, `res3.pak`, ...

The numbering must be **continuous** without gaps. For example, if `res3.pak` is missing, `res4.pak` and any higher-numbered files will be ignored.

## Chinese Mainland Version

Fortunately, the Chinese mainland version has no signature verification or package tampering checks. This makes it easy to add new `.pak` files without affecting the game's ability to log in. However, **Bilibili client authorized login (quick login)** will not work, as the Bilibili client detects the incorrect signature.

![Login method choice](assets/Screenshot_2026-07-05-09-51-24-07_0715d4e5d0806f4dfa5884f7c8c92547.jpg)

When logging in on a modified package, choose the **phone number login** (手机号登录) option instead of Bilibili authorized login (bilibili授权登录).

### How to Mod

![Modding demo](assets/modding.gif)

The demonstration uses **MT Manager** as the APK modification tool.

> [!WARNING]
> After modification, you must uninstall the original version first, then install the modified APK. This is because the signature of the modified APK does not match the official version, and Android will refuse to install it.
>
> It is recommended to back up your local saves to the cloud before uninstalling.

> [!WARNING]
> Only the official Bilibili Game version has been verified. Channel versions may have additional signature verification or other integrity checks.

## Global Version

> [!IMPORTANT]
> Modding the original package (the genuine version downloaded from Google Play) is **extremely difficult**. The most viable approach for modding is to first bypass or remove Pairip from the package, and ideally merge all original PAK resources into a single APK's internal assets directory (bypassing PAD), which makes subsequent modifications much easier.

The Global version uses **Split APK**. The bundled PAK files included with the package are located in the `split_AssetPackMain.apk` split package. Additionally, it uses **Google Play Asset Delivery (PAD)** to deliver extra assets beyond what is bundled. PAD assets are loaded from a separate directory, and each PAD pack has a hardcoded limit of only `res.pak` through `res5.pak` (6 files max). The split APK assets and PAD assets are independent — PAD cannot fill gaps in the APK asset numbering.

For example, in version **v3.5.9**, the bundled split APK only contains `res.pak` and `res1.pak`, while `res2.pak`, `res3.pak`, and `res4.pak` are delivered via PAD. The PAD files are stored at the following paths (root access required, where `<versioncode>` varies per version (e.g., `263` for v3.5.9)):

- `res2.pak`: `/data/data/com.playdigious.deadcells.mobile/files/assetpacks/AssetPackMusicDefault/<versioncode>/<versioncode>/assets/`
- `res3.pak`: `/data/data/com.playdigious.deadcells.mobile/files/assetpacks/AssetPackMusicRetro/<versioncode>/<versioncode>/assets/`
- `res4.pak`: `/data/data/com.playdigious.deadcells.mobile/files/assetpacks/AssetPackDelivery/<versioncode>/<versioncode>/assets/`

If you attempt to load modded PAK files through PAD, in addition to the hardcoded `res.pak` to `res5.pak` limit, you would also need to **modify the dex** (Java layer) to register the additional asset packs, as the list of PAD packs is controlled at the Java level. However, this requires the package to already have Pairip bypassed; otherwise, the Pairip integrity check will be triggered and cause a crash.

The Global version is protected by **Pairip** (Google's Automatic Integrity Protection / AIP), which includes **installer checks** (blocking sideloaded APKs), **anti-tamper** detection (blocking modified or re-signed APKs), and **anti-hooking** detection (blocks tools like Frida and GDB from attaching to the process).

### How to Mod

Once Pairip has been bypassed or removed from the package and all original PAK files have been merged into the APK assets, the process is essentially the same as the Chinese mainland version. This approach is recommended because PAK files loaded from the APK assets directory use dynamic continuous numbering with no upper limit, avoiding the PAD hardcoded limit of only `res.pak` through `res5.pak`.

> [!WARNING]
> Versions that bundle game data (including PAD data) as external OBB-like archives have not been tested.

