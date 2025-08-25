# Kalkulator PRO INSTAL - OZE

Profesjonalny kalkulator instalacji OZE (Odnawialnych Źródeł Energii) z panelem administracyjnym i synchronizacją danych w czasie rzeczywistym.

## Funkcjonalności

### 🧮 Kalkulator Instalacji
- **Rozbudowa PV** - panele fotowoltaiczne
- **Magazyn energii** - sam magazyn energii
- **Komplet** - panele + magazyn energii
- **Falowniki** - wybór odpowiedniego falownika
- **Opcje montażu** - dach skośny, płaski, grunt

### 💰 Obliczenia Finansowe
- Ceny netto/brutto z VAT 8%
- Dotacje "Mój Prąd" (do 16 000 zł dla magazynów, 23 000 zł dla kompletów)
- Ulga termomodernizacyjna (12%, 32%, 19%, 8.5%)
- Symulacja kredytów z różnymi bankami
- Kalkulacja rat miesięcznych

### 🔧 Panel Administracyjny
- Zarządzanie produktami (panele, magazyny, falowniki, komplety)
- Zarządzanie bankami i oprocentowaniem
- Ustawienia narzutów i kosztów montażu
- Synchronizacja w czasie rzeczywistym

## Konfiguracja Firebase (Synchronizacja danych)

Aby włączyć synchronizację danych między urządzeniami:

### 1. Utwórz projekt Firebase
1. Przejdź do [Firebase Console](https://console.firebase.google.com/)
2. Kliknij "Dodaj projekt"
3. Nazwij projekt (np. "oze-kalk")
4. Wyłącz Google Analytics (opcjonalnie)
5. Kliknij "Utwórz projekt"

### 2. Włącz Firestore Database
1. W menu po lewej kliknij "Firestore Database"
2. Kliknij "Utwórz bazę danych"
3. Wybierz "Rozpocznij w trybie testowym"
4. Wybierz lokalizację (np. europe-west3)

### 3. Skonfiguruj reguły bezpieczeństwa
W Firestore Database → Reguły, zastąp reguły na:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

### 4. Pobierz konfigurację
1. W ustawieniach projektu kliknij ikonę koła zębatego
2. Wybierz "Ustawienia projektu"
3. Przewiń do sekcji "Twoje aplikacje"
4. Kliknij ikonę web (</>)
5. Nazwij aplikację (np. "oze-kalk-web")
6. Skopiuj konfigurację

### 5. Klucze Firebase są już skonfigurowane! 🔐

**✅ Twoje klucze Firebase są już zakodowane w kodzie aplikacji.**

Klucze są chronione prostym szyfrowaniem XOR i są bezpieczne w publicznym repozytorium. Aplikacja automatycznie dekoduje je podczas uruchamiania.

**🔒 Bezpieczeństwo:** 
- Klucze są zakodowane, nie widać ich bezpośrednio w kodzie
- Każdy może zobaczyć kod, ale nie może łatwo odczytać kluczy
- Aplikacja działa natychmiast po wdrożeniu na GitHub Pages

### 🎉 Gotowe!
Twoja aplikacja jest teraz w pełni skonfigurowana z:
- ✅ Firebase Firestore (synchronizacja danych)
- ✅ Google Analytics (śledzenie użytkowników)
- ✅ Synchronizacja w czasie rzeczywistym
- ✅ Fallback do localStorage (jeśli Firebase nie działa)

**Wszystkie zmiany w panelu administracyjnym będą automatycznie widoczne dla wszystkich użytkowników!**

## Użycie

### Panel Administracyjny
- **Hasło**: `instal2025`
- **Dostęp**: Kliknij "Panel Admin" w prawym górnym rogu

### Dodawanie produktów
1. Zaloguj się do panelu admin
2. Wybierz sekcję "Produkty"
3. Kliknij "Dodaj [typ produktu]"
4. Wprowadź nazwę, cenę i narzut
5. Produkt automatycznie pojawi się u wszystkich użytkowników

## Technologie

- **Frontend**: HTML5, CSS3 (Tailwind CSS), JavaScript
- **Baza danych**: Firebase Firestore
- **Analityka**: Google Analytics (Firebase)
- **Hosting**: GitHub Pages
- **Ikony**: Font Awesome

## Struktura danych

### Produkty
```javascript
{
    panels: [
        {id: 1, name: "5kW Canadian Solar", price: 9000, markup: 1500, power: 5}
    ],
    batteries: [
        {id: 1, name: "5.12kWh Lithtech", price: 11000, markup: 5000}
    ],
    inverters: [
        {id: 1, name: "5kW Falownik Deye", price: 2500, markup: 500}
    ],
    completes: [
        {id: 1, name: "5kW + 5.12kWh Komplet", price: 32000, markup: 3000, power: 5}
    ]
}
```

### Banki
```javascript
[
    {name: "Santander", rate: 6.0},
    {name: "PKO BP", rate: 7.5}
]
```

### Ustawienia
```javascript
{
    installationCosts: {flat: 200, ground: 600},
    batteryMarkups: {"10": 2000, "15": 4500}
}
```

## Wdrażanie

### GitHub Pages
1. Przejdź do ustawień repozytorium
2. Przewiń do sekcji "Pages"
3. W "Source" wybierz "Deploy from a branch"
4. Wybierz branch "main" i folder "/ (root)"
5. Kliknij "Save"

Twoja aplikacja będzie dostępna pod adresem: `https://twoja-nazwa-uzytkownika.github.io/oze-kalk`

## Licencja

Projekt jest dostępny na licencji MIT.

## 🔒 Bezpieczeństwo

### Ochrona kluczy Firebase
- **Klucze API są zakodowane** w kodzie za pomocą szyfrowania XOR
- **Publiczne repo jest bezpieczne** - klucze nie są widoczne bezpośrednio
- **Aplikacja działa natychmiast** po wdrożeniu na GitHub Pages

### Reguły bezpieczeństwa Firebase
W Firebase Console → Firestore Database → Reguły, ustaw:
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true; // Tylko dla testów!
    }
  }
}
```

**⚠️ Uwaga:** Reguły `allow read, write: if true` pozwalają każdemu na dostęp do bazy. W produkcji należy dodać autoryzację.

## Wsparcie

W przypadku problemów z konfiguracją Firebase lub synchronizacją danych, sprawdź:
1. Czy reguły Firestore pozwalają na odczyt/zapis
2. Czy konfiguracja Firebase jest poprawna
3. Czy konsola przeglądarki nie pokazuje błędów
4. Czy GitHub Pages jest włączone w ustawieniach repozytorium
