**Polski** · [English](README.en.md)

---

# Matura z informatyki, poziom rozszerzony - kurs Python, część 4. "Instrukcje warunkowe"

> ### 🎬 Wideo z omówieniem
> Pełne omówienie tej części kursu krok po kroku znajdziesz na moim kanale YouTube:
> **[Link do filmu na YouTube](https://youtu.be/VbAC_1ebf8I)**
>
> Na filmie przypominam warunki logiczne i pokazuję operator `not`, zapis przedziałów oraz leniwe obliczanie. Potem omawiam instrukcje `if`, `if ... else` i `if ... elif ... else`, wyrażenie warunkowe, instrukcję `match` oraz funkcje `min`, `max` i `abs`.

---

## Opis

Kod do czwartej części kursu języka Python, który przygotowuje do matury z informatyki na poziomie rozszerzonym.

We wcześniejszych częściach kursu pokazałem, jak przechowywać w zmiennych dane różnego rodzaju i jak wykonywać na nich obliczenia. Ta część dotyczy instrukcji warunkowych, czyli podejmowania decyzji w programie. Program wykonuje różne operacje w zależności od tego, jaka wartość jest zapisana w zmiennej.

W repozytorium są też pliki z poprzednich części kursu. Kod omawiany w tym nagraniu znajduje się w pliku `app-4-instrukcje-warunkowe.py`.

Następna część kursu dotyczy pętli.

## Wymagania

- Python 3.10 lub nowszy, ponieważ plik `app-4-instrukcje-warunkowe.py` korzysta z instrukcji `match`
- Brak zewnętrznych zależności, wykorzystano wyłącznie bibliotekę standardową

## Uruchomienie

```bash
git clone https://github.com/kmprograms/matura-kurs-python-4-instrukcje-warunkowe
cd matura-kurs-python-4-instrukcje-warunkowe
python app-4-instrukcje-warunkowe.py
```

Pozostałe pliki uruchamiasz w ten sam sposób, podając nazwę wybranego pliku. Żaden program nie wymaga wpisywania danych z klawiatury, bo fragment z `input` w pliku `app-3-pozyskiwanie-danych-systemy-liczbowe-float.py` jest zakomentowany.

## Struktura projektu

| Plik | Opis |
| --- | --- |
| `app-1-pierwszy-program-zmienne.py` | Pierwszy program, zmienne i ich typy, formatowanie w f-stringach, operatory arytmetyczne, zamiana wartości zmiennych, parametry `end` i `sep` w `print`, zamiana typów oraz operatory `+=`, `-=` i `*=` |
| `app-2-liczby-calkowite.py` | Operacje na liczbach całkowitych, parzystość i podzielność z użyciem `%`, operatory relacji, spójniki `and` i `or`, wyznaczanie cyfr liczby oraz zamiana sekund na godziny, minuty i sekundy |
| `app-3-pozyskiwanie-danych-systemy-liczbowe-float.py` | Pobieranie danych przez `input` (zakomentowane), losowanie z modułem `random`, systemy liczbowe, operacje bitowe oraz funkcje z modułu `math` |
| `app-4-instrukcje-warunkowe.py` | Kod omawiany w tym nagraniu: warunki logiczne, leniwe obliczanie, `if`, `if ... else`, `if ... elif ... else`, wyrażenie warunkowe, `match` oraz `min`, `max` i `abs` |

## Omówione zagadnienia i sposób działania kodu

### Warunki logiczne i operator `not`

Warunek logiczny to wyrażenie, którego wartością jest `True` albo `False`. Na początku pliku przypominam operatory relacji oraz spójniki `and` i `or`, a potem dodaję operator `not`, który neguje wartość logiczną.

```python
a = 11
b = 12

print(a > 10)  # True
print(a == 11)  # True
print(a != 12)  # True
print(a > 0 and a < 15)  # True
print(a < 0 or a > 10)  # True
print(not (a > 10))   # False
```

Operator `and` daje `True` tylko wtedy, gdy oba warunki składowe są prawdziwe. Operatorowi `or` wystarczy, że prawdziwy jest przynajmniej jeden z nich. Negowane wyrażenie warto umieścić w nawiasie. W tak prostym zapisie nie jest to konieczne, ale przy bardziej złożonym warunku z `and` i `or` nawias jasno pokazuje, że negacja dotyczy całości.

### Sprawdzanie, czy liczba należy do przedziału

Python pozwala zapisać przynależność do przedziału w jednym wyrażeniu, bez łączenia dwóch porównań spójnikiem `and`.

```python
c = 37
print(20 <= c <= 40)
print(not (20 <= c <= 40))
```

Pierwszy warunek sprawdza, czy `c` należy do przedziału obustronnie domkniętego od 20 do 40, i daje `True`. Drugi neguje całe wyrażenie, dlatego daje `False`. Rodzaj przedziału określają użyte operatory `<` i `<=`.

### Leniwe obliczanie (lazy evaluation)

```python
# Leniwe obliczanie
d = 5
print(d != 0 and 10 / d > 1)
```

Python sprawdza takie wyrażenie od lewej do prawej. Gdy `d` wynosi 0, pierwszy warunek daje `False`. Przy spójniku `and` cały warunek jest wtedy na pewno fałszywy, więc Python nie sprawdza już drugiej części. Dzięki temu nie dochodzi do dzielenia przez zero, które w Pythonie kończy się błędem. Gdy `d` wynosi 5, pierwszy warunek jest prawdziwy, więc Python musi sprawdzić również drugi. `10 / 5` to 2, a 2 jest większe od 1, dlatego wynik to `True`.

Takie działanie daje dwie korzyści. Wartość całego warunku jest ustalana szybciej, a obliczenia są bezpieczniejsze. Przy `and` warto umieszczać dalej na prawo te warunki, które zależą od wcześniejszych sprawdzeń albo wymagają więcej obliczeń. Jeżeli lżejszy warunek z lewej strony da `False`, cięższe operacje w ogóle się nie wykonają.

### Instrukcja `if`

Instrukcję zapisujesz jako `if`, potem warunek logiczny i dwukropek. Poniżej, po wcięciu na cztery spacje, umieszczasz instrukcje, które mają się wykonać. Może ich być dowolnie wiele. W Pythonie wcięcia są częścią składni.

```python
e, f = 3, 25

# Jeżeli zachodzi warunek logiczny, wykonaj instrukcje
# które zapiszesz poniżej "we wcięciu"
# Jeżeli warunek nie jest prawdziwy, wtedy pomijasz ten
# fragment kodu
if e >= f:
    g = e + f
    print(f"Wersja 1 - Dodawanie: {g = }")
```

Dla `e = 3` i `f = 25` warunek nie zachodzi, więc ten fragment jest pomijany i nic się nie wypisuje. W nagraniu sprawdzam też `e = 30`. Wtedy warunek zachodzi i pojawia się komunikat z sumą.

### Instrukcja `if ... else`

```python
# Jeżeli warunek zachodzi, wtedy wykonaj to, co pod if.
# Jeżeli warunek nie zachodzi, wtedy wykonaj to co pod else.
if e >= f:
    g = e + f
    print(f"Wersja 2 - Dodawanie: {g = }")
else:
    g = e * f
    print(f"Wersja 2 - Mnożenie: {g = }")
```

Sam `if` obsługuje tylko sytuację, w której warunek zachodzi. Konstrukcja z `else` obsługuje oba warianty. Dla wartości z pliku warunek nie zachodzi, więc wykonuje się sekcja `else` i program wypisuje iloczyn `g = 75`.

### Instrukcja `if ... elif ... else`

Ten wariant stosujesz, gdy sprawdzasz wiele warunków rozłącznych. Są to warunki, z których może zajść tylko jeden. Jeśli zachodzi jeden z nich, to pozostałe już nie zachodzą. Przykładem jest sprawdzanie, do którego z czterech przedziałów należy liczba:

- przedział 1 - `[1, 10]`, obustronnie domknięty
- przedział 2 - `(10, 25)`, obustronnie otwarty
- przedział 3 - `[25, 33)`, lewostronnie domknięty i prawostronnie otwarty
- przedział 4 - `[33, 48]`, obustronnie domknięty

Przedziały stykają się, ale nie mają części wspólnej. Liczba 10 należy tylko do przedziału 1, a liczba 33 tylko do przedziału 4.

Pierwsza wersja, zakomentowana w pliku, używa czterech osobnych instrukcji `if`:

```python
# 4 osobne if - każdy z nich jest sprawdzany osobno
# if 1 <= h <= 10:
#     print(f"Liczba {h} w przedziale 1")
# if 10 < h < 25:
#     print(f"Liczba {h} w przedziale 2")
# if 25 <= h < 33:
#     print(f"Liczba {h} w przedziale 3")
# if 33 <= h <= 48:
#     print(f"Liczba {h} w przedziale 4")
```

Ta wersja daje poprawne wyniki, ale nie jest optymalna. Każdy `if` jest sprawdzany niezależnie, więc dla `h = 10` Python po trafieniu w przedział 1 wykonuje jeszcze trzy niepotrzebne sprawdzenia.

Lepsza wersja używa konstrukcji `if ... elif ... else`:

```python
# Kiedy masz warunki rozłączne, wtedy lepiej sprawdzać je za pomocą if ... elif ... else
if 1 <= h <= 10:
    print(f"Liczba {h} w przedziale 1")
elif 10 < h < 25:
    print(f"Liczba {h} w przedziale 2")
elif 25 <= h < 33:
    print(f"Liczba {h} w przedziale 3")
elif 33 <= h <= 48:
    print(f"Liczba {h} w przedziale 4")
else:
    print("Liczba nie należy do żadnego z przedziałów")
```

Warunki są sprawdzane po kolei, aż któryś okaże się prawdziwy. Pozostałe są wtedy pomijane. Sekcja `else` wykonuje się, gdy nie zachodzi żaden warunek. Jest opcjonalna. Bez niej program nic by nie wypisał dla liczby spoza przedziałów.

Ta konstrukcja działa prawidłowo tylko dla warunków rozłącznych, bo służy do wybrania jednego z wielu wariantów. Kolejność warunków ma znaczenie. Warunki, które chcesz sprawdzić w pierwszej kolejności, umieszczasz wyżej.

### Wyrażenie warunkowe

Wyrażenie warunkowe (ternary operator) to krótszy zapis prostych konstrukcji `if ... else`, których wynikiem jest wartość.

```python
# Wyrażenie warunkowe
i, j = 12, 40
print(i * j if i < j else i + j)
k = i * j if i < j else i + j
print(k)
```

Warunek znajduje się między `if` a `else`. Gdy warunek zachodzi, całe wyrażenie przyjmuje wartość tego, co stoi na lewo od `if`, czyli `i * j`. Gdy nie zachodzi, przyjmuje wartość tego, co stoi na prawo od `else`, czyli `i + j`. Wynik możesz od razu wypisać albo przypisać do zmiennej i wykorzystać w dalszych obliczeniach. Dla `i = 12` i `j = 40` warunek zachodzi, więc w obu przypadkach wynik to 480.

### Instrukcja `match`

Instrukcja `match` wybiera jeden z wielu przypadków na podstawie wartości zmiennej. Przypadki opisujesz za pomocą `case`.

```python
# Instrukcja match

opcja = 31

match opcja:
    case 1:
        print("Opcja 1 - dodawanie")
    case 2 | 3:
        print("Opcja 2 - mnożenie lub dzielenie")
    case 6:
        print("Koniec")
    case _:
        print("Nie ma takiej opcji")
```

Zapis `case 2 | 3` obejmuje kilka wartości naraz. `case _` wykonuje się, gdy wartość nie pasuje do żadnego z wcześniejszych przypadków. Po dopasowaniu jednego przypadku pozostałe są pomijane. Typowe zastosowanie to proste menu w aplikacji.

Po `case` można zapisać znacznie więcej rodzajów wyrażeń. Szczegóły znajdziesz w dokumentacji Pythona. Na potrzeby matury z informatyki wystarczy to, co pokazuję w nagraniu.

### Funkcje `min`, `max` i `abs`

```python
m, n, o = 12, 34, 25

najmniejsza = min(m, n, o)
print(najmniejsza)

najwieksza = max(m, n, o)
print(najwieksza)

p = -13
print(abs(p))
```

`min` zwraca najmniejszą z podanych wartości, `max` największą, a `abs` wartość bezwzględną. Najmniejszą wartość można też wyznaczyć serią porównań. Takie podejście będziemy ćwiczyć przy implementacji algorytmów i zadań maturalnych.

## Wyniki

Uruchomienie pliku `app-4-instrukcje-warunkowe.py` z wartościami zapisanymi w kodzie wypisuje:

```
True
True
True
True
True
False
True
False
True
Wersja 2 - Mnożenie: g = 75
Liczba 15 w przedziale 2
480
480
Nie ma takiej opcji
12
34
13
```

W nagraniu sprawdzam też inne wartości zmiennych:

| Zmiana w kodzie | Wynik |
| --- | --- |
| `d = 0` | `False`, bez sprawdzania `10 / d > 1` |
| `e = 30` | `Wersja 1 - Dodawanie: g = 55` oraz `Wersja 2 - Dodawanie: g = 55` |
| `h = 10` | `Liczba 10 w przedziale 1` |
| `h = 33` | `Liczba 33 w przedziale 4` |
| `h = 111` | `Liczba nie należy do żadnego z przedziałów` |
| `opcja = 3` | `Opcja 2 - mnożenie lub dzielenie` |

## Uwagi implementacyjne

Wersja z czterema osobnymi instrukcjami `if` została w pliku jako komentarz, żeby można było porównać ją z konstrukcją `if ... elif ... else`.

W f-stringach użyto zapisu `{g = }`, który wypisuje nazwę zmiennej razem z jej wartością, na przykład `g = 75`.

Instrukcja `match` jest stosunkowo nowa w Pythonie. Pojawiła się w wersji 3.10, dlatego starsze interpretery nie uruchomią pliku `app-4-instrukcje-warunkowe.py`.

W nagraniu nazywam `print`, `min`, `max` i `abs` instrukcjami, bo pojęcie funkcji nie zostało jeszcze wprowadzone. W rzeczywistości są to funkcje wbudowane. Omówię je dokładniej w dalszej części kursu.