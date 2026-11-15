# ICERP Printer: pomoc

Polski · **[English](en.md)**

ICERP Printer to mały program dla Windows, który drukuje etykiety wysyłkowe, faktury i inne
dokumenty z ICERP na drukarkach tego komputera. Działa w zasobniku, sam łączy się z ICERP
i drukuje każde zlecenie raz, gdy tylko ICERP je wyśle. W ciągu dnia nikt nie musi go otwierać.

Ta strona prowadzi od pobrania programu do pierwszej wydrukowanej etykiety.

1. [Czego potrzebujesz](#czego-potrzebujesz)
2. [Pobieranie i instalacja](#pobieranie-i-instalacja)
3. [Połączenie z ICERP](#połączenie-z-icerp)
4. [Wybór drukarek](#wybór-drukarek)
5. [Wydruk testowy](#wydruk-testowy)
6. [Ustawienia wydruku](#ustawienia-wydruku)
7. [Sprawdzanie stanu drukarki etykiet](#sprawdzanie-stanu-drukarki-etykiet)
8. [Drukarki w systemie Windows](#drukarki-w-systemie-windows)
9. [Uruchamianie z Windows, powiadomienia, proxy](#uruchamianie-z-windows-powiadomienia-proxy)
10. [Aktualizacje](#aktualizacje)
11. [Co oznaczają stany](#co-oznaczają-stany)
12. [Logi i diagnostyka](#logi-i-diagnostyka)
13. [Typowe problemy](#typowe-problemy)
14. [Odinstalowanie](#odinstalowanie)

## Czego potrzebujesz

- Windows 10 lub 11, 64-bitowy.
- Drukarki zainstalowane w Windows, każda z własnym sterownikiem. Drukarka etykiet powinna przed
  startem wydrukować stronę testową z Windows.
- Konto w ICERP z prawem do zarządzania drukowaniem, aby otworzyć w ICERP stronę **ICERP Printer**.
- Dostęp do internetu i do Twojego serwera ICERP. Program łączy się tylko na zewnątrz, więc nie
  trzeba otwierać żadnych portów.
- Bez uprawnień administratora: program instaluje się dla bieżącego użytkownika Windows.

## Pobieranie i instalacja

1. Otwórz **[najnowsze wydanie](https://github.com/Raywenik24/icerp-printer-releases/releases/latest)**
   (link jest też na stronie ICERP Printer w ICERP).
2. W sekcji **Assets** pobierz plik `ICERP-Printer_<wersja>_x64-setup.exe`.
   Jeśli przeglądarka ostrzeże, że plik nie jest często pobierany, zachowaj go
   (Edge: **…** → **Zachowaj** → **Zachowaj mimo to**).
3. Uruchom plik. Instalator nie jest podpisany cyfrowo, więc za pierwszym razem Windows pokaże
   **System Windows ochronił ten komputer** z nieznanym wydawcą:
   1. Kliknij **Więcej informacji**.
   2. Sprawdź, czy nazwa pliku to `ICERP-Printer_<wersja>_x64-setup.exe`.
   3. Kliknij **Uruchom mimo to**.
4. Przejdź przez instalator. Nie prosi o uprawnienia administratora; w polskim Windows jest po
   polsku, w innych po angielsku. Na ostatniej stronie możesz zaznaczyć skrót na pulpicie. Jeśli
   brakuje WebView2, instalator go pobierze, więc nie odłączaj internetu w trakcie.
5. Uruchom **ICERP Printer** z ostatniej strony instalatora albo z menu Start.

Okno ma cztery zakładki: **Status**, **Drukarki**, **Logi** i **Ustawienia**. Przyciski **PL / EN**
u góry zmieniają język; **?** otwiera tę stronę.

**Zamknięcie okna nie wyłącza programu.** Działa dalej w zasobniku (ikona przy zegarze) i dalej
drukuje. Kliknij ikonę, aby znów otworzyć okno; prawy przycisk otwiera menu: **Otwórz ICERP
Printer**, stan połączenia, **Sprawdź aktualizacje** i **Zakończ**.

> W świeżo zainstalowanym Windows 11 **Inteligentna kontrola aplikacji** (Smart App Control) może
> całkiem zablokować program. Trzeba ją wyłączyć (Zabezpieczenia Windows → Kontrolka aplikacji
> i przeglądarki → Inteligentna kontrola aplikacji), zanim program da się zainstalować.

## Połączenie z ICERP

Każdy komputer ma własny klucz. ICERP tworzy go, gdy dodajesz komputer.

1. W ICERP otwórz stronę **ICERP Printer** i kliknij **Dodaj komputer**.
2. Kliknij **Ustaw w aplikacji**. Jeśli przeglądarka zapyta, czy otworzyć ICERP Printer, zezwól.
3. Program zapyta **Dodać połączenie z erp.example.com?** (z nazwą Twojego serwera). Kliknij **Dodaj połączenie**.

Zakładka Status pokazuje teraz **Połączono z ICERP**, a przy połączeniu stan **Połączono**.

**Jeśli „Ustaw w aplikacji” nic nie robi** (albo program jest na innym komputerze niż przeglądarka):

1. W ICERP kliknij **Kopiuj do schowka** przy ciągu połączenia. Wygląda on tak:
   `https://erp.example.com#icerp_1a2b3c4d_…`.
2. W programie otwórz **Ustawienia** → **Połączenia**, wklej go w pole **Ciąg połączenia**
   i kliknij **Dodaj**.

ICERP pokazuje klucz tylko raz. Jeśli okno z kluczem zostało już zamknięte, wygeneruj w ICERP nowy
klucz dla tego komputera (**Wygeneruj nowy klucz**) i użyj go.

Jeden komputer może drukować dla kilku serwerów ICERP (na przykład testowego i produkcyjnego):
dodaj po jednym połączeniu dla każdego. Klucze są przechowywane w Menedżerze poświadczeń Windows,
nie w pliku.

### Kilka kont Windows na jednym komputerze

Program instaluje się dla jednego użytkownika Windows, z własnymi ustawieniami, kluczami i historią
zleceń. Jeśli na tym komputerze loguje się kilka osób na własne konta Windows, każde konto, które ma
drukować, instaluje program i dostaje własny klucz: w ICERP kliknij **Dodaj komputer** osobno dla
każdego konta. ICERP pokazuje wtedy ten komputer raz dla każdego konta, a drukarka udostępniona
z obu kont widnieje pod oboma.

Po **Przełącz użytkownika** program pierwszego konta dalej działa w tle i dalej drukuje zlecenia,
które ICERP do niego wysyła, obok programu konta, które jest teraz zalogowane.

## Wybór drukarek

ICERP widzi tylko drukarki, które mu udostępnisz.

1. W programie otwórz zakładkę **Drukarki**. Są tam wszystkie drukarki z Windows wraz ze stanem.
   Każde połączenie ma własną kolumnę, nazwaną tak jak serwer ICERP.
2. W tej kolumnie zaznacz pole przy każdej drukarce, której ma używać ICERP. Stan zmieni się
   z **Nieudostępniona** na **Nieaktywna**: ICERP już ją ma.
3. W ICERP, na stronie ICERP Printer, w sekcji **Aktywne drukarki** zaznacz drukarki, których chcesz
   używać, i kliknij **Zapisz**. Drukarki mają tam nazwy `Nazwa drukarki (Nazwa komputera)`.
4. W programie drukarka ma teraz stan **Aktywna**.

Jeśli lista w ICERP jest pusta albo nieaktualna, kliknij w ICERP **Odśwież listę drukarek** albo
**Odśwież** w zakładce Drukarki w programie.

Odznaczenie drukarki usuwa ją z ICERP. ICERP zachowuje jej zaznaczenie, ale pokazuje ją jako
niedostępną, a zlecenia, które jeszcze do niej wyśle, kończą się błędem **Drukarka
nieudostępniona dla tego ICERP**.

## Wydruk testowy

- **Z programu:** w zakładce Drukarki kliknij **Drukuj stronę testową** przy drukarce. Strona podaje
  drukarkę i komputer oraz pokazuje, jak ustawienia wydruku układają ją na papierze.
- **Drukarka etykiet** z własnym językiem (ZPL, TSPL): kliknij **Domyślne** w jej kolumnie
  **Ustawienia wydruku**, w części **Test drukarki etykiet (raw)** wybierz **Język etykiety**
  i kliknij **Drukuj etykietę testową**.
- **Z ICERP:** wydrukuj etykietę albo dokument przyciskiem szybkiego drukowania. Wydruk powinien
  pojawić się w sekundę lub dwie, a zakładka Status w programie pokaże go w sekcji
  **Ostatnie zlecenia** jako **Wydrukowane**.

## Ustawienia wydruku

Ustawienia wydruku dotyczą zleceń PDF (etykiet i dokumentów, które ICERP wysyła jako PDF). Etykiety
w języku drukarki (ZPL, TSPL, EPL) trafiają do drukarki bez zmian.

**Ustawienia → Drukowanie** to ustawienia domyślne:

- **Domyślna drukarka**: osobno **Etykiety** oraz **Faktury i inne dokumenty**. Są używane dla
  zleceń bez wskazanej drukarki. Każda może być domyślną drukarką Windows.
- Sześć ustawień: **Obróć wydruk 180 stopni**, **Skaluj plik wydruku, aby zmieścił się na stronie**,
  **Powiększ wydruk, aby wypełnił stronę**, **Położenie poziome wydruku**, **Położenie pionowe
  wydruku** i **Orientacja wydruku (PDF)**.

**Własne ustawienia drukarki:** w zakładce Drukarki kliknij **Domyślne** w kolumnie **Ustawienia
wydruku** tej drukarki. Każde ustawienie albo podąża za domyślnym (**Domyślnie: …**), albo ma własną
wartość. Drukarka z własnymi wartościami ma tam napis **Własne ustawienia**; **Użyj domyślnych**
je czyści.

Rozmiar papieru pochodzi z ustawień drukarki w Windows. W drukarce etykiet ustaw w Windows papier
o rozmiarze etykiety (Drukarki i skanery → drukarka → Preferencje drukowania albo **Preferencje
drukowania** w programie, zobacz [Drukarki w systemie Windows](#drukarki-w-systemie-windows)).

## Sprawdzanie stanu drukarki etykiet

Drukarka etykiet, która nie może drukować (otwarta pokrywa, brak etykiet), i tak przyjmuje etykietę
do własnej pamięci i drukuje ją później, po naciśnięciu przycisku papieru, nawet jeśli w tym czasie
etykietę wydrukowano ponownie z ICERP. Wychodzą wtedy dwie etykiety. Aby temu zapobiec, program może
przed wysłaniem każdego zlecenia zapytać drukarkę, czy jest gotowa.

Działa to dla **drukarek etykiet obsługujących TSPL** (takich jak 4BARCODE) podłączonych przez
**USB** albo na **standardowym porcie TCP/IP** (raw, port 9100). Nie zaznaczaj tego dla innych
drukarek: mogą wydrukować pytanie jako stronę dziwnych znaków.

1. W zakładce Drukarki kliknij **Domyślne** (albo **Własne ustawienia**) w kolumnie **Ustawienia
   wydruku** tej drukarki.
2. W części **Stan drukarki** zaznacz **Sprawdzaj stan drukarki przed drukowaniem (drukarki etykiet
   TSPL)**. Przy innym rodzaju portu pole jest wyszarzone, z uwagą, że sprawdzanie stanu działa tylko
   dla drukarek USB i standardowych portów TCP/IP (raw 9100).
3. **Sprawdź teraz** pyta drukarkę raz i pokazuje odpowiedź: **Gotowa**, **Drukuje**, **Otwarta
   pokrywa**, **Brak papieru**, **Zacięcie papieru**, **Wstrzymana**, **Koniec taśmy**, **Błąd**,
   **Nieznana odpowiedź** albo **Brak odpowiedzi**. Działa niezależnie od tego, czy pole jest
   zaznaczone.

Gdy pole jest zaznaczone, każde zlecenie dla tej drukarki, etykiety i PDF-y tak samo, jest wysyłane
tylko wtedy, gdy drukarka odpowie **Gotowa** albo **Drukuje**. Każda inna odpowiedź wstrzymuje
zlecenie w programie:

- Zakładki Status i Logi pokazują zlecenie jako **Czeka na drukarkę: Otwarta pokrywa** (albo to, co
  zgłasza drukarka), a ikona w zasobniku jest oznaczona, dopóki zlecenia czekają.
- Powiadomienie Windows podaje drukarkę i jej stan: raz, gdy drukarka zaczyna wstrzymywać zlecenia,
  i jeszcze raz, jeśli jej stan się zmieni (na przykład z Otwarta pokrywa na Brak papieru). Nie po
  jednym na każde zlecenie.
- Program pyta drukarkę ponownie co 2 sekundy. Gdy tylko jest gotowa (pokrywa zamknięta, rolka
  założona), czekające zlecenia się drukują, każde raz.
- Jeśli drukarka nie będzie gotowa, zanim zlecenie wygaśnie (domyślnie po minucie), zlecenie kończy
  się błędem **Drukarka nie jest gotowa: …** z ostatnim stanem i nigdy nie drukuje się z opóźnieniem.
  ICERP pokazuje je jako nieudane; wydrukuj je stamtąd ponownie.
- **Brak odpowiedzi** też wstrzymuje zlecenia: drukarka jest wyłączona, odłączona albo
  nieosiągalna w sieci. **Sprawdź teraz** pokaże to od razu.
- **Drukuj stronę testową** i **Drukuj etykietę testową** też najpierw sprawdzają stan, ale nie
  czekają: od razu mówią, co jest nie tak, i nic nie drukują.

**Po wymianie rolki naciśnij przycisk papieru (podawania).** Przy zamkniętej pokrywie i bez rolki
drukarka nadal odpowiada **Gotowa**, dopóki nie naciśniesz przycisku albo nie zostanie wysłana
etykieta. Etykieta wysłana w tym czasie trafia do drukarki i może przepaść: aplikacja i ICERP
pokazują ją jako wydrukowaną, ale nie wychodzi, nawet po założeniu nowej rolki. Wydrukuj ją
ponownie z ICERP.

**Jedno ograniczenie:** etykieta drukowana w chwili, gdy kończy się rolka, jest już w drukarce.
Wyjdzie po założeniu nowej rolki i naciśnięciu przycisku papieru, nawet jeśli w tym czasie
wydrukowano ją ponownie.

## Drukarki w systemie Windows

### Drukarki, które pytają o nazwę pliku

„Microsoft Print to PDF”, „Microsoft XPS Document Writer” i każda drukarka na porcie `FILE:`
otwierają okno **Zapisz jako** przy każdym zleceniu. Na komputerze, którego nikt nie pilnuje, nikt
go nie zamknie: zlecenie zostaje w toku, ICERP oznacza je jako nieudane, a kolejne zlecenia tej
drukarki czekają za nim. Zakładka Drukarki ostrzega o tym pod polem udostępniania takiej drukarki.
Udostępniaj ją tylko do testów, na komputerze, przy którym ktoś siedzi.

### Otwieranie kolejki i preferencji drukarki

Ustawienia Windows 10 nie pokazują każdej drukarki: brakuje tam drugiej drukarki na tym samym
porcie (na przykład „Canon MF650C Series UFR II”) i „Microsoft Print to PDF”, więc ich kolejki
wydruku i preferencji drukowania nie da się otworzyć z Ustawień.

**W programie**, dla każdej drukarki: w zakładce Drukarki kliknij **Domyślne** (albo **Własne
ustawienia**) w kolumnie **Ustawienia wydruku** tej drukarki, a potem w części **W systemie
Windows** kliknij **Otwórz kolejkę wydruku** albo **Preferencje drukowania**. Otworzą się okna
systemu Windows dla tej drukarki.

**Ręcznie:** naciśnij Win+R i wpisz jedno z poleceń, z nazwą drukarki dokładnie taką, jak pokazuje
ją Windows:

| Polecenie | Otwiera |
|---|---|
| `rundll32 printui.dll,PrintUIEntry /o /n "Nazwa drukarki"` | kolejkę wydruku |
| `rundll32 printui.dll,PrintUIEntry /e /n "Nazwa drukarki"` | preferencje drukowania |
| `rundll32 printui.dll,PrintUIEntry /y /n "Nazwa drukarki"` | ustawia ją jako domyślną drukarkę Windows (bez okna) |

## Uruchamianie z Windows, powiadomienia, proxy

Wszystko w zakładce **Ustawienia**:

- **Uruchamianie → Uruchamiaj razem z Windows**: domyślnie włączone. Po zalogowaniu program
  uruchamia się w zasobniku, bez okna, więc etykiety drukują się bez otwierania go. Na stanowisku
  pakowania zostaw to włączone.
- **Powiadomienia → Powiadamiaj o problemach z drukowaniem**: powiadomienie Windows, gdy zlecenie
  się nie powiedzie (podaje zlecenie, drukarkę i przyczynę), oraz gdy drukarka nie jest gotowa
  i zaczyna wstrzymywać zlecenia (zobacz [Sprawdzanie stanu drukarki
  etykiet](#sprawdzanie-stanu-drukarki-etykiet)). Ikona w zasobniku jest oznaczana tak czy inaczej:
  przy nieudanych zleceniach do otwarcia zakładki Logi, przy wstrzymanych, dopóki czekają.
- **Proxy → Połączenie przez**: **Ustawienia systemu** (proxy ustawione w Windows, domyślnie),
  **Bez proxy** albo **Ręcznie** z adresem, np. `http://proxy.example.com:3128`, i opcjonalnie
  nazwą użytkownika i hasłem. Hasło jest przechowywane w Menedżerze poświadczeń Windows.
  Jeśli Twoja sieć używa skryptu konfiguracji proxy, wpisz proxy w opcji **Ręcznie**.
- **Wygląd → Motyw**: Systemowy, Jasny albo Ciemny.

## Aktualizacje

Program aktualizuje się sam ze strony wydań. Sprawdza przy starcie i co kilka godzin, pobiera nową
wersję w tle i instaluje ją, gdy przez minutę nic nie było drukowane. Zlecenia wysłane w tym czasie
czekają w ICERP i drukują się zaraz potem. Program sam uruchamia się ponownie (w zasobniku, jeśli
tam był), a powiadomienie podaje nową wersję.

**Ustawienia → Aktualizacje** pokazuje zainstalowaną wersję i ostatnie sprawdzenie; **Sprawdź
aktualizacje** (tam albo w menu w zasobniku) sprawdza od razu.

**Sprawdź aktualizacje** w menu w zasobniku odpowiada powiadomieniem, nawet gdy powiadomienia są
wyłączone: program jest aktualny, trwa pobieranie nowej wersji, nowa wersja jest gotowa (zainstaluje
się, gdy nic nie będzie drukowane) albo sprawdzenie się nie udało (przyczyna jest w dzienniku).
Kliknięcie powiadomienia otwiera Ustawienia → Aktualizacje. Automatyczne sprawdzanie i przycisk
w Ustawieniach nie pokazują powiadomienia.

## Co oznaczają stany

**Połączenia** (zakładka Status oraz Ustawienia → Połączenia):

| Stan | Znaczenie | Co zrobić |
|---|---|---|
| **Połączono** | ICERP może wysyłać zlecenia. | Nic. |
| **Łączenie…** | Program łączy się z ICERP. | Poczekaj kilka sekund. |
| **Brak połączenia** | Nie można połączyć się z ICERP; program próbuje dalej. | Sprawdź sieć i proxy. |
| **Klucz odrzucony** | Klucz został unieważniony albo wygenerowany na nowo w ICERP, albo komputer został tam usunięty. | W ICERP wygeneruj nowy klucz dla tego komputera (albo dodaj go ponownie, jeśli został usunięty), potem kliknij **Ustaw w aplikacji** albo wklej ciąg w **Wymień klucz** w Ustawienia → Połączenia. |
| **Klucz innego komputera** | Tego klucza używa już inny komputer. | Dodaj ten komputer osobno w ICERP. |
| **Wymagana aktualizacja** | ICERP potrzebuje nowszej wersji programu. | Program od razu szuka aktualizacji; zobacz [Aktualizacje](#aktualizacje). |

**Drukarki** (zakładka Drukarki): **Gotowa**, **Offline** (włącz ją lub podłącz), **Wymaga uwagi**
(papier, pokrywa, błąd na drukarce), **Nieznany**, **Brak na tym komputerze** (ICERP wciąż ją ma,
ale Windows już jej nie pokazuje).

**Dla połączenia** (kolumna każdego ICERP): **Nieudostępniona** (ICERP jej nie widzi),
**Jeszcze nie wysłano**, **Nieaktywna** (ICERP ją ma, ale jej nie używa), **Aktywna**.

**Zlecenia** (zakładki Status i Logi): **W toku**, **Czeka na drukarkę: …** (drukarka etykiet nie
jest gotowa; zobacz [Sprawdzanie stanu drukarki etykiet](#sprawdzanie-stanu-drukarki-etykiet)),
**Wysłane do drukarki**, **Wydrukowane**, **Nieudane** (z przyczyną).

## Logi i diagnostyka

Zakładka **Logi** ma dwa widoki:

- **Historia zleceń**: każde zlecenie z ostatnich 30 dni, z drukarką, czasem, stanem i, przy
  nieudanym, przyczyną. Zawężają ją **Tylko nieudane**, filtr **Połączenie** i **Szukaj w tytułach**.
- **Log aplikacji**: co program robi, na bieżąco.

**Otwórz folder logów** otwiera dzienne pliki logów (`%LOCALAPPDATA%\pl.icerihub.printer\logs`,
przechowywane 14 dni). **Kopiuj diagnostykę** kopiuje podsumowanie dla osoby, która pomaga: wersje,
połączenia, drukarki i ostatnie błędy. Nie zawiera kluczy; wklej je do wiadomości.

## Typowe problemy

**„System Windows ochronił ten komputer” / przeglądarka blokuje pobieranie.** To normalne dla tego
instalatora; zobacz [Pobieranie i instalacja](#pobieranie-i-instalacja).

**„Ustaw w aplikacji” nic nie robi.** Sprawdź, czy program jest zainstalowany na tym komputerze,
i wklej ciąg połączenia ręcznie (Ustawienia → Połączenia).

**„Ten klucz należy do innego komputera”.** Każdy komputer potrzebuje w ICERP własnego wpisu.
Kliknij w ICERP **Dodaj komputer** dla tego komputera.

**ICERP nie pokazuje drukarek.** Zaznacz je w zakładce Drukarki w programie, sprawdź, czy połączenie
ma stan **Połączono**, i kliknij w ICERP **Odśwież listę drukarek**.

**Zlecenie nieudane z powodu „Drukarka offline”.** Włącz drukarkę lub ją podłącz. Program próbuje
dalej, aż zlecenie wygaśnie w ICERP (domyślnie po minucie); potem wyślij je ponownie.

**Zlecenie nieudane z powodu „Drukarka nie jest gotowa: …”.** Sprawdzanie stanu wykazało, że
drukarka etykiet nie była gotowa (otwarta pokrywa, brak papieru, wstrzymana…), dopóki zlecenie nie
wygasło. Zamknij pokrywę albo załóż rolkę i naciśnij przycisk papieru, potem wyślij je ponownie.
Zobacz [Sprawdzanie stanu drukarki etykiet](#sprawdzanie-stanu-drukarki-etykiet).

**Zlecenia ciągle mają stan „Czeka na drukarkę: Brak odpowiedzi”.** Program nie może się połączyć
z drukarką etykiet: jest wyłączona, odłączona albo nieosiągalna w sieci. Włącz ją lub podłącz;
**Sprawdź teraz** w zakładce Drukarki powinno wtedy pokazać **Gotowa**. Jeśli ta drukarka nigdy nie
może odpowiedzieć, odznacz dla niej sprawdzanie stanu.

**Zlecenie dla Print to PDF albo XPS nigdy się nie kończy.** Drukarka czeka, aż ktoś wybierze nazwę
pliku. Zobacz [Drukarki, które pytają o nazwę pliku](#drukarki-które-pytają-o-nazwę-pliku).

**Drukarki nie ma w Ustawieniach Windows.** Otwórz jej kolejkę albo preferencje z programu; zobacz
[Otwieranie kolejki i preferencji drukarki](#otwieranie-kolejki-i-preferencji-drukarki).

**„Drukarka nieudostępniona dla tego ICERP”.** Zlecenie było dla drukarki, która nie jest
zaznaczona dla tego ICERP w zakładce Drukarki, albo nie wskazywało drukarki, a domyślna drukarka
dla jego rodzaju nie jest udostępniona. Zaznacz ją albo wybierz inną domyślną w Ustawienia →
Drukowanie.

**„Wygasło przed wydrukiem”.** Komputer był wyłączony, uśpiony albo bez sieci, gdy wysłano
zlecenie, albo drukarka cały czas była offline. Wyślij je ponownie.

**Etykieta jest za mała, ucięta albo w złym miejscu.** Ustaw w Windows rozmiar papieru drukarki
etykiet na rozmiar etykiety, a potem użyj **Drukuj stronę testową** i ustawień wydruku (skalowanie,
wypełnienie, położenie, obrót), aż będzie pasować.

**Po restarcie komputera nic się nie drukuje.** Sprawdź **Ustawienia → Uruchamiaj razem
z Windows** i czy program jest w zasobniku.

**Dalej nie działa?** Otwórz zakładkę Logi, kliknij **Kopiuj diagnostykę** i wyślij ją osobie,
która opiekuje się ICERP.

## Odinstalowanie

Ustawienia Windows → Aplikacje → **ICERP Printer** → Odinstaluj. Ustawienia, historia zleceń i logi
zostają, chyba że zaznaczysz **Usuń dane aplikacji**. Klucze zostają w Menedżerze poświadczeń
Windows; usuń też ten komputer w ICERP, aby jego klucz przestał działać.
