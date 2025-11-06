# Szyfrowany Trop - Tutorial & Wskazówki

## Dodatkowe Wskazówki dla Początkujących

### 1. Analiza struktury plików
Jeśli nie wiesz od czego zacząć:
- Sprawdź wszystkie pliki w katalogu
- Przeczytaj nazwy plików - mogą wskazywać na typ zawartości
- Pliki `.bin` często zawierają dane binarne lub zaszyfrowane

### 2. Rozpoznawanie kodowania Base64
**Charakterystyczne cechy Base64:**
- Zawiera znaki: A-Z, a-z, 0-9, +, /
- Długość stringa jest wielokrotnością 4
- Często kończy się znakiem `=`
- Przykład: `SGVsbG8gV29ybGQ=`

**Jak rozpoznać Base64 w hexdump:**
```bash
hexdump -C encrypted_file.bin | head -10
```

### 3. Narzędzia do odszyfrowywania Base64

**Online decoders:**
- https://www.base64decode.org/
- https://base64.guru/converter/decode

**Linux commands:**
```bash
# Metoda 1 - base64
base64 -d encrypted_file.bin > output.txt

# Metoda 2 - xxd + base64
xxd -r -p encrypted_file.bin | base64 -d

# Metoda 3 - sprawdzenie typu pliku
file encrypted_file.bin
```

**Python one-liner:**
```python
import base64; print(base64.b64decode(open('encrypted_file.bin','rb').read()).decode())
```

**Windows PowerShell:**
```powershell
[System.Convert]::FromBase64String((Get-Content -Raw -Path .\encrypted_file.bin -Encoding UTF8)) | ForEach-Object { [System.Text.Encoding]::UTF8.GetString($_) }
```

### 4. Analiza strony logowania
**Co sprawdzić:**
- Źródło strony (View Source)
- Zawartość pliku `credentials.json`
- JavaScript na stronie (Console/Developer Tools)
- Czy istnieją ukryte elementy

**Sprawdzanie konsoli przeglądarki:**
1. F12 → Console
2. Sprawdź czy są błędy JavaScript
3. Zobacz czy są jakieś komunikaty debug

### 5. Przydatne komendy Linux

```bash
# Sprawdzenie typu pliku
file nazwa_pliku

# Hex dump (pierwsze 100 bajtów)
xxd -l 100 nazwa_pliku

# Przeszukiwanie tekstu
grep -r "CTF" .

# Lista wszystkich plików
ls -la

# Szukanie plików z określonym rozszerzeniem
find . -name "*.txt"
find . -name "*.json"
```

### 6. Analiza JSON
**Sprawdzanie poprawności JSON:**
```bash
python -m json.tool credentials.json
```

**Wyczytanie danych Python:**
```python
import json

with open('credentials.json', 'r') as f:
    data = json.load(f)

# Wyświetl wszystkich użytkowników
for user in data['users']:
    print(f"Username: {user['username']}, Valid: {user.get('valid', False)}")
```

### 7. Debugging krok po kroku

**Krok 1:** Sprawdź strukturę
```bash
ls -la
```

**Krok 2:** Sprawdź typ pliku
```bash
file encrypted_file.bin
```

**Krok 3:** Sprawdź początek pliku
```bash
head -5 encrypted_file.bin
```

**Krok 4:** Odszyfruj
```bash
base64 -d encrypted_file.bin
```

**Krok 5:** Znajdź flagę
```bash
grep -i "ctf" decrypted_file.txt
```

### 8. Częste błędy

❌ **Błędy początkujących:**
- Próba otwarcia pliku .bin w edytorze tekstu
- Nie rozpoznanie Base64
- Zapomnienie o `-d` w base64
- Błędne kodowanie znaków

✅ **Dobre praktyki:**
- Używaj `file` do sprawdzenia typu pliku
- Sprawdzaj początek pliku przed odszyfrowywaniem
- Testuj różne metody dekodowania
- Sprawdzaj czy dane wyglądają sensownie

### 9. Wskazówki bonusowe

**Sprawdź czy plik zawiera więcej warstw:**
```bash
# Sprawdź hex dump
xxd encrypted_file.bin | head -20

# Sprawdź czy nie ma innego kodowania
file encrypted_file.bin
strings encrypted_file.bin
```

**Sprawdź zawartość strony:**
```bash
# Pobierz źródło HTML
curl -s download_page.html | grep -i "download\|file\|bin"

# Sprawdź czy są linki
grep -o 'href="[^"]*"' download_page.html
```

### 10. Rozwiązywanie problemów

**Problem:** "Invalid base64"
- Sprawdź czy plik nie ma znaku nowej linii na końcu
- Usuń ewentualne białe znaki: `tr -d '\n' < encrypted_file.bin | base64 -d`

**Problem:** "Permission denied"
- Sprawdź uprawnienia: `ls -l encrypted_file.bin`
- Dodaj uprawnienia: `chmod +r encrypted_file.bin`

**Problem:** "No such file"
- Sprawdź ścieżkę: `pwd && ls -la`
- Upewnij się że jesteś w właściwym katalogu

---

## Status Zadania

**Poziom:** Średni-Trudny  
**Czas rozwiązywania:** 30-60 minut  
**Umiejętności:** Kryptografia, Analiza plików, Web Security  

**Gotowy do rozpoczęcia? Powodzenia! 🚀**