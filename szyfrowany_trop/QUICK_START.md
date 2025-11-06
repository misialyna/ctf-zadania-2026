# Szybki Start - Szyfrowany Trop

## ⚡ Szybkie Uruchomienie (1 minuta)

### Opcja 1: Python HTTP Server (Zalecane)
```bash
cd ctf_zadania/szyfrowany_trop/
python3 -m http.server 8000
```

Otwórz w przeglądarce: http://localhost:8000/download_page.html

---

### Opcja 2: Live Server (VS Code)
1. Otwórz folder w VS Code
2. Prawym przyciskiem na `download_page.html`
3. "Open with Live Server"

---

## 🎯 Rozwiązanie (5 minut)

### Krok 1: Pobierz plik
- Idź na download_page.html
- Kliknij "Pobierz Plik" - pobierzesz `encrypted_file.bin`

### Krok 2: Odszyfruj
```bash
base64 -d encrypted_file.bin > decrypted_file.txt
```

### Krok 3: Znajdź dane
W pliku `decrypted_file.txt` znajdziesz:
- Login: `secure_user`
- Hasło: `secure_pass123`
- **FLAGA:** `CTF{krypto_secure_2024}`

### Krok 4: Zaloguj się
- Idź na login_page.html
- Wprowadź dane logowania
- Potwierdź flagę!

---

## 📚 Więcej informacji
- **README.md** - Pełne rozwiązanie
- **README_tutorial.md** - Szczegółowe wskazówki
- **HOSTING.md** - Instrukcje hostingu

---

## 🔗 Linki po uruchomieniu serwera
- http://localhost:8000/download_page.html - Strona pobierania
- http://localhost:8000/login_page.html - Strona logowania
- http://localhost:8000/encrypted_file.bin - Zaszyfrowany plik
- http://localhost:8000/credentials.json - Baza danych użytkowników
- http://localhost:8000/flag.txt - Flaga CTF

---

**Powodzenia w rozwiązywaniu! 🚀**

*Zadanie CTF - SecureSystems 2024*