# House Prices: Advanced Regression Techniques
## Wykorzystałem zbiór danych ze strony kaggle z konkurencji: House Prices - Advanced Regression Techniques
## Przegląd Projektu
Celem tego projektu jest stworzenie modelu uczenia maszynowego przewidującego ceny nieruchomości na podstawie zestawu różnorodnych cech. Projekt stanowi praktyczne zastosowanie technik regresji oraz inżynierii cech (Feature Engineering) w języku Python.

Głównym wyzwaniem było obsłużenie dużej liczby różnorodnych zmiennych (zarówno numerycznych, jak i kategorycznych) oraz zidentyfikowanie kluczowych czynników wpływających na wycenę rynkową domu.

# Technologie i Narzędzia
W projekcie wykorzystano następujące biblioteki Data Science:
* Pandas / NumPy: Manipulacja danymi, czyszczenie i operacje na ramkach danych.
* Scikit-learn: Budowa modeli regresyjnych, preprocessing danych oraz walidacja.
* Matplotlib / Seaborn: Wizualizacja danych w celu zrozumienia korelacji.
* Jupyter Notebook: Środowisko pracy, podzielone na moduły dla zachowania czytelności kodu.

# Architektura i Proces Przetwarzania
Struktura projektu została podzielona na logiczne etapy, co ułatwia zarządzanie kodem:
1. Analiza Danych: Analiza rozkładu zmiennej celowej (SalePrice) i sprawdzenie skośności danych. Identyfikacja i wizualizacja korelacji między cechami a ceną. Wykrywanie i usuwanie wartości odstających (outliers), które mogłyby negatywnie wpłynąć na model.
2. Transformacja zmiennych: Logarytmowanie zmiennych skośnych w celu zbliżenia ich rozkładu do normalnego.
3. Kodowanie zmiennych kategorycznych: Zastosowanie technik takich jak One-Hot Encoding lub Label Encoding dla danych tekstowych.
4. Tworzenie nowych cech: Agregacja istniejących danych.
5. Modelowanie i ewaluacja i testowanie różnych algorytmów regresji. Zastosowanie walidacji krzyżowej (Cross-Validation) w celu uniknięcia przeuczenia (overfittingu). Strojenie hiperparametrów modeli w celu optymalizacji błędu (minimalizacja RMSE - Root Mean Squared Error).
