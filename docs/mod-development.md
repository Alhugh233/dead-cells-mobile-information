# Mod Development Notes

> [!TIP]
> Before reading this section, it is recommended to first read **[ModDocCE](https://n3rdl0rd.github.io/ModDocCE/)** to familiarize yourself with the fundamentals of Dead Cells modding.

## PAK Resource Differences

There are minor differences in PAK resource files between the Chinese mainland version and the Global version. For example, some `.png` texture files in the Chinese mainland version are stored as `.ktx` in the Global version. If you plan to create mods that deeply modify resources (such as custom visual effects), keep this format difference in mind.

## PAK Stamp Differences

The PAK format includes a **stamp** (a Git commit hash) embedded in the file header for version matching. Even when both versions share the same version number (e.g., v3.5.9), the Chinese mainland version and the Global version have **different stamps**. This means you must package separate PAK files for each version with their respective stamps.

