# Variadic templates i fold expressions - zadania

Pięć [zadań na zajęcia](zadania.md): dwa najprostsze, jedno konkretne i dwa praktyczne.

- [Zadanie 1](zadanie1): suma kwadratów oraz lewostronna redukcja za pomocą binarnych fold expressions.
- [Zadanie 2](zadanie2): sprawdzanie podzielności, wykrywanie liczb ujemnych oraz łączny rozmiar typów w bajtach.
- [Zadanie 3](zadanie3): wyznaczanie minimum z paczki argumentów oraz przycinanie zmiennych do zadanego przedziału przez fold po przecinku.
- [Zadanie 4](zadanie4): budowanie ścieżki URL i wiersza CSV za pomocą `std::ostringstream` oraz fold expressions.
- [Zadanie 5](zadanie5): przetwarzanie strumienia zdarzeń za pomocą wzorca `overloaded` i `std::visit`.

Wymagany jest kompilator obsługujący **C++17** (lub nowszy) oraz **CMake >= 3.16**.
## Budowanie zadania

W katalogu głównym projektu (na przykładzie `zadanie1`):

```sh
cmake -S zadanie1 -B zadanie1/build
cmake --build zadanie1/build
```

Uruchomienie programu na Linux/macOS:

```sh
./zadanie1/build/program
```

Uruchomienie programu na Windowsie w PowerShell:

```powershell
.\zadanie1\build\Debug\program.exe
```
