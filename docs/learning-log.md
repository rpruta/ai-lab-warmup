## 2026-11-21: PATH, Homebrew, pierwsze repo
- Zadziałało: `which -a git`, `gh repo create`. Zrozumiałem kolejność przeszukiwania PATH.
- Nie zadziałało: literówki (`witch`, `--ad-readme`) i `code` poza PATH. Wniosek: czytać pierwszą linijkę błędu.
- Decyzja: repo publiczne, tylko dane publiczne i syntetyczne.
- Koszt: 0 zł.
- Na później: duplikat `/opt/homebrew/bin` w PATH, dodanie `code` do PATH.

# Learning log

## 2026-11-21: PATH, Homebrew, pierwsze repo
- Zadziałało: `which -a git`, `gh repo create`. Zrozumiałem kolejność przeszukiwania PATH.
- Nie zadziałało: literówki (`witch`, `--ad-readme`) i `code` poza PATH. Wniosek: czytać pierwszą linijkę błędu.
- Decyzja: repo publiczne, tylko dane publiczne i syntetyczne.
- Koszt: 0 zł.
- Na później: duplikat `/opt/homebrew/bin` w PATH, dodanie `code` do PATH.

## 2026-11-22: PATH, symlink i polecenie `code`
- Tryb: standardowy
- Co zrobiłem: zdiagnozowałem, czemu `code` nie działa (`which code`, `ls /Applications`), podpiąłem VS Code symlinkiem do `/opt/homebrew/bin`.
- Co zadziałało: `which`, `ls -l` (strzałka `->` pokazuje cel skrótu), `ln -sf` do podmiany błędnego skrótu.
- Co nie zadziałało i dlaczego: `ln -s "Applications/..."` bez `/` na początku, czyli ścieżka względna; powstał dangling symlink, a `ln` nie zgłosił błędu. Potem `File exists`, bo stary skrót nie jest nadpisywany bez `-f`.
- Nowe pojęcia (3): symlink, ścieżka względna vs bezwzględna, dangling symlink.
- Na później: puste
- Co może pójść źle (bezpieczeństwo): PATH hijacking, czyli podstawienie złośliwego pliku pod znane polecenie w katalogu z PATH. Skrypty i komendy tylko ze znanych źródeł.
- Koszt utrzymania: ok. 0; tylko przeniesienie lub usunięcie VS Code psuje skrót.
- Decyzja: symlink do istniejącej lokalizacji zamiast edycji `$PATH`; duplikat `/opt/homebrew/bin` w PATH zostawiony bez zmian (ADR 0001).
- Następny krok: nawigacja w terminalu (tydzień 2), commit logu przez branch.
- Czego się nauczyłem dodatkowo: `$PATH` składa się z `path_helper` (`/etc/paths`, `/etc/paths.d`) i z plików startowych (`~/.zprofile`), stąd duplikat.

## 2026-11-23: nawigacja w terminalu (pwd, cd, ls -a)
- Tryb: standardowy
- Co zrobiłem: powtórka PATH/symlinków (słabo, brak powtórki wczoraj), potem `pwd`, `cd ~`, `cd projects/ai-lab-warmup` (ścieżka względna), `ls` vs `ls -a`.
- Co zadziałało: czytanie ścieżki od lewej do prawej (`/` → Users → rafal → projects → ai-lab-warmup), wyłapanie błędu w komendzie przed Enterem po wskazówce.
- Co nie zadziałało i dlaczego: samo `~` (zsh próbuje uruchomić katalog jako program, stąd `permission denied`); `cd ~ pwd` w jednej linii (dwa argumenty zamiast dwóch komend); `/project/...` (ścieżka bezwzględna z literówką, a ja chciałem względną).
- Nowe pojęcia (3): `pwd`, `cd` (ścieżka względna vs bezwzględna w praktyce), `ls -a` (ukryte pliki).
- Na później: `cd` z dwoma argumentami w zsh; alias `ls` (sprawdzić `type ls`); duplikat `/opt/homebrew/bin` w PATH (hipoteza: podwójne `brew shellenv` w ~/.zprofile i ~/.zshrc, sprawdzić `grep -n "brew shellenv" ~/.zprofile ~/.zshrc`).
- Co może pójść źle (bezpieczeństwo): `.env` jest ukryty, więc `ls` go nie pokaże, a `git add .` może go dodać do commita. W repo publicznym klucz wycieka w minuty, a usunięcie pliku nie czyści historii. Klucz, który wyciekł, unieważniam.
- Koszt utrzymania: 0 zł dziś. Przy pierwszym kluczu API ustawić limit wydatków i alert.
- Decyzja: brak nowego ADR. Hipotezę o PATH zweryfikować, zanim trafi do ADR.
- Następny krok: powtórka PATH/symlink bez notatek (5 min), potem commit logu przez branch.