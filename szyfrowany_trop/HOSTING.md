# Instrukcje Hostingu - Szyfrowany Trop

## Opcje Uruchomienia Zadania

### 1. Serwer Lokalny (Python)

#### Python 3 (zalecane)
```bash
# Przejdź do katalogu zadania
cd ctf_zadania/szyfrowany_trop/

# Uruchom prosty serwer HTTP
python3 -m http.server 8000

# Lub dla Python 2 (legacy)
python -m SimpleHTTPServer 8000
```

#### Python z konkretnym portem
```bash
python3 -m http.server 8080
```

**Dostęp:** http://localhost:8000

---

### 2. Node.js (http-server)

#### Instalacja
```bash
# Globalna instalacja http-server
npm install -g http-server

# Lub użyj npx (bez instalacji)
npx http-server -p 8000
```

#### Uruchomienie
```bash
# Przejdź do katalogu
cd ctf_zadania/szyfrowany_trop/

# Uruchom serwer
http-server -p 8000 -c-1

# Z opcjami
http-server -p 8000 -c-1 --cors
```

**Dostęp:** http://localhost:8000

---

### 3. PHP Built-in Server

```bash
# Upewnij się że masz zainstalowany PHP
php --version

# Przejdź do katalogu
cd ctf_zadania/szyfrowany_trop/

# Uruchom serwer
php -S localhost:8000
```

**Dostęp:** http://localhost:8000

---

### 4. Live Server (VS Code)

#### Instalacja rozszerzenia
1. Otwórz VS Code
2. Przejdź do Extensions (Ctrl+Shift+X)
3. Wyszukaj "Live Server"
4. Zainstaluj rozszerzenie "Live Server" od Ritwick Dey

#### Uruchomienie
1. Otwórz folder `ctf_zadania/szyfrowany_trop/` w VS Code
2. Kliknij prawym przyciskiem na `download_page.html`
3. Wybierz "Open with Live Server"
4. Lub kliknij "Go Live" w dolnym pasku statusu

**Dostęp:** http://127.0.0.1:5500 (lub inny port)

---

### 5. GitHub Pages (Online)

#### Przygotowanie repozytorium
```bash
# Inicjalizuj repozytorium git
git init

# Dodaj pliki
git add .
git commit -m "Initial commit - Szyfrowany Trop CTF"

# Utwórz repozytorium na GitHub i dodaj remote
git remote add origin https://github.com/TWOJ_USERNAME/ctf-szyfrowany-trop.git

# Wypchnij zmiany
git push -u origin main
```

#### Aktywacja GitHub Pages
1. Idź do repozytorium na GitHub
2. Settings → Pages
3. Source: Deploy from a branch
4. Branch: main / root
5. Kliknij Save

**Dostęp:** https://TWOJ_USERNAME.github.io/ctf-szyfrowany-trop/

---

### 6. Netlify (Darmowy hosting)

#### Drag & Drop
1. Idź na https://www.netlify.com
2. Drag & drop katalog `szyfrowany_trop/` na stronę
3. Otrzymasz link typu `https://random-name-123.netlify.app`

#### Git Integration
1. Połącz repozytorium GitHub z Netlify
2. Ustaw build command: `echo "No build needed"`
3. Publish directory: `/` (root)
4. Deploy automatyczny przy każdym push

---

### 7. Vercel (Darmowy hosting)

#### Instalacja CLI
```bash
npm install -g vercel
```

#### Deploy
```bash
# Przejdź do katalogu
cd ctf_zadania/szyfrowany_trop/

# Zaloguj się do Vercel
vercel login

# Deploy
vercel --prod

# Lub bez interakcji
vercel --prod --yes
```

---

## Testowanie Zadania

### Sprawdzenie plików
```bash
# Sprawdź czy wszystkie pliki są dostępne
ls -la szyfrowany_trop/

# Sprawdź zawartość zaszyfrowanego pliku
file szyfrowany_trop/encrypted_file.bin
head -5 szyfrowany_trop/encrypted_file.bin

# Sprawdź JSON
python3 -m json.tool szyfrowany_trop/credentials.json
```

### Test strony
1. Otwórz w przeglądarce: `http://localhost:8000/download_page.html`
2. Pobierz plik `encrypted_file.bin`
3. Odszyfruj: `base64 -d encrypted_file.bin`
4. Sprawdź zawartość odszyfrowanego pliku
5. Przejdź do: `http://localhost:8000/login_page.html`
6. Zaloguj się z danymi z odszyfrowanego pliku

---

## Rozwiązywanie Problemów

### CORS Errors (Cross-Origin)
**Problem:** `Access to fetch at 'credentials.json' from origin has been blocked by CORS policy`

**Rozwiązanie:**
1. Użyj serwera HTTP zamiast otwierania pliku bezpośrednio
2. Lub dodaj flagę `--cors` do http-server
3. Lub w Chrome uruchom z flagą: `--disable-web-security --user-data-dir=/tmp/chrome_dev`

### File Not Found
**Problem:** Pliki nie są znalezione

**Sprawdzenia:**
1. Czy wszystkie pliki są w tym samym katalogu?
2. Czy ścieżka do pliku jest poprawna?
3. Czy serwer działa na odpowiednim porcie?

### Permission Denied
**Problem:** Brak uprawnień do odczytu

**Rozwiązanie:**
```bash
# Dodaj uprawnienia do odczytu
chmod +r szyfrowany_trop/encrypted_file.bin
chmod +r szyfrowany_trop/credentials.json

# Lub dla całego katalogu
chmod -R +r szyfrowany_trop/
```

---

## Struktura URL

### Przy uruchomieniu na localhost:8000

#### Strony HTML
- http://localhost:8000/download_page.html
- http://localhost:8000/login_page.html

#### Pliki do pobrania
- http://localhost:8000/encrypted_file.bin
- http://localhost:8000/credentials.json
- http://localhost:8000/flag.txt

#### Dokumentacja
- http://localhost:8000/README.md
- http://localhost:8000/README_tutorial.md

---

## Konfiguracja dla Hostingu Publicznego

### GitHub Pages
Upewnij się że struktura jest poprawna:
```
szyfrowany_trop/
├── download_page.html
├── login_page.html
├── encrypted_file.bin
├── credentials.json
├── flag.txt
├── README.md
└── README_tutorial.md
```

### Zmiana ścieżek w HTML (jeśli potrzebne)
Jeśli strony są w podfolderze, zaktualizuj ścieżki:

**W download_page.html:**
```html
<a href="./encrypted_file.bin" download="encrypted_file.bin">
```

**W login_page.html:**
```javascript
fetch('./credentials.json')
```

---

## Bezpieczeństwo Uruchomienia

### ⚠️ Uwagi
1. **Nie uruchamiaj** zadania na serwerze produkcyjnym
2. **Używaj** tylko do celów edukacyjnych CTF
3. **Nie udostępniaj** rozwiązań publicznie
4. **Monitoruj** dostęp do serwera

### 🔒 Zabezpieczenia
- Wszystkie serwery mają ograniczoną funkcjonalność
- Brak dostępu do systemu plików
- Tylko HTTP (bez HTTPS)
- Logowanie wszystkich operacji w konsoli

---

## Podsumowanie

**Najłatwiejsze opcje uruchomienia:**

1. **Python HTTP Server** - najszybsze, bez instalacji
2. **Live Server (VS Code)** - dla użytkowników VS Code
3. **GitHub Pages** - dla publicznego udostępnienia

**Dla początkujących:** Użyj Python HTTP Server
**Dla zaawansowanych:** GitHub Pages + automatyczny deploy

---

*Dokumentacja hostingu - SecureSystems CTF 2024*