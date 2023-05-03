1. Zaimplementuj funkcję `find_all_pairs_about_to_clash()` w pliku `fight_functions.py`. Powinna ona działać w następujący sposób. Zakładamy że ludzie oraz zombie to listy instancji właściwych klas. Funkcja powinna przyjąć jako argumenty te dwie listy a zwrócić powinna listę par indeksów postaci, które będą musiały stoczyć walkę. Kryterium aby dana para człowiek-zombie miała w danej iteracji stoczyć walkę jest to że odległość między nimi jest mniejsza niż pewna stała wartość, np. 3. Niech identyfikatorami postaci będą ich indeksy na listach.

Podpowiedź: użyj podwójnej pętli for

Przykład:
```
humans = [Human(x=1, y=0), Human(x=10, y=40), Human(x=0, y=1)]
zombies = [Zombie(x=30, y=50), Zombie(x=0, z=0)]

result = [(0, 1), (2, 1)]   # człowiek nr 0 i zombie nr 1, człowiek nr 2 i zombie nr 1
```

---
2. Zaimplementuj funkcję `calculate_n_of_rivals()` w pliku `fight_functions.py`. Powinna ona działać w następujący sposób. Niech funkcja ta przyjmuje trzy argumenty: dwie listy (`humans`, `zombies`) z poprzedniego zadania oraz output funkcji z poprzedniego zadania. Niech zwraca informację o liczbie rywali z jakimi ma zmierzyć się każda postać. Forma outputu powinna być jak w poniższym przykładzie:

```
humans = [Human(x=1, y=0), Human(x=10, y=40), Human(x=0, y=1)]
zombies = [Zombie(x=30, y=50), Zombie(x=0, z=0)]
clashing_pairs = [(0, 1), (2, 1)]

result = {"humans": [1, 0, 1], "zombies": [0, 2]}
```

Podpowiedź: zacznij od zainicjalizowania wynikowego słownika z listami samych zer a następnie iterując po `clashing_pairs` inkrementuj stopniowo poszczególne elementy list w tym słowniku


---
3. Napisz funkcję `carry_out_clashes()`. Powinna ona przyjmować następujące argumenty:
- `humans`  - lista instancji klasy `Human`
- `zombies` - lista instancji klasy `Zombie`
- `clashing_pairs` - output funkcji z zadania 1
- `rivals_number` - output funkcji z zadania 2

oraz zwracać:
- victories - słownik o następującej strukturze:
```
{'humans': [0, 0, 0, 1, 0], 'zombies': [1, 0, 2, 0, 0]}
```
gdzie pod kluczami 'humans' i 'zombies' znajdują się listy odpowiadające listom instancji tych klas przy czym wartości w tej liście oznaczają ile zwycięstw odniosła dana postać w tej iteracji.

- loosers - słownik o następującej strukturze:
```
{'humans': [3, 3, 1], 'zombies': [2]}
```
gdzie pod kluczami 'humans' i 'zombies' znajdują się listy indeksów postaci, które przegrały starcie w tej iteracji. Jeśli jakaś postać przegrała więcej niż jedno starcie, jej indeks może się powtarzać.

Przyjmij że dla każdej walki decyduje to, dla której postaci następująca metryka przyjmuje większą wartość.

```
(power + experience) / n_rivals
```

---
4. Napisz funkcję `implement_results()`. Powinna ona przyjmować następujące argumenty:
- `humans`  - lista instancji klasy `Human`
- `zombies` - lista instancji klasy `Zombie`
- `victories` - output funkcji z zadania 3
- `loosers` - output funkcji z zadania 3

i niczego nie zwracać. Zamiast tego będzie modyfikować listy `humans` i `zombies` na podstawie wyników walk:
- człowiek, który przegrał zamienia się w zombie. Jego atrybuty będą mieć dotychczasową wartość, jedynie `n_infected` będzie równe 0 
- zombie który przegrał ginie
- każda postać która wygrała starcie dostaje +1 punkt doświadczenia
