# Analiza rynku Airbnb w Waszyngtonie 🇺🇸 (Python)

Eksploracyjna i statystyczna analiza ofert **Airbnb w Waszyngtonie (Washington, D.C.)** w Pythonie. Pełny przepływ: od pobrania surowych danych, przez czyszczenie i diagnostykę rozkładów, po badanie korelacji i siły związków między zmiennymi — ze szczególnym naciskiem na **czynniki kształtujące cenę** noclegu.

## Dane

- **Źródło:** [Inside Airbnb](http://insideairbnb.com/) — `listings.csv.gz` dla Washington, D.C., zrzut z **17 września 2024**, wczytywany bezpośrednio z adresu URL (nie trzeba pobierać plików ręcznie).
- **Zmienne kluczowe (`important_vars`):** `price`, `accommodates`, `beds`, `bathrooms`, `bedrooms`, `room_type`.

## Zakres analizy

- **Eksploracja (EDA)** — informacje o zbiorze, podgląd wierszy, statystyki opisowe, unikalne wartości zmiennych kategorycznych.
- **Braki danych** — analiza braków (liczby i procenty) oraz **imputacja medianą** (m.in. grupowo per `room_type` przez `groupby().transform()`, `bedrooms` → 0, grupowanie `9+`).
- **Czyszczenie i typowanie** — konwersja `price` z formatu `"$1,234"` na `float` (regex), zamiana kolumn walutowych/procentowych na liczby, mapowanie flag `t`/`f` → wartości logiczne, korekta typów.
- **Diagnostyka rozkładów** — skośność i kurtoza (`scipy.stats`), normalizacja z-score.
- **Analiza ceny** — statystyki ceny po oczyszczeniu, podział na przedziały cenowe, **boxploty ceny względem typu pokoju**, mediana ceny per `room_type`.
- **Korelacje** — macierz korelacji zmiennych numerycznych oraz `pairplot` dla zmiennych kluczowych (cena vs liczba gości/łóżek/łazienek/sypialni).
- **Siła związków zmiennych** — test **chi-kwadrat** (`chi2_contingency`) i miara **φ²** dla zmiennych kategorycznych oraz **współczynnik korelacji (R²/η²)** liczony regresją OLS `zm_numeryczna ~ C(zm_kategoryczna)` (`statsmodels`).
- **Analiza typów pokoi** — liczność i udział procentowy ofert wg `room_type` (przed i po czyszczeniu).

Wizualizacje powstały w `matplotlib`/`seaborn` oraz interaktywnie w `plotly.express`; notebook zawiera komplet wyrenderowanych wyników.

## Pliki

| Plik | Opis |
|------|------|
| `Airbnb_washington.ipynb` | Kompletny notebook (Python): EDA → czyszczenie → diagnostyka → korelacje i testy związków. |

## Uruchomienie

```bash
pip install pandas numpy matplotlib seaborn plotly scipy statsmodels tabulate
```

Otwórz `Airbnb_washington.ipynb` w Jupyterze lub Google Colab i uruchom komórki po kolei. Dane wczytują się automatycznie z adresu Inside Airbnb.

## Tech stack

`Python` · `pandas` · `numpy` · `scipy` · `statsmodels` · `matplotlib` · `seaborn` · `plotly`

---

> Siostrzany projekt do [analizy rynku Airbnb w Winnipeg](https://github.com/karolpolikarp/Winnipeg) wykonanej w języku **R** — ta sama domena, inny warsztat (Python vs R).
