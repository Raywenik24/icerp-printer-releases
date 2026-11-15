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
7. [Check a label printer's status](#check-a-label-printers-status)
8. [Printers in Windows](#printers-in-windows)
9. [Start with Windows, notifications, proxy](#start-with-windows-notifications-proxy)
10. [Updates](#updates)
11. [What the statuses mean](#what-the-statuses-mean)
12. [Logs and diagnostics](#logs-and-diagnostics)
13. [Common problems](#common-problems)
14. [Uninstall](#uninstall)

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

### Several Windows accounts on one PC

The app installs for one Windows user, with its own settings, keys and job history. If several
people sign in to this PC with their own Windows accounts, each account that should print installs
the app and gets its own key: in ICERP, click **Add computer** once for each account. ICERP then
lists the PC once per account, and a printer shared from both shows under both.

After **Switch user**, the first account's app keeps running in the background and keeps printing
the jobs ICERP sends to it, next to the app of the account now signed in.

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
the label size in Windows (Printers & scanners → the printer → Printing preferences, or
**Printing preferences** in the app, see [Printers in Windows](#printers-in-windows)).

## Check a label printer's status

A label printer that cannot print (lid open, no labels) still takes the label into its own memory
and prints it later, once the paper button is pressed, even if the label was printed again from
ICERP meanwhile. Two labels come out. To prevent that, the app can ask the printer whether it is
ready before it sends each job.

This works for **label printers that speak TSPL** (such as the 4BARCODE) connected over **USB** or
on a **standard TCP/IP port** (raw, port 9100). Do not tick it for other printers: they may print
the question as a page of odd characters.

1. On the Printers tab, click **Defaults** (or **Own settings**) in the printer's **Print settings**
   column.
2. Under **Printer status**, tick **Check the printer's status before printing (TSPL label
   printers)**. On any other kind of port it is greyed out, with a note that status checks work
   only for USB printers and standard TCP/IP (raw 9100) ports.
3. **Check now** asks the printer once and shows its answer: **Ready**, **Printing**, **Lid open**,
   **No paper**, **Paper jam**, **Paused**, **Ribbon end**, **Error**, **Unknown answer** or **No
   answer**. It works whether the box is ticked or not.

With the box ticked, every job for that printer, labels and PDFs alike, is sent only when the
printer answers **Ready** or **Printing**. Any other answer holds the job in the app:

- The Status and Logs tabs show the job as **Waiting for printer: Lid open** (or whatever the
  printer reports), and the tray icon is marked while jobs wait.
- A Windows notification names the printer and its state, once when the printer starts holding
  jobs and once more if its state changes (for example from Lid open to No paper). Not one per job.
- The app asks the printer again every 2 seconds. As soon as it is ready (lid closed, roll loaded),
  the waiting jobs print, each once.
- If the printer is not ready before the job expires (one minute by default), the job fails with
  **Printer not ready: …**, naming the last state, and it never prints late. ICERP shows it as
  failed; print it again from there.
- **No answer** holds jobs too: the printer is switched off, unplugged or unreachable over the
  network. **Check now** shows it at once.
- **Print test page** and **Print label test** check first as well, but do not wait: they say at
  once what is wrong and print nothing.

**After changing the roll, press the paper (feed) button.** With the lid closed and no roll, the
printer still answers **Ready** until the button is pressed or a label is sent. A label sent then
goes to the printer and can be lost: the app and ICERP show it as printed, but it does not come
out, not even after a new roll is loaded. Print it again from ICERP.

**One limit:** the label being printed at the moment the roll runs out has already reached the
printer. It comes out once a new roll is loaded and the paper button is pressed, even if it was
printed again meanwhile.

## Printers in Windows

### Printers that ask for a file name

"Microsoft Print to PDF", "Microsoft XPS Document Writer" and any printer on the `FILE:` port open
a **Save As** window for every job. On a PC nobody is watching, nobody answers it: the job stays in
progress, ICERP marks it failed, and that printer's later jobs wait behind it. The Printers tab
warns about it under the printer's share tick. Share such a printer only for testing, on a PC
someone is sitting at.

### Opening a printer's queue and preferences

Windows 10 Settings does not list every printer: a second printer on the same port (for example
"Canon MF650C Series UFR II") and "Microsoft Print to PDF" are missing there, so their print queue
and printing preferences cannot be opened from Settings.

**In the app**, for any printer: on the Printers tab, click **Defaults** (or **Own settings**) in
the printer's **Print settings** column, then under **In Windows** click **Open print queue** or
**Printing preferences**. Windows' own windows open for that printer.

**By hand:** press Win+R and type one of these, with the printer's name exactly as Windows shows it:

| Command | Opens |
|---|---|
| `rundll32 printui.dll,PrintUIEntry /o /n "Printer name"` | the print queue |
| `rundll32 printui.dll,PrintUIEntry /e /n "Printer name"` | the printing preferences |
| `rundll32 printui.dll,PrintUIEntry /y /n "Printer name"` | sets it as the Windows default printer (no window) |

## Start with Windows, notifications, proxy

All in the **Settings** tab:

- **Startup → Start with Windows**: on by default. After you sign in, the app starts in the tray
  with no window, so labels print without anyone opening it. Leave it on at a packing station.
- **Notifications → Notify about printing problems**: a Windows notification when a job fails
  (naming the job, the printer and the reason) and when a printer starts holding jobs because it
  is not ready (see [Check a label printer's status](#check-a-label-printers-status)). The tray
  icon is marked either way: for failed jobs until you open the Logs tab, for held jobs while they
  wait.
- **Proxy → Connect through**: **System settings** (the proxy set in Windows, the default),
  **No proxy**, or **Manual** with an address such as `http://proxy.example.com:3128` and an
  optional user name and password. The password is kept in Windows Credential Manager.
  If your network uses a proxy setup script, enter the proxy under **Manual**.
- **Appearance → Theme**: System, Light or Dark.

## Updates

The app updates itself from the releases page. It checks when it starts and every few hours,
downloads a new version in the background and installs it once no job has been printing for a
minute. Jobs sent meanwhile wait in ICERP and print right after. The app starts again by itself
(in the tray if it was there) and a notification names the new version.

**Settings → Updates** shows the installed version and the last check; **Check for updates** (there
or in the tray menu) checks at once.

**Check for updates** in the tray menu answers with a notification, even with notifications
switched off: the app is up to date, a new version is downloading, a new version is ready (it
installs when no job is printing), or the check failed (the reason is in the log). Click the
notification to open Settings → Updates. The automatic checks and the button in Settings show no
notification.

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

**Jobs** (Status and Logs tabs): **In progress**, **Waiting for printer: …** (the label printer is
not ready; see [Check a label printer's status](#check-a-label-printers-status)), **Sent to
printer**, **Printed**, **Failed** (with the reason).

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

**A job failed with "Printer not ready: …".** The label printer's status check found it not ready
(lid open, no paper, paused…) until the job expired. Close the lid or load a roll and press the
paper button, then send it again. See [Check a label printer's status](#check-a-label-printers-status).

**Jobs keep "Waiting for printer: No answer".** The app cannot reach the label printer: it is off,
unplugged, or unreachable over the network. Turn it on or plug it in; **Check now** on the
Printers tab should then say **Ready**. If that printer can never answer, untick its status check.

**A job for Print to PDF or XPS never finishes.** The printer is waiting for someone to choose a
file name. See [Printers that ask for a file name](#printers-that-ask-for-a-file-name).

**A printer is missing from Windows Settings.** Open its queue or preferences from the app; see
[Opening a printer's queue and preferences](#opening-a-printers-queue-and-preferences).

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
