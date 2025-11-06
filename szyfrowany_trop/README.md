# Szyfrowany Trop - SecureSystems

## Opis Zadania

Poziom: **Średni-Trudny**

Kategoria: **Kryptografia/Free**

### Historia
Zespół bezpieczeństwa SecureSystems odkrył podejrzany plik na komputerze jednego z pracowników. Plik jest zaszyfrowany i może zawierać poufne informacje firmowe. Zadaniem jest odszyfrowanie pliku i znalezienie tajnych danych.

### Wskazówki
1. Poszukaj plików na stronie download
2. Plik jest zaszyfrowany za pomocą prostego kodowania
3. Po odszyfrowaniu znajdziesz dane logowania do systemu
4. Użyj znalezionych danych na stronie logowania
5. Sprawdź czy istnieje ukryty plik z flagą

### Pliki do pobrania
- `download_page.html` - Strona z linkiem do pobrania zaszyfrowanego pliku
- `encrypted_file.bin` - Zaszyfrowany plik z danymi pracownika

---

## KOMPLETNE ROZWIĄZANIE

### Krok 1: Analiza strony pobierania
Otwórz `download_page.html` w przeglądarce i pobierz `encrypted_file.bin`

### Krok 2: Odszyfrowanie pliku
Zaszyfrowany plik używa kodowania Base64. Do odszyfrowania:

**Linux/Mac:**
```bash
base64 -d encrypted_file.bin > decrypted_file.txt
```

**Windows (PowerShell):**
```powershell
[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String((Get-Content -Raw encrypted_file.bin))) | Out-File decrypted_file.txt
```

**Python:**
```python
import base64

with open('encrypted_file.bin', 'rb') as f:
    encrypted_data = f.read()
    
decrypted_data = base64.b64decode(encrypted_data).decode('utf-8')

with open('decrypted_file.txt', 'w') as f:
    f.write(decrypted_data)
```

### Krok 3: Analiza odszyfrowanych danych
W pliku `decrypted_file.txt` znajdziesz:
- Login: `secure_user`
- Hasło: `secure_pass123`
- ID pracownika: `SEC-2024-AX7492`
- **FLAGA:** `CTF{krypto_secure_2024}`

### Krok 4: Dostęp do strony logowania
Otwórz `login_page.html` i zaloguj się używając:
- Login: `secure_user`
- Hasło: `secure_pass123`

### Krok 5: Weryfikacja danych
System zweryfikuje dane z bazy `credentials.json`. Poprawne dane pozwolą na dostęp do systemu i potwierdzenie flagi.

---

## SZCZEGÓŁY TECHNICZNE

### Metoda szyfrowania
- **Base64 Encoding** - powszechne kodowanie binarne
- Klucz: brak (proste kodowanie)
- Bezpieczeństwo: niskie (łatwe do odszyfrowania)

### Struktura danych
```json
{
  "users": [
    {"username": "secure_user", "password": "secure_pass123", "valid": true},
    {"username": "admin", "password": "admin123", "valid": false},
    {"username": "user1", "password": "password1", "valid": false},
    ...
  ]
}
```

### Pliki zadania
- `README.md` - Główny opis (ten plik)
- `README_tutorial.md` - Dodatkowe wskazówki
- `flag.txt` - Plik z flagą CTF
- `download_page.html` - Strona pobierania
- `encrypted_file.bin` - Zaszyfrowany plik (Base64)
- `decrypted_file.txt` - Odszyfrowane dane (odpowiedź)
- `login_page.html` - Strona logowania SecureSystems
- `credentials.json` - Baza danych użytkowników

---

## PODSUMOWANIE ROZWIĄZANIA

1. **Pobierz plik** z download_page.html
2. **Odszyfruj** encrypted_file.bin używając Base64
3. **Znajdź dane logowania** w odszyfrowanym pliku
4. **Zaloguj się** na login_page.html
5. **Potwierdź flagę** CTF{krypto_secure_2024}

**FLAGA:** `CTF{krypto_secure_2024}`

---

*Zadanie stworzone dla celów edukacyjnych CTF*
*SecureSystems Security Team 2024*