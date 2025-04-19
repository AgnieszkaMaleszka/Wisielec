# 🎮 Wisielec – sieciowa gra słowna

**Autorzy:**  
- 📌 Agnieszka Maleszka
- 📌 Bartosz Kozłowski 

Gra sieciowa z wykorzystaniem **BSD sockets**, w której gracze rywalizują w odgadywaniu haseł, zdobywając punkty i premie za szybkość. Gra wspiera wielu graczy, dynamiczne dołączanie do rozgrywki, opóźnienia sieciowe oraz rozłączenia.

---

## 🖼️ Zrzuty ekranu

<img width="788" alt="Wisielec2" src="https://github.com/user-attachments/assets/335f9732-4c97-4cf9-a85f-1bd81a4ed3ce" />

<img width="786" alt="Wisielec4" src="https://github.com/user-attachments/assets/658f8e26-cc16-4b89-965d-a8a917fe9734" />

---

## 🔧 Wymagania systemowe

- Kompilator `g++` w wersji **10.x.x**
- Standard języka **C++17** lub nowszy
- CMake (minimum 3.10)
- Biblioteka **Qt** (do klienta graficznego)
- System wspierający BSD sockets (Linux / macOS)

---

## 🚀 Instrukcja uruchomienia

1. **Przejdź do katalogu projektu:**
   ```bash
   cd Hangman-main
   ```

2. **Utwórz katalog `build`:**
   ```bash
   mkdir build
   cd build
   ```

3. **Wygeneruj pliki projektu za pomocą CMake i zbuduj aplikację:**
   ```bash
   cmake ..
   cmake --build .
   ```

4. **Uruchom serwer i klienta w osobnych terminalach:**
   - **Serwer:**
     ```bash
     cd serwer
     ./serwer
     ```
   - **Klient:**
     ```bash
     cd client
     ./client
     ```

---

## 🕹️ Opis działania gry

- Gracz łączy się z serwerem i podaje **unikalny nick**. Jeśli nick jest zajęty – proszony jest o zmianę.
- Po zaakceptowaniu nicku, gracz trafia do **menu głównego** i może dołączyć do **jednego wspólnego pokoju gry**.
- W pokoju widoczna jest **lista aktywnych graczy**, ich aktualny stan wisielca oraz zgromadzone punkty.

### 🧩 Zasady rozgrywki:

- Hasło reprezentowane jest jako **puste linie**, jedna dla każdej litery.
- Gracze na zmianę zgadują litery. Za każdą poprawną literę przyznawany jest punkt.
- Tura kończy się, gdy:
  - upłynie **1,5 minuty**,
  - wszyscy popełnią maksymalną liczbę błędów,
  - wszyscy odgadną hasło.
- Po odgadnięciu hasła przez jednego z graczy, pozostali mają **20 sekund** na odpowiedź (chyba że pozostały czas jest krótszy).
- Gracze mogą dołączać do trwającej gry, ale udział biorą dopiero w następnej rundzie.
- **Premie punktowe** przyznawane są za odgadnięcie całego hasła, w zależności od szybkości.

### 🧠 Dodatkowe informacje:

- Gra rozpoczyna się automatycznie po dołączeniu **min. dwóch graczy**.
- Każde hasło należy do określonej **kategorii**, którą widać w trakcie rozgrywki.
- W przypadku rozłączenia gracza w trakcie tury:
  - tura kontynuuje się bez niego,
  - jeśli pozostanie tylko jeden gracz, tura dobiega końca, a gracz trafia do poczekalni.
- Jeśli kilku graczy odgadnie hasło **jednocześnie**, otrzymują taką samą premię.

---

## 🌐 Wsparcie dla sieci rozległych

Projekt został zaprojektowany z myślą o działaniu w sieciach internetowych:

- Obsługa **opóźnień sieciowych** oraz **braku odpowiedzi** z `connect()` (np. przy filtrze firewall).
- Możliwość **dowolnego dołączania/rozłączania graczy** w dowolnym momencie gry.
- Stabilność serwera przy **nagłych zerwaniach połączeń**.
- Możliwość **bezczynności graczy** (np. brak odpowiedzi przez całą turę).

---

## 🛠️ Technologie

- **C/C++ + BSD sockets** – obsługa komunikacji sieciowej po TCP
- **Qt** – frontend klienta (GUI)
- **CMake** – system budowania projektu
