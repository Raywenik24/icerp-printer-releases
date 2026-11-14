# ICERP Printer: help

**[Polski](pl.md)** · English

ICERP Printer is a small Windows app that prints ICERP's shipping labels, invoices and other
documents on this computer's printers. It runs in the tray, connects out to ICERP, and prints each
job once as soon as ICERP sends it. Nobody needs to open it during the day.

This page takes you from download to the first printed label.

1. [What you need](#what-you-need)
2. [Download and install](#download-and-install)
3. [Connect the app to ICERP](#connect-the-app-to-icerp)
4. [Choose the printers](#choose-the-printers)
5. [Print a test](#print-a-test)
6. [Print settings](#print-settings)
7. [Start with Windows, notifications, proxy](#start-with-windows-notifications-proxy)
8. [Updates](#updates)
9. [What the statuses mean](#what-the-statuses-mean)
10. [Logs and diagnostics](#logs-and-diagnostics)
11. [Common problems](#common-problems)
12. [Uninstall](#uninstall)

## What you need

- Windows 10 or 11, 64-bit.
- The printers installed in Windows, each with its driver. A label printer should print a test
  page from Windows before you start.
- An ICERP account that may manage printing, to open ICERP's **ICERP Printer** page.
- Internet access to your ICERP server. The app only connects out, so no port has to be opened.
- No administrator rights: the app installs for the current Windows user.

## Download and install

1. Open the **[latest release](https://github.com/Raywenik24/icerp-printer-releases/releases/latest)**
   (ICERP's ICERP Printer page links to it too).
2. Under **Assets**, download `ICERP-Printer_<version>_x64-setup.exe`.
   If the browser warns that the file is not commonly downloaded, keep it
   (Edge: **…** → **Keep** → **Keep anyway**).
3. Run the file. The installer is not code-signed, so the first time Windows shows
   **Windows protected your PC** with an unknown publisher:
   1. Click **More info**.
   2. Check that the file name is `ICERP-Printer_<version>_x64-setup.exe`.
   3. Click **Run anyway**.
4. Follow the installer. It needs no administrator prompt and is in Polish on a Polish Windows,
   English otherwise. On the last page you can tick a desktop shortcut. If WebView2 is missing, the
   installer downloads it, so stay online while it runs.
5. Start **ICERP Printer** from the last page or the Start menu.

The window opens with four tabs: **Status**, **Printers**, **Logs** and **Settings**. The **PL / EN**
buttons at the top switch the language; **?** opens this page.

**Closing the window does not stop the app.** It keeps running in the tray (the icon by the clock)
and keeps printing. Click the tray icon to open the window again; right-click it for **Open ICERP
Printer**, the connection status, **Check for updates** and **Quit**.

> On a freshly installed Windows 11, **Smart App Control** may block the app entirely. It has to be
> turned off (Windows Security → App & browser control → Smart App Control) before the app can be
> installed.

## Connect the app to ICERP

Each computer has its own key. ICERP creates it when you add the computer.

1. In ICERP, open the **ICERP Printer** page and click **Add computer** (*Dodaj komputer*).
2. Click **Set in app** (*Ustaw w aplikacji*). If the browser asks whether to open ICERP Printer,
   allow it.
3. The app shows **Add connection to erp.example.com?** (with your server's name). Click **Add connection**.

The Status tab now shows **Connected to ICERP** and the connection with the state **Connected**.

**If "Set in app" does nothing** (or you set up the app on another computer than the browser):

1. In ICERP, click **Copy** (*Kopiuj do schowka*) next to the connection string. It looks like
   `https://erp.example.com#icerp_1a2b3c4d_…`.
2. In the app, open **Settings** → **Connections**, paste it into **Connection string** and click
   **Add**.

ICERP shows the key only once. If you closed it, generate a new key for this computer in ICERP
(*Wygeneruj nowy klucz*) and use that.

One computer can print for several ICERP servers (for example a test and a production one): add
one connection for each. The keys are kept in Windows Credential Manager, not in a file.

## Choose the printers

ICERP sees only the printers you share with it.

1. In the app, open the **Printers** tab. It lists every printer Windows has, with its status.
   Each connection has its own column, named after the ICERP server.
2. In that column, tick the box next to each printer ICERP should use. It changes from
   **Not shared** to **Not active**: ICERP now has it.
3. In ICERP, on the ICERP Printer page, under **Active printers** (*Aktywne drukarki*), tick the
   printers to use and click **Save** (*Zapisz*). Printers are named `Printer name (Computer name)`.
4. Back in the app, the printer shows **Active**.

If ICERP's list is empty or out of date, click **Refresh printer list** (*Odśwież listę drukarek*)
in ICERP or **Refresh** on the app's Printers tab.

Unticking a printer takes it out of ICERP. ICERP keeps its tick but shows it as unavailable, and
any job ICERP still sends for it fails with **Printer not shared with this ICERP**.

## Print a test

- **From the app:** on the Printers tab, click **Print test page** next to a printer. The page names
  the printer and the computer, and shows how the print settings place it on the paper.
- **A label printer** that speaks its own language (ZPL, TSPL): click **Defaults** in its
  **Print settings** column, choose the **Label language** under **Label printer test (raw)**, and
  click **Print label test**.
- **From ICERP:** print a label or a document with the quick-print button. It should come out
  within a second or two, and the app's Status tab lists it under **Recent jobs** as **Printed**.

## Print settings

Print settings apply to PDF jobs (labels and documents ICERP sends as PDF). Labels in the printer's
own language (ZPL, TSPL, EPL) are sent to the printer unchanged.

**Settings → Printing** holds the defaults:

- **Default printer**: one for **Labels** and one for **Invoices and other documents**. They are
  used for jobs that name no printer. Each can be the Windows default.
- Six settings: **Rotate the printout 180 degrees**, **Scale the printout to fit the page**,
  **Enlarge the printout to fill the page**, **Horizontal position of the printout**,
  **Vertical position of the printout** and **Orientation of the printout (PDF)**.

**A printer's own settings:** on the Printers tab, click **Defaults** in the printer's **Print
settings** column. Each setting either follows the default (**Default: …**) or has its own value.
A printer with values of its own shows **Own settings** there; **Use defaults** clears them.

The paper size comes from the printer's settings in Windows. For a label printer, set its paper to
the label size in Windows (Printers & scanners → the printer → Printing preferences).

## Start with Windows, notifications, proxy

All in the **Settings** tab:

- **Startup → Start with Windows**: on by default. After you sign in, the app starts in the tray
  with no window, so labels print without anyone opening it. Leave it on at a packing station.
- **Notifications → Notify me when a job fails**: a Windows notification names the job, the
  printer and the reason. The tray icon is marked either way until you open the Logs tab.
- **Proxy → Connect through**: **System settings** (the proxy set in Windows, the default),
  **No proxy**, or **Manual** with an address such as `http://proxy.example.com:3128` and an
  optional user name and password. The password is kept in Windows Credential Manager.
- **Appearance → Theme**: System, Light or Dark.

## Updates

The app updates itself from the releases page. It checks when it starts and every few hours,
downloads a new version in the background and installs it once no job has been printing for a
minute. Jobs sent meanwhile wait in ICERP and print right after. The app starts again by itself
(in the tray if it was there) and a notification names the new version.

**Settings → Updates** shows the installed version and the last check; **Check for updates** (there
or in the tray menu) checks at once.

## What the statuses mean

**Connections** (Status tab and Settings → Connections):

| Status | Meaning | What to do |
|---|---|---|
| **Connected** | ICERP can send jobs. | Nothing. |
| **Connecting…** | The app is reaching ICERP. | Wait a few seconds. |
| **Offline** | ICERP cannot be reached; the app keeps trying. | Check the network and the proxy. |
| **Key rejected** | The key was revoked or generated again in ICERP, or the computer was deleted there. | In ICERP, generate a new key for this computer (or add it again if it was deleted), then click **Set in app**, or paste the string under **Replace key** in Settings → Connections. |
| **Key of another computer** | This key is already used by another PC. | Add this computer separately in ICERP. |
| **Update needed** | ICERP needs a newer app. | The app looks for an update at once; see [Updates](#updates). |

**Printers** (Printers tab): **Ready**, **Offline** (turn it on or plug it in), **Needs attention**
(paper, cover, error on the printer), **Unknown**, **Not on this computer** (ICERP still has it, but
Windows no longer lists it).

**Per connection** (the column of each ICERP): **Not shared** (ICERP does not see it),
**Not sent yet**, **Not active** (ICERP has it but does not use it), **Active**.

**Jobs** (Status and Logs tabs): **In progress**, **Sent to printer**, **Printed**, **Failed**
(with the reason).

## Logs and diagnostics

The **Logs** tab has two views:

- **Job history**: every job of the last 30 days, with its printer, time, status and, for a failed
  job, the reason. **Failed only**, the **Connection** filter and **Search titles** narrow it.
- **App log**: what the app is doing, live.

**Open log folder** opens the daily log files (`%LOCALAPPDATA%\pl.icerihub.printer\logs`, kept for
14 days). **Copy diagnostics** copies a summary for whoever helps you: versions, connections,
printers and recent errors. It contains no keys; paste it into your message.

## Common problems

**Windows protected your PC / the browser blocks the download.** Expected for this installer; see
[Download and install](#download-and-install).

**"Set in app" does nothing.** Check that the app is installed on this computer, then paste the
connection string instead (Settings → Connections).

**"This key belongs to another computer."** Each computer needs its own entry in ICERP. Click
**Add computer** in ICERP for this one.

**ICERP shows no printers.** Tick them on the app's Printers tab, check the connection is
**Connected**, then click **Refresh printer list** in ICERP.

**A job failed with "Printer offline".** Turn the printer on or plug it in. The app keeps trying
until the job expires in ICERP (one minute by default); after that, send it again.

**"Printer not shared with this ICERP".** The job was for a printer that is not ticked for this
ICERP on the Printers tab, or it named no printer and the default printer for its kind is not
shared. Tick it, or choose another default in Settings → Printing.

**"Expired before it could print".** The computer was off, asleep or offline when the job was
sent, or the printer stayed offline. Send it again.

**The label is too small, cut off or on the wrong spot.** Set the label printer's paper size in
Windows to the label size, then use **Print test page** and the print settings (scale, fill,
position, rotation) until it fits.

**Nothing prints after the PC restarts.** Check **Settings → Start with Windows** and that the app
is in the tray.

**Still stuck?** Open the Logs tab, click **Copy diagnostics** and send it to whoever looks after
ICERP.

## Uninstall

Windows Settings → Apps → **ICERP Printer** → Uninstall. Settings, the job history and the logs are
kept unless you tick **Delete the application data**. Keys stay in Windows Credential Manager; also
delete this computer in ICERP so its key stops working.
