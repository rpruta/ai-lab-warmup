# 📘 Podręcznik AI Lab

Wiedza „jak to się robi", ułożona jak książka kucharska: jedno pytanie = jeden wpis.

> [!NOTE]
> **Log** (`learning-log.md`) mówi, co się działo. **Ten plik** mówi, jak to zrobić. Uzupełniamy go po każdych zajęciach.

## 🧩 Legenda ramek

> [!NOTE]
> 🔵 **Model mentalny**: jak to działa pod spodem.

> [!TIP]
> 🟢 **Jak sprawdzić**: jedna komenda lub obserwacja, że działa.

> [!WARNING]
> 🟡 **Na co uważać**: błędy, na które już wpadłem.

> [!CAUTION]
> 🔴 **Bezpieczeństwo / koszt**: rzeczy, które kosztują naprawdę drogo.

> [!IMPORTANT]
> 🟣 **Zasada**: coś, co robimy zawsze.

## 🧱 Szablon wpisu

1. **❓ Pytanie**: po ludzku, tak jak byś zapytał kolegę.
2. **🎯 Kiedy tego użyć**: w jakiej sytuacji sięgasz po ten wpis.
3. **🔵 Model mentalny**: jedno–dwa zdania z analogią.
4. **🪜 Kroki**: numerowane; przy każdym komenda, co robi, czego się spodziewać.
5. **🟡 / 🔴 Ramki ostrzeżeń** przy krokach, w których można się pomylić.
6. **🟢 Jak sprawdzić**.
7. **🧠 Sprawdź się**: 3 pytania z zakrytymi odpowiedziami (do powtórek).
8. **🔗 Powiązane**.

## 📑 Spis treści

