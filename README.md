# NPV Tunnel Configuration Decoder

A lightweight Windows GUI for opening and decoding NPV Tunnel configuration files (`.npvs` and `.npvt`). The interface is built with Python and Tkinter, while the actual configuration decoding is handled by the bundled [Pantegnos](https://github.com/FrontierTM/Pantegnos/) command-line tool.

## Features

- Simple Windows desktop interface.
- Automatically starts decoding after a configuration file is selected with **Open .npvs file**.
- File diagnostics, including file size, detected signature, UTF-8 check, and readable ASCII fragments.
- Displays decoded text in the application.
- Copy decoded output or save it to a file.
- Light and dark themes.
- Automatically locates the bundled Pantegnos executable.
- Can be packaged as a portable Windows executable.

## Requirements

### Running from source

- Windows
- Python 3.10 or newer
- Tkinter (usually included with the standard Windows Python installer)
- The Pantegnos executable and its accompanying license/notice files

### Running the packaged application

Python does not need to be installed on the destination computer. Keep the application executable and the `tools` directory together:

```text
Portable_EXE/
├── NPVSDecoder.exe
└── tools/
    ├── pantegnos.exe
    ├── LICENSE
    └── PANTEGNOS_README.md
```

Do not distribute `NPVSDecoder.exe` on its own; the Pantegnos executable is required for decoding.

## Run from source

Open PowerShell in the project directory and run:

```powershell
py main.py
```

Select **Open .npvs file** and choose a supported configuration file. Decoding starts automatically. If Pantegnos requests a passphrase, enter it in the console window it opens.

## Build a Windows EXE

On the build computer, install Python 3.10+ and PyInstaller:

```powershell
py -m pip install --upgrade pyinstaller
```

From the project source directory, build the GUI executable:

```powershell
py -m PyInstaller --noconfirm --clean --onefile --windowed --name NPVSDecoder .\main.py
```

Then create the portable folder and copy the required files:

```powershell
New-Item -ItemType Directory -Force .\Portable_EXE\tools | Out-Null
Copy-Item .\dist\NPVSDecoder.exe .\Portable_EXE\NPVSDecoder.exe -Force
Copy-Item .\tools\pantegnos.exe .\Portable_EXE\tools\pantegnos.exe -Force
Copy-Item .\tools\LICENSE .\Portable_EXE\tools\LICENSE -Force
Copy-Item .\tools\PANTEGNOS_README.md .\Portable_EXE\tools\PANTEGNOS_README.md -Force
```

Transfer the entire `Portable_EXE` folder to the destination computer.

## How it works

The GUI copies the selected configuration into a temporary input directory and runs Pantegnos with input and output directories. Text files produced by Pantegnos are then loaded into the application for viewing, copying, or saving.

This project provides a graphical interface; it does **not** implement its own decryption algorithm.

## Limitations

- Successful decoding depends on whether Pantegnos supports the selected file variant and whether any required passphrase is correct.
- Some files may fail to decode. If that happens, check the Pantegnos console output for details.
- The application should be tested with the specific configuration files you intend to use. Support for every `.npvs`/`.npvt` variant is not guaranteed.

## Licensing

Pantegnos is a separate project with its own license and notices. The Pantegnos README identifies its current release as licensed under **AGPL-3.0**. Keep its license and attribution files with the bundled executable, and review the license requirements before redistributing this application or modified builds. This README does not replace the upstream license.

## Acknowledgements

Special thanks to the [Pantegnos project](https://github.com/FrontierTM/Pantegnos/) by **FrontierTM**. This application relies on Pantegnos for the underlying NPV Tunnel configuration decoding functionality. Thank you for making this project available and for the work behind it.
