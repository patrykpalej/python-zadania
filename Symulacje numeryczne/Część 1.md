1. Stwórz następującą strukturę projektu. Na razie wszystkie pliki powinny być puste.

```
├── conf/
│   ├── human.json
│   └── zombie.json
|
├── src/
│   ├── classes/
│   │   ├── common.py
│   │   ├── human.py
│   │   └── zombie.py
|   |
│   ├── fight_functions.py
│   ├── init.py
│   ├── main.py
│   ├── visualization.py
│   └── simulation.py
|
├── requirements.txt
```

Następnie utwórz w tej lokalizacji projekt PyCharma wybierając jako środowisko `virtualenv`.

---
2. Do plików konfiguracyjnych .json zapisz słowniki stworzone według następujących instrukcji. Dla każdej klasy postaci słownik powinien zawierać poniższe klucze:
- `initial_number` (*int*) - ilu ludzi/zombie będzie na początku symulacji
- `x` (*list*) - początkowe położenie ludzi/zombie wzdłuż osi *x* wyrażone w postaci dwuelementowej listy. Zakładamy, że współrzędna *x* będzie losowana z rozkładu normalnego o określonej średniej oraz odchyleniu standardowym. Wartości średniej oraz odchylenia standardowego powinny znaleźć się w liście pod tym kluczem słownika
- `y` (*list*) - średnia i odchylenie standardowe dla współrzędnej y
- `velocity` (*list*) - średnia i odchylenie standardowe dla prędkości
- `power` (*list*) - średnia i odchylenie standardowe dla siły

---
3. W plikach w folderze `classes` napisz klasy dla poszczególnych typów postaci. Ich atrybuty powinny być następujące:
- x
- y
- velocity
- power
- n_killed / n_infected

Niech w pliku common.py znajdzie się klasa bazowa, po której będą dziedziczyć klasy Human oraz Zombie. W klasie bazowej powinny znaleźć się wspólne dla obu klas atrybuty a także metoda `move()`, która będzie przyjmować jako argumenty `delta_x` i `delta_y`. O takie odległości należy przemieścić postać (zmienić jej współrzędne).

Ponadto klasy dziedziczące powinny mieć metodę `choose_new_position()` (każda klasa swoją). Niech te metody wyznaczają oraz zwracają `delta_x` i `delta_y`, które będą użyte w `move()`. W każdej klasie `choose_new_position()` powinna przyjmować jako argument listę instancji klasy przeciwnika.

Logika obu klas postaci niech będzie następująca:
- Wyznaczyć wszystkie wektory prowadzące od mojego położenia do położeń moich przeciwników
- Znormalizować te wektory do długości 1. Oznacza to, że powinny dalej wskazywać w tym samym kierunku ale niech będą tak przeskalowane, że długość każdego to dokładnie 1
- Każdy ze znormalizowanych wektorów przemnożyć przez wagę określającą w jakim stopniu chcę iść w kierunku danego przeciwnika. Załóżmy, że suma moich atrybutów *power* oraz *n_killed / n_infected* to moje "punkty walki". Podobnie dla moich przeciwników. To jaką przewagę mam nad przeciwnikiem jest proporcjonalne do tego jak bardzo chcę podążać w jego kierunku
- Zsumować wektory wskazujące na poszczególnych przeciwników. Następnie znormalizować wynik oraz przemnożyć go przez atrybut `velocity`

Powyższy algorytm mógłby oczywiście różnić się dla poszczególnych klas postaci, ale niech dla uproszczenia będzie taki sam. 