1. [Jak przesłać zmianę do repo na GitHubie](#1-jak-przesłać-zmianę-do-repo-na-githubie)
2. [Skąd zsh wie, który program uruchomić](#2-skąd-zsh-wie-który-program-uruchomić-path-i-symlinki)

---

## 1. Jak przesłać zmianę do repo na GitHubie

**🎯 Kiedy tego użyć:** zmieniłem lub dodałem plik lokalnie i chcę, żeby trafił do repo na GitHubie.

> [!NOTE]
> 🔵 **Model mentalny.** Lokalne repo na Macu i repo na GitHubie to dwa osobne egzemplarze (jak oryginał i ksero). Zmiana w jednym nie pojawia się w drugim, dopóki jej nie przeniesiesz ręcznie: `push` w jedną stronę, `pull` w drugą.

### 🪜 Kroki

**Krok 1: Sprawdź stan.**

```
git status
```

Pokazuje, co jest zmienione i co jest już przygotowane do commita.

> [!WARNING]
> 🟡 Git pokazuje cały nowy folder jako jedną pozycję, a nie pliki w środku.

**Krok 2: Utwórz branch na tę zmianę.**

```
git switch -c typ/krotka-nazwa
```

Przykład: `docs/learning-log`. `-c` = create. Prompt pokaże nową nazwę gałęzi zamiast `main`.

> [!WARNING]
> 🟡 Nieśledzone pliki nie należą do żadnej gałęzi, więc przechodzą z Tobą.

**Krok 3: Zobacz, co dokładnie dodasz.**

```
ls -a ścieżka/folderu
```

`-a` pokazuje też ukryte pliki.

> [!CAUTION]
> 🔴 **Bezpieczeństwo.** `.env` jest ukryty i zwykłe `ls` go nie pokaże. W repo publicznym klucz z commita wycieka w minuty, a usunięcie pliku nie czyści historii. Wyciekły klucz = **unieważnić klucz**.

**Krok 4: Dodaj do commita tylko konkretne pliki.**

```
git add ścieżka/do/pliku
```

Plik trafia do „staged" (w prompcie pojawia się `+`).

> [!CAUTION]
> 🔴 Nie używaj `git add .` bez sprawdzenia `git status`. Bierze wszystko naraz, łącznie z tym, czego nie chciałeś.

**Krok 5: Zrób commit.**

```
git commit -m "typ: opis zmiany"
```

Format Conventional Commits. Typ to np. `feat`, `fix`, `docs`. Opis w trybie rozkazującym.

> [!IMPORTANT]
> 🟣 Opis mówi **co zmienia repo**, a nie co robisz z gitem. ✅ `docs: add learning log` ❌ „dodanie do commitu pliku".

**Krok 6: Wyślij branch na GitHuba.**

```
git push -u origin typ/krotka-nazwa
```

`origin` to zdalne repo, `-u` zapamiętuje powiązanie lokalnej gałęzi ze zdalną. Na końcu wyniku jest link do utworzenia Pull Requesta.

**Krok 7: Utwórz Pull Request** (w przeglądarce, link z kroku 6).

Tytuł z commita. Opis w trzech częściach: **Co** (co dodaje), **Dlaczego** (po co, nie „bo dodaję plik"), **Jak sprawdzić** (zakładka Files changed). Kliknij *Create pull request*.

**Krok 8: Zrób merge.**

*Merge pull request* → *Confirm merge*. Opcjonalnie *Delete branch*.

> [!WARNING]
> 🟡 PR i merge to dwa osobne kliknięcia, więc możesz się jeszcze zatrzymać.

**Krok 9: Zsynchronizuj lokalny `main`.**

```
git switch main
git pull
```

> [!WARNING]
> 🟡 Komunikat „merged" dotyczy GitHuba, a nie Twojego Maca. `git status` pisze „na bieżąco z origin/main", ale to wiedza z ostatniego kontaktu z GitHubem, a nie sprawdzenie na żywo.

> [!TIP]
> 🟢 **Jak sprawdzić.** Po `git pull` na `main` plik jest na dysku: `ls ścieżka`.

### 🧠 Sprawdź się

**1.** Skończyłeś merge na GitHubie. Czy `main` na Twoim Macu ma już ten plik? Dlaczego?

<details>
<summary>Odpowiedź</summary>

Nie. Lokalne repo i GitHub to dwa osobne egzemplarze (oryginał i ksero). Trzeba zrobić `git switch main` i `git pull`.
</details>

**2.** Czemu `git add .` jest groźniejsze niż `git add plik`?

<details>
<summary>Odpowiedź</summary>

Bierze wszystko naraz, także ukryte pliki jak `.env`. W publicznym repo klucz wycieka w minuty, a usunięcie pliku nie czyści historii.
</details>

**3.** Oceń wiadomość commita „dodanie do commitu pliku learning-log". Co jest nie tak i jak by wyglądała dobra?

<details>
<summary>Odpowiedź</summary>

Brak typu i opis czynności zamiast zmiany. Dobra: `docs: add learning log`.
</details>

**🔗 Powiązane:** wpis 2; do dopisania: `.gitignore` i `.env.example`.

---

## 2. Skąd zsh wie, który program uruchomić (PATH i symlinki)

**🎯 Kiedy tego użyć:** komenda „not found", dwie wersje tego samego programu, albo pytanie „co się naprawdę uruchamia".

> [!NOTE]
> 🔵 **Model mentalny.** `PATH` to spis treści: lista katalogów (nie plików), oddzielonych dwukropkami. zsh przeszukuje je od lewej do prawej i uruchamia pierwszy trafiony plik. Symlink to skrót na pulpicie: wskazuje na prawdziwy plik, ale nim nie jest. Kopia, w przeciwieństwie do skrótu, żyje własnym życiem.

### 🪜 Kroki

**Krok 1: Podejrzyj PATH.**

```
echo $PATH
```

`$` znaczy „daj wartość zmiennej". Samo `PATH` zsh potraktuje jak nazwę programu.

**Krok 2: Sprawdź, który plik się uruchomi.**

```
type -a git
```

Pokaże wszystkie trafienia w kolejności z PATH, pierwsze wygrywa.

> [!WARNING]
> 🟡 Do zweryfikowania u siebie, zanim wejdzie do podręcznika na stałe.

**Krok 3: Zobacz, czy to symlink.**

```
ls -l ścieżka/do/pliku
```

Pierwsza litera `l` i strzałka `->` oznaczają symlink, a po strzałce stoi cel (prawdziwy plik).

> [!WARNING]
> 🟡 Kolejność w PATH rozstrzyga: Homebrew wstawia swój katalog na początek, żeby jego nowszy program wygrywał z systemowym. Symlink wskazujący w próżnię to *broken symlink*. Homebrew trzyma programy w `Cellar/nazwa/wersja` i tylko przepina symlink przy aktualizacji, a stara wersja zostaje obok.

> [!TIP]
> 🟢 **Jak sprawdzić.** `ls -l /opt/homebrew/bin/git` pokazuje strzałkę do `../Cellar/git/<wersja>/bin/git`.

### 🧠 Sprawdź się

**1.** Skąd zsh wie, który plik uruchomić po wpisaniu `git`?

<details>
<summary>Odpowiedź</summary>

Przeszukuje katalogi z `PATH` od lewej do prawej i uruchamia pierwszy trafiony plik.
</details>

**2.** Masz `git` w `/opt/homebrew/bin` i w `/usr/bin`. Który się uruchomi?

<details>
<summary>Odpowiedź</summary>

Ten z katalogu, który jest wcześniej (bardziej na lewo) w PATH.
</details>

**3.** Po co Homebrew trzyma w `bin` tylko symlink, a prawdziwy plik w `Cellar/git/<wersja>`?

<details>
<summary>Odpowiedź</summary>

Przy aktualizacji instaluje nową wersję obok starej i tylko przepina symlink. PATH się nie zmienia, a stara wersja zostaje na wypadek problemów.
</details>

**🔗 Powiązane:** do dopisania: duplikat `/opt/homebrew/bin` w PATH (hipoteza do sprawdzenia).
