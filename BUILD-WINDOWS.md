# Snowhush portable Windows build

This repository copy removes the Support item from the Windows tray menu and adds a
GitHub Actions workflow that builds the Windows app binary directly (not the setup
installer).

## Build using GitHub's Windows runner

1. Create a new **private** repository on GitHub.
2. Extract this ZIP on your PC.
3. Upload the *contents* of the `Snowhush-main` folder to the repository root
   (so `windows`, `core`, `Sources`, `Package.swift`, etc. are at the top level).
4. In the repository, create the file
   `.github/workflows/build-portable-windows.yml` and paste the workflow from
   that path in this ZIP.
5. Commit the file.
6. Open the repository's **Actions** tab. Select
   **Build portable Snowhush for Windows**, then **Run workflow**.
7. When it finishes successfully, open the run and download the
   `Snowhush-portable-Windows-x64` artifact. Extract it to get `Snowhush.exe`.

The workflow builds the `Snowhush` binary from `windows/Cargo.toml`. It does not
enable the `setup` feature and does not build `Snowhush-Setup.exe`.

## Startup setting

The Windows source already has an **Open at Login** menu setting. It writes a
per-user Windows Run registry value, so it does not need administrator rights.
Put `Snowhush.exe` in a permanent folder before enabling it; moving the EXE later
can break the startup entry.

## Security

A source build is not automatically safe. Review the source and dependencies,
inspect the GitHub Actions log, and scan the resulting EXE before running it.
The build is unsigned unless separately signed, so SmartScreen may show a warning.
