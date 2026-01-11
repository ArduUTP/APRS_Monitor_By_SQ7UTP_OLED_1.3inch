# APRS Monitor (ESP8266 + OLED) 📡

![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)
![Platform: ESP8266](https://img.shields.io/badge/Platform-ESP8266-orange.svg)
![Status: Active](https://img.shields.io/badge/Status-Active-green.svg)

**APRS Monitor** to samodzielne urządzenie oparte na mikrokontrolerze ESP8266, które łączy się z serwerami APRS-IS przez WiFi, nasłuchuje ruchu w określonym promieniu od Twojej lokalizacji i wyświetla informacje o stacjach na ekranie OLED.

Projekt stworzony przez: **Marcin "Skrętka" (SQ7UTP)**.

## 🌟 Funkcjonalności

* **Monitorowanie na żywo:** Odbiór ramek APRS z serwerów Tier 2 (domyślnie `lodz.aprs2.net`).
* **Geolokalizacja:** Obliczanie odległości i azymutu (kierunku) do odbieranych stacji względem Twojej pozycji.
* **Tryb Smart Display:**
    * *Lista:* Przewijana lista ostatnich stacji.
    * *Szczegóły:* Gdy nadejdzie nowy pakiet, ekran automatycznie pokazuje duży znak, strzałkę kierunkową, prędkość, kurs i komentarz.
* **Konfiguracja przez WiFi:** Brak konieczności edycji kodu! Wszystkie ustawienia (Znak, Hasło, Koordynaty, Filtry) wprowadzasz przez przeglądarkę w telefonie/komputerze.
* **Web Panel:** Możliwość zmiany konfiguracji w trakcie pracy urządzenia bez konieczności resetowania do ustawień fabrycznych.
* **Beacon:** Urządzenie wysyła własną ramkę pozycyjną (SmartBeaconing - interwał czasowy).

## 🛠️ Wymagany Sprzęt

1.  **Mikrokontroler:** ESP8266 (np. NodeMCU v3, Wemos D1 Mini).
2.  **Wyświetlacz:** OLED 1.3" I2C na sterowniku **SH1106** (128x64).
    * *Uwaga: Standardowe ekrany 0.96" (SSD1306) wymagają zmiany jednej linii w kodzie.*
3.  **Zasilanie:** Kabel Micro-USB.

### Schemat połączeń (I2C)
| ESP8266 (NodeMCU) | OLED (SH1106) |
| :--- | :--- |
| 3.3V (lub 5V) | VCC |
| GND | GND |
| D1 (GPIO 5) | SCL |
| D2 (GPIO 4) | SDA |

## 📦 Instalacja

1.  Zainstaluj środowisko **Arduino IDE**.
2.  Dodaj obsługę płytek ESP8266 w Menedżerze Płytek.
3.  Zainstaluj wymagane biblioteki (Szkic -> Dołącz bibliotekę -> Zarządzaj bibliotekami):
    * `U8g2` (autor: oliver)
    * `WiFiManager` (autor: tzapu)
    * `ArduinoJson` (wersja 6.x)
4.  Wybierz w Arduino IDE odpowiednią płytkę (np. "NodeMCU 1.0").
5.  Przed wgraniem upewnij się, że masz zainstalowaną wtyczkę do przesyłania plików **ESP8266 LittleFS Data Upload** (opcjonalne, kod sam sformatuje pamięć przy pierwszym uruchomieniu, ale warto o tym pamiętać).
6.  Wgraj szkic (`APRS_Monitor.ino`) do urządzenia.

## 🚀 Pierwsze Uruchomienie i Konfiguracja

Urządzenie po pierwszym uruchomieniu (lub gdy nie znajdzie znanej sieci) wejdzie w tryb **Access Point**.

1.  Wyszukaj na telefonie/komputerze sieć WiFi o nazwie: `APRS-SETUP`.
2.  Połącz się z nią (hasło nie jest wymagane).
3.  Powinno automatycznie otworzyć się okno konfiguracji (Captive Portal). Jeśli nie, wejdź w przeglądarce na adres `192.168.4.1`.
4.  Wybierz swoją domową sieć WiFi i wpisz do niej hasło.
5.  Uzupełnij parametry APRS:
    * **Znak:** Twój znak krótkofalarski (np. SQ7UTP-10).
    * **APRS Pass:** Kod wygenerowany dla Twojego znaku (poszukaj "APRS Passcode Generator" w Google).
    * **Lat/Lon:** Twoje współrzędne geograficzne (np. 51.75 / 19.45).
    * **Filtr:** Promień nasłuchu w kilometrach (np. 50).
6.  Zapisz. Urządzenie zrestartuje się i połączy z siecią.

## 📖 Instrukcja Obsługi

### Ekran Główny (Lista)
Po uruchomieniu zobaczysz listę ostatnio odebranych stacji.
* Format: `ZNAK | DYSTANS | AZYMUT`
* Na dole paska: Zegar (pobierany z NTP) oraz Twój adres IP.

### Ekran Nowej Stacji
Gdy urządzenie odbierze nowy pakiet, przełączy się na 12 sekund w tryb szczegółowy:
* Wyświetla duży Znak i strzałkę kierunkową (N/S/W/E).
* Cyklicznie zmienia informacje na dole:
    1.  Dystans i Kierunek (deg).
    2.  Prędkość (km/h) i Kurs (Heading).
    3.  Komentarz (Beacon text).

### Zmiana Ustawień (Web Panel)
Gdy urządzenie jest połączone z Twoją siecią, wpisz jego adres IP (widoczny na dole ekranu OLED) w przeglądarce. Otrzymasz dostęp do panelu, gdzie możesz zmienić promień filtra, ikonę lub komentarz bez resetowania urządzenia.

## 📜 Licencja
Projekt udostępniony na licencji **GNU GPL v3**.
Masz prawo do kopiowania, modyfikowania i rozpowszechniania kodu, pod warunkiem zachowania informacji o autorze i udostępniania zmian na tej samej licencji.

**Autor:** Marcin "Skrętka" (SQ7UTP)
**Podziękowania:** Jacek (SP7EZD)

---
*73 i udanych nasłuchów!*
