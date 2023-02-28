1. W pliku `init.py` napisz funkcję `initialize()`, która wczyta pliki konfiguracyjne obu typów postaci a następnie na ich podstawie utworzy listy instancji klas `Human` oraz `Zombie`. Pamiętaj o konieczności wylosowania wartości atrybutów używając rozkładu normalnego. Niech funkcja zwróci obie te listy.

---
2. W pliku `main.py`, który będzie głównym skryptem do uruchamiania symulacji:
 - utwórz tablicę 2D numpy o wymiarach 100x100, która będzie składała się z samych zer. Będzie to mapa symulacji
 - wywołaj funkcję `initialize()` i przechwyć obie listy postaci do zmiennych
 - wywołaj funkcję `run_simulation()` z pliku `simulation.py`, która powstanie dopiero później

---
3. W pliku `visualization.py` napisz funkcję `visualize_simulation()`. Niech przyjmuje następujące parametry:
 - `humans` (lista instancji klasy `Human`) 
 - `zombies` (lista instancji klasy `Zombie`)
 - `map2d` (dwuwymiarowa tablica - mapa symulacji)
 - `t` (`int` - numer iteracji)

Funkcja ta powinna:
- Utworzyć kopię mapy (aby nie nadpisać oryginału)
- Nanieść na mapę (czyli macierz) wszystkie postaci bazując na ich położeniu (x, y). Niech każda klasa postaci będzie oznaczona inną liczbą z przedziału (0, 1), np. 0.8 dla ludzi i 0.5 dla zombie. Dany punkt (x, y) na mapie (macierzy) powinien otrzymać taką właśnie wartość 
- Utworzyć wykres (heatmapę) i nadać jej tytuł zawierający w sobie numer iteracji. Aby wyświetlić wykres użyj funkcji `plt.show()`
- Odczekać chwilę za pomocą funkcji `plt.pause()` 

---
4. W pliku `simulation.py` napisz funkcję `run_simulation()`, która przyjmie następujące parametry:
- `humans` (lista instancji klasy `Human`)
- `zombies` (lista instancji klasy `Zombie`)
- `map2d` (dwuwymiarowa tablica - mapa symulacji)

Funkcja ta będzie wywołana w pliku `main.py` i odbędzie się w niej cała symulacja. Zacznij od zdefiniowania zmiennej, która będzie licznikiem iteracji głównej pętli.

Następnie napisz pętlę nieskończoną, z której wyjdziemy pod jednym z poniższych warunków:
- liczba ludzi będzie wynosiła 0
- liczba zombie będzie wynosiła 0
- licznik iteracji przekroczy określoną wartość, np. 1000

Wewnątrz tej pętli powinny wydarzyć się następujące akcje:
- Inkrementacja licznika iteracji
- Każda z postaci powinna wybrać dokąd przemieści się w kolejnej iteracji
- Kiedy wszystkie postacie dokonają wyboru dopiero wtedy należy je przemieścić
- Walka postaci (o ile są od siebie odpowiednio blisko, np. 3 jednostki odległości)

W celu odbycia starć pomiędzy postaciami wklej poniższy kod:
```
clash_pairs = find_all_pairs_about_to_clash(humans, zombies)

rivals_number = calculate_n_of_rivals(humans, zombies, clash_pairs)

victories, loosers = carry_out_clashes(
    humans, zombies, clash_pairs, rivals_number, t)

implement_results(humans, zombies, victories, loosers)
```

Poszczególne funkcje zaimplementowane zostaną w następnej części zadań.
