# Marsun — prototyp landing page lead magnetu

Jednostronicowy interfejs promujący materiał edukacyjny o konfiguracji falowników hybrydowych Deye. Projekt prezentuje ścieżkę od opisu materiału i korzyści do formularza kontaktowego oraz komunikatu potwierdzenia.

Formularz jest demonstracyjny: pokazuje zmianę stanu interfejsu, ale nie wysyła danych ani PDF.

## Zaimplementowane elementy

- Responsywny układ z formularzem imienia, adresu e-mail, opcjonalnego NIP i wymaganej zgody.
- Natywna walidacja HTML oraz formatowanie NIP podczas wpisywania.
- Symulacja wysyłki: wyłączenie przycisku, komunikat oczekiwania i pokazanie potwierdzenia po 1,2 s.
- Popup przy próbie opuszczenia strony oraz po 45 s; `sessionStorage` ogranicza jego ponowne wyświetlenie w danej sesji.
- Przeniesienie e-maila z popupu do głównego formularza i przewinięcie do niego.
- Mobilny pasek CTA, którego widoczność zależy od położenia formularza, oraz animacje sekcji przez `IntersectionObserver`.

## Uruchomienie

Wymagania: współczesna przeglądarka i Python 3 do lokalnego serwera plików.

```bash
git clone https://github.com/dzwoniar/marsun.pl-lead.git
cd marsun.pl-lead
python -m http.server 8000 --bind 127.0.0.1
```

Otwórz [http://localhost:8000](http://localhost:8000). Na Windows można zastąpić `python` poleceniem `py`. Zatrzymaj serwer przez `Ctrl+C`. Instalacja zależności i budowanie nie są wymagane.

## Organizacja kodu

```text
.
├── index.html   # HTML, osadzony CSS i obsługa interakcji
└── README.md
```

Całość znajduje się w [index.html](index.html). Projekt korzysta z HTML5, CSS, JavaScript i API przeglądarki, bez frameworka. Google Fonts ładuje DM Sans i Playfair Display jako zewnętrzne zasoby wizualne.

Przepływ formularza: walidacja przeglądarki → `handleSubmit()` z `preventDefault()` → `setTimeout()` → przełączenie widoków `form-content` i `form-success`. Nie ma żądania HTTP z danymi kontaktowymi. W `sessionStorage` zapisywana jest flaga `marsun_popup_shown`, bez pól formularza.

Skrypt zawiera warunkowe wywołania `gtag` i `fbq` po symulowanym zgłoszeniu. Sam plik nie ładuje bibliotek Google Analytics ani Meta Pixel i nie definiuje ich konfiguracji.

## Granice demonstracji

- Komunikat „sprawdź skrzynkę” nie oznacza wysłania wiadomości. Brakuje backendu, integracji mailingowej i samego pliku PDF.
- Walidacja NIP sprawdza format i ogranicza liczbę cyfr; nie weryfikuje sumy kontrolnej ani danych firmy w rejestrze.
- Polityka prywatności jest odnośnikiem `#`. Realna obsługa kontaktów wymaga własnego endpointu i docelowych dokumentów.
- Liczby, opinie i deklaracje handlowe na stronie stanowią treść prototypu, a nie potwierdzone wyniki projektu.
- Repozytorium nie ma skonfigurowanego zestawu testów ani procesu wdrożenia.

## Powiązane warianty

[Wariant v2 lead magnetu](https://github.com/dzwoniar/marsun.pl-demo-lead-v2) rozwija treść strony i ekran potwierdzenia. [Główny prototyp B2B](https://github.com/dzwoniar/marsun.pl-demo) prezentuje szerszą ofertę.
