# Multi-Format Configuration Decoder for Windows

A lightweight Python/Tkinter Windows GUI for opening, inspecting, and attempting to decode supported configuration files across multiple extensions.

## Supported file extensions

The Open dialog includes the following formats:

- `.slip` — SlipNet profiles
- `.ehi` — HTTP Injector configurations
- `.dark` — DarkTunnel configurations
- `.hat` — HA Tunnel Plus configurations
- `.npvt`, `.npvs` — NPV Tunnel configurations
- `.nm` — NetMod configurations
- `.happ` — Happ Proxy configurations
- `.bpf` — profile exports associated with sing-box tools
- `.tls` — TLS Tunnel profiles

The file picker also includes **All files** so you can select a file even if its extension is missing or unusual.

> **Compatibility note:** Listing an extension in the file picker does not guarantee every variant with that extension can be decoded. Successful decoding depends on the actual file format, the bundled decoding engine's capabilities, and a correct passphrase when required.

## Features

- Multi-format file picker with per-extension filters
- File inspection and automatic decoding attempt after selection
- View, copy, and save decoded output
- Light/dark theme
- Portable Windows EXE build support

## Run from source

Python 3.10+ with Tkinter is required.

```powershell
py main.py
```

## Project layout

```text
NPVS_Decoder_Source/
  main.py
  tools/
    pantegnos.exe
    LICENSE
    PANTEGNOS_README.md
  build.bat
  requirements.txt
```

## Build the Windows EXE

Run `build.bat` on Windows. It builds `dist\NPVSDecoder.exe` and copies the `tools` folder next to the executable. Distribute the full `Portable_EXE` folder, not the EXE alone, because the bundled decoding engine is required.

If a selected file requires a passphrase, a separate console window may appear to request it.

## Troubleshooting

- If decoding fails, verify the passphrase and check whether that specific file variant is supported by the bundled engine.
- Keep the `tools` folder next to the EXE.
- Use **All files** if the file does not have one of the listed extensions.

## Third-party engine and license

This application bundles a third-party decoding engine in `tools/`. Its original license and notices are retained in that folder. Review `tools/LICENSE` and `tools/PANTEGNOS_README.md` before redistribution, and comply with the applicable license terms, including source-code obligations where required.
