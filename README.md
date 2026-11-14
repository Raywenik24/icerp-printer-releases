# ICERP Printer: releases

Installers and update files for **ICERP Printer**, the Windows app that prints ICERP's labels and
documents on a PC's local printers. This repository holds releases only; there is no source here.

## Download

**[Latest release](https://github.com/Raywenik24/icerp-printer-releases/releases/latest)**: under
*Assets*, download `ICERP-Printer_<version>_x64-setup.exe` and run it.

- Windows 10 or 11, x64. Installs for the current Windows user, with no administrator prompt.
- The installer is not code-signed. Windows SmartScreen shows "Windows protected your PC": click
  **More info**, then **Run anyway**.
- After installing, open ICERP's "ICERP Printer" integration page and click **Set in app**.
- The app updates itself from this repository.

## Pobieranie

**[Najnowsze wydanie](https://github.com/Raywenik24/icerp-printer-releases/releases/latest)**: w
sekcji *Assets* pobierz `ICERP-Printer_<wersja>_x64-setup.exe` i uruchom.

- Windows 10 lub 11, x64. Instaluje się dla bieżącego użytkownika Windows, bez uprawnień
  administratora.
- Instalator nie jest podpisany cyfrowo. Windows SmartScreen pokaże „System Windows ochronił ten
  komputer”: kliknij **Więcej informacji**, a potem **Uruchom mimo to**.
- Po instalacji otwórz w ICERP stronę integracji „ICERP Printer” i kliknij **Ustaw w aplikacji**.
- Aplikacja aktualizuje się sama z tego repozytorium.

## Files in each release

| File | Use |
|---|---|
| `ICERP-Printer_<version>_x64-setup.exe` | The installer |
| `ICERP-Printer_<version>_x64-setup.exe.sig` | Its update signature |
| `latest.json` | The update manifest the app reads |
