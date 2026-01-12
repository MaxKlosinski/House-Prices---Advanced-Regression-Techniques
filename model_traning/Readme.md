# 🏠 House Prices Prediction - Model Training Pipeline

## 1. Przegląd Projektu

Ten moduł odpowiada za trenowanie modelu regresji (XGBoost) w celu przewidywania cen nieruchomości. Proces opiera się na danych wcześniej przetworzonych w module *Feature Engineering*. Głównym celem jest minimalizacja błędu RMSE (Root Mean Squared Error) na wartościach które zostały znormalizowane za pomocą metodą logarytmiczną przy użyciu optymalizacji hiperparametrów.

## 2. Wykorzystane Technologie

**Silnik modelu:** XGBoost (Extreme Gradient Boosting)

  – Wybrany ze względu na wysoką wydajność na danych.
  – Jest to popularna biblioteka, co umożliwiło my szybsze znalezienie potrzebnych mi treści do nauki 
 
**Optymalizacja:** Optuna – framework do automatycznego dostrajania hiperparametrów.

**Walidacja:** Scikit-learn (KFold, train_test_split, metrics).

**Analiza:** Pandas, NumPy, Seaborn.

## 3. Strategia Walidacji i Trenowania

Aby zapewnić rzetelną ocenę modelu i uniknąć przeuczenia (overfittingu) na małym zbiorze danych, zastosowałem następujące techniki:

### A. Przetwarzanie Typów Danych

Przed trenowaniem następuje ostateczna konwersja typów danych:

* Zmienne kategoryczne są rzutowane na typ `category`, aby wykorzystać natywną obsługę kodowania danych przez XGBoost (`enable_categorical=True`).

    * Dzięki automatycznemu kodowaniu w XGboost nie byłem zmuszony na wykonywanie prostych kodowań które zabierały by mi czas a nie uczyły mnie czegokolwiek innego.

* Specyficzne kolumny numeryczne, takie jak `MSSubClass`, są traktowane jako kategoryczne, ponieważ ich wartości liczbowe reprezentują kody klas, a nie wartości ciągłe. Tak została objąsniona ta kolumna w dokumencie opisującym dane w tabeli.


### B. Walidacja Krzyżowa (Cross-Validation)

Zastosowano metodę **K-Fold Cross-Validation** z podziałem na 5 części ().

* **Cel:** Każda próbka danych jest używana zarówno do trenowania, jak i walidacji.

**Zastosowanie:** Wewnątrz funkcji celu (objective function) Optuny, błąd RMSE jest uśredniany z 5 foldów, co daje bardziej stabilną metrykę niż pojedynczy podział train/test.

## 4. Optymalizacja Hiperparametrów (Optuna)

Model jest dostrajany przy użyciu biblioteki Optuna z bazą danych SQLite do przechowywania historii prób. Optymalizowana funkcja celu minimalizuje średni błąd RMSE.

**Kluczowe parametry podlegające optymalizacji:**

**Struktura drzewa:** `max_depth`, `max_leaves`, `min_child_weight` – kontrola złożoności modelu.

**Uczenie:** `learning_rate`, `n_estimators` – szybkość uczenia i liczba drzew.

**Regularyzacja:** `reg_alpha` (L1), `reg_lambda` (L2), `gamma` – zapobieganie przeuczeniu.

**Metoda boostingu:** Testowanie wariantów `gbtree` oraz `dart`.

## 5. Wyniki i Interpretacja Modelu

Po zakończeniu optymalizacji trenowany jest ostateczny model na pełnym zbiorze danych przy użyciu najlepszych znalezionych parametrów.

### Najważniejsze cechy (Feature Importance)

Analiza ważności cech wskazuje, że kluczowymi czynnikami wpływającymi na cenę są :

