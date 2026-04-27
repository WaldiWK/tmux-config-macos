# tmux-macos-config

Konfiguracja tmux dla macOS z działającym kopiowaniem do schowka systemowego.

## Problem

Na macOS domyślny tmux nie kopiuje tekstu do systemowego schowka (Cmd+V). 
Po wejściu w tryb kopiowania (`Ctrl+B [`) spacja nie działa prawidłowo – 
zamiast zaznaczać tekst, przewija stronę w dół.

## Rozwiązanie

Ten plik `.tmux.conf`:
- włącza tryb kopiowania w stylu **vi** (spacja = zaznaczanie)
- konfiguruje mostek do schowka przez `reattach-to-user-namespace`
- dodaje wygodne skróty klawiszowe

## Wymagania

- macOS
- tmux (wersja 1.8 lub nowsza) – sprawdź: `tmux -V`
- **`reattach-to-user-namespace`** – mostek do schowka (patrz instalacja poniżej)

## Instalacja

### 1. Zainstaluj mostek do schowka

**MacPorts:**
sudo port install tmux-pasteboard

**Homebrew:**
brew install reattach-to-user-namespace

Sprawdź, czy działa:
which reattach-to-user-namespace

### 2. Pobierz plik konfiguracyjny

curl -o ~/.tmux.conf https://raw.githubusercontent.com/TWOJA_NAZWA_UZYTKOWNIKA/tmux-macos-config/main/tmux.conf

Lub ręcznie: skopiuj plik `tmux.conf` z tego repozytorium do `~/.tmux.conf`

### 3. Przeładuj konfigurację

Jeśli tmux już działa:
tmux source-file ~/.tmux.conf

Lub zrestartuj tmux:
tmux kill-server
tmux

## Jak używać

| Skrót | Działanie |
|-------|-----------|
| Ctrl+B [ | Wejdź w tryb kopiowania |
| Spacja | Rozpocznij zaznaczanie |
| Strzałki | Zaznacz tekst |
| y | Skopiuj do schowka |
| Cmd+V | Wklej w dowolnej aplikacji |

**Uwaga:** używaj `y`, nie `Enter`. `Enter` tylko wychodzi z trybu kopiowania bez zapisu.

## Testowanie

Sprawdź, czy mostek działa:
echo "test" | reattach-to-user-namespace pbcopy

Następnie naciśnij Cmd+V – powinno pojawić się "test".

## Rozwiązywanie problemów

**Kopiowanie nie działa?**
1. Sprawdź, czy reattach-to-user-namespace jest zainstalowane: which reattach-to-user-namespace
2. Przetestuj mostek ręcznie (patrz wyżej)
3. Upewnij się, że używasz y, a nie Enter

**Cmd+V nie wkleja?**
Upewnij się, że w ~/.tmux.conf jest linia: set -g extended-keys off

## Licencja

BSD 2-Clause

## Autor

[Waldemar Jacek Kuranc]
