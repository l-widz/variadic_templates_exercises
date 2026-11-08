# Variadic templates i fold expressions — zadania

Pięć zadań na zajęcia: dwa najprostsze, jedno konkretne i dwa praktyczne.

## 1. Suma kwadratów i lewostronna redukcja

**Najprostsze.** W `zadanie1/main.cpp` zdefiniuj:
- pomocniczą funkcję `square(T x)` zwracającą `x * x`;
- szablon funkcji `sum_of_squares(Ts... xs)` zwracający sumę kwadratów wszystkich przekazanych argumentów za pomocą binarnego fold expression (dla pustej paczki zwraca `0`);
- szablon funkcji `reduce_from(T start, Ts... xs)` odejmujący od wartości początkowej `start` wszystkie kolejne argumenty od lewej do prawej: `((start - x1) - x2) - ...` (użyj binarnego lewego fold expression).

W `main.cpp` sprawdź:
- `sum_of_squares()` -> `0`;
- `sum_of_squares(3, 4)` -> `25`;
- `sum_of_squares(1, 2, 3, 4)` -> `30`;
- `reduce_from(100, 10, 25, 5)` -> `60`;
- `reduce_from(50)` -> `50`.

## 2. Podzielność, ujemne wartości i łączny rozmiar typów

**Najprostsze.** W `zadanie2/main.cpp` zaimplementuj:
- szablon funkcji `all_divisible_by(int divisor, Ts... xs)` sprawdzający za pomocą fold expression po operatorze `&&`, czy każdy argument z paczki dzieli się bez reszty przez `divisor` (dla pustej paczki zwraca `true`);
- szablon funkcji `any_negative(Ts... xs)` sprawdzający za pomocą fold expression po operatorze `||`, czy którykolwiek z przekazanych argumentów jest mniejszy od zera (dla pustej paczki zwraca `false`);
- szablon zmiennej `template <typename... Ts> inline constexpr std::size_t total_sizeof_v` obliczający za pomocą binarnego fold expression sumę rozmiarów `sizeof(Ts)` wszystkich typów w paczce (dla pustej paczki `0`).

W `main.cpp` sprawdź:
- `all_divisible_by(3, 3, 6, 12, -9)` -> `true`;
- `all_divisible_by(3, 3, 7, 12)` -> `false`;
- `all_divisible_by(5)` -> `true`;
- `any_negative(1, 0, -2, 5)` -> `true`;
- `any_negative(1, 2, 3)` -> `false`;
- `total_sizeof_v<char, char, char>` -> `3`, `total_sizeof_v<>` -> `0`.

## 3. Minimum z paczki i przycinanie zmiennych do zakresu

**Konkretne.** W `zadanie3/main.cpp` wykorzystaj fold expression po operatorze przecinka:
- napisz szablon funkcji `min_value(const T& first, const Rest&... rest)`, który przyjmuje co najmniej jeden argument i zwraca najmniejszą wartość spośród przekazanych elementów;
- napisz szablon funkcji `clamp_all(const T& low, const T& high, Refs&... vars)`, który przyjmuje dolną i górną granicę oraz dowolną liczbę zmiennych przez referencję, a następnie przycina każdą zmienną do przedziału `[low, high]` (wartości mniejsze niż `low` ustawia na `low`, a większe niż `high` na `high`).

W `main.cpp` sprawdź:
- `min_value(5, 2, 8, -3, 4)` -> `-3`;
- `min_value(42)` -> `42`;
- dla zmiennych `int a = -5, b = 4, c = 15, d = 10` po wywołaniu `clamp_all(0, 10, a, b, c, d)` ich wartości wynoszą odpowiednio `0, 4, 10, 10`.

## 4. Budowanie ścieżki URL i wiersza CSV

**Praktyczne.** W `zadanie4/main.cpp` wykorzystaj `std::ostringstream` oraz fold expressions:
- napisz szablon funkcji `build_url_path(const Args&... segments)` zwracający `std::string`, który dokleja przed każdym segmentem znak `'/'` (np. dla argumentów `"api"`, `"v1"`, `"users"`, `42` zwraca `"/api/v1/users/42"`, a dla pustej paczki zwraca `"/"`);
- zdefiniuj strukturę `Product { std::string name; double price; }` wraz z przeciążonym `operator<<` wypisującym produkt w formacie `"nazwa:cena"`;
- napisz szablon funkcji `to_csv_line(const T& first, const Rest&... rest)` zwracający `std::string`, w którym kolejne argumenty są rozdzielone średnikiem `';'` (bez średnika na końcu).

W `main.cpp` sprawdź i wypisz na ekranie:
- `build_url_path("api", "v1", "items", 105)` -> `"/api/v1/items/105"`;
- `build_url_path()` -> `"/"`;
- `to_csv_line(1, Product{"Chleb", 4.5}, "dostepny")` -> `"1;Chleb:4.5;dostepny"`.

## 5. System zdarzeń gry z `overloaded` i `std::visit`

**Praktyczne.** W `zadanie5/main.cpp` zdefiniuj trzy struktury reprezentujące akcje zmieniające punkty gracza:
- `AddPoints { int amount; }` — dodaje `amount` do wyniku;
- `MultiplyPoints { int factor; }` — mnoży bieżący wynik przez `factor`;
- `ResetPoints {}` — zeruje wynik.

Zdefiniuj typ `using Event = std::variant<AddPoints, MultiplyPoints, ResetPoints>;` oraz szablon struktury `overloaded` dziedziczący po paczce lambd. Napisz funkcję `int calculate_score(int initial_score, const std::vector<Event>& events)`, która przechodzi po wektorze zdarzeń i za pomocą `std::visit` oraz `overloaded` aktualizuje wynik.

W `main.cpp` sprawdź:
- dla `initial_score = 10` i listy zdarzeń `{AddPoints{5}, MultiplyPoints{3}, AddPoints{-10}, ResetPoints{}, AddPoints{7}}`:
  - po pierwszych trzech zdarzeniach wynik wynosi `35` (`(10 + 5) * 3 - 10`);
  - po wykonaniu całej listy wynik końcowy wynosi `7`.
