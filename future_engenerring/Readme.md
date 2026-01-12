# 🛠️ Feature Engineering & Data Preprocessing Pipeline

## 1. Cel Modułu

Ten etap projektu koncentruje się na czyszczeniu, transformacji i przygotowaniu surowych danych o nieruchomościach do modelowania. Głównym wyzwaniem jest obsługa brakujących danych (Missing Values) oraz wysoką skośność danych, przy jednoczesnym zachowaniu spójności między zbiorem treningowym a testowym.

## 2. Kluczowe Technologie

* **Pandas & NumPy:** Manipulacja danymi i operacje wektorowe.
* **Dython:** Analiza korelacji zmiennych kategorycznych (Nominal Association).
* **SciPy & Statsmodels:** Analiza statystyczna rozkładów cech.
* **Seaborn/Matplotlib:** Wizualizacja danych (EDA).

## 3. Strategia Imputacji Danych (Missing Values Imputation)

Zastosowano **imputację opartą na grupie wartości** zamiast prostego uzupełniania średnią globalną lub kosztownych metod iteracyjnych.

### Decyzja Projektowa: Grupowanie po sąsiedztwie (`Neighborhood`)

Zamiast używać zaawansowanych modeli (np. IterativeImputer czy imputacji opartej na drzewach decyzyjnych), zdecydowano się na imputację statystykami (średnia/mediana) **agregowanymi w grupach sąsiedztwa**.

* **Uzasadnienie:** Ceny i cechy domów są silnie skorelowane z lokalizacją. Dom w bogatej dzielnicy z brakującą informacją o powierzchni prawdopodobnie ma metraż zbliżony do sąsiadów, a nie do średniej całego miasta.
* **Uzasadnienie:** Imputacja oparta na modelach ML wewnątrz pętli walidacyjnej (Optuna) drastycznie wydłużyłaby czas treningu. Metoda grupowania jest kompromisem zapewniającym wysoką jakość danych przy niskim koszcie obliczeniowym .

## 4. Obsługa Zmiennych Kategorycznych

### Problem: Rzadkie Etykiety (Rare Labels)

Zidentyfikowano problem "rzadkich kategorii" w zbiorach walidacyjnych, które nie występowały w treningu (lub odwrotnie). Standardowe kodowanie (np. Target Encoding) mogłoby prowadzić do przeuczenia (overfitting) lub błędów wykonania.

### Rozwiązanie: Obsługa `NA` (Not Available)

Wiele kolumn (np. `PoolQC`, `GarageType`) zawiera wartości `NA`, które w tym zbiorze danych nie oznaczają "braku informacji", lecz **fizyczny brak udogodnienia** (np. brak garażu).

* **Działanie:** Wartości te zostały jawnie przekształcone na nową kategorię ('None').

## 5. Analiza Statystyczna

Wykorzystano bibliotekę **Dython** oraz **korelację Spearmana/Pearsona** do identyfikacji zmiennych silnie skorelowanych z ceną (`SalePrice`), co pozwoliło na wstępną selekcję cech przed modelowaniem.