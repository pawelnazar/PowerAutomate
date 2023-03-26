## Wnioski na bazie list sharepointowych z wykorzystaniem onedrive

Potrzebne licencje:
- onedrive
- outlook (wystarczy wersja przeglądarkowa)
- power automate free

##Lista kroków:
1. Utwórz nowy przeływ, który będzie uruchamiany podczas utworzenia nowego wpisu na liście sharepointowej.
2. Pobierz dane na temat użytkownika, który dodał wpis.
3. Pobierz dane na temat managera
4. Nie wymagany krok - pobierz dane na temat przełożonego przełożonego. 
5. Nie wymagany krok -  Sprawdź czy data rozpoczęcia nie jest później niż data zakończenia wniosku.
6. Uruchom i czekaj na zatwierdzenie  - zatwierdzenie do przełożonego.
7. Warunek - jeżeli tak idź dalej, jeżeli nie zmień status na brak akceptacji i anuluj przepływ.
8. Compose - szablon HTML wniosku
9. Utwórz wniosek w formacie html z szablonu compose z odpowiednimi danymi (onedrive connector).
10. Przekonwertuj html na pdf (onedrive connector).
11. Dodaj plik pdf na sharepoint.
12. Zaktualizuj status wpisu listy na zatwierdzony
13. Wyslij odpowiednie powiadomienia emailowe.

###FlowChart

```flow
st=>start: When an item is created (Sharepoint)
getuser=>operation: Get user profile (V2) (Office 365 Users)
getmanager=>operation: Get manager (V2) (Office 365 Users)
conditiondate=>condition: Data rozp < data zakon
updatelisterror=>operation: Update item (Sharepoint)
approval=>condition: Approve?
compose=>operation: Compose HTML (varibles)
createhtml=>operation: Create HTML file from Compose (onedrive)
converthtml=>operation: Convert HTML file to PDF (onedrive)
createpdf=>operation: Create file on Sharepoint  (Sharepoint)
e=>end: send emails to HR + employee (Outlook)

st->getuser->getmanager->conditiondate->approval->compose->createhtml->converthtml->createpdf->e

conditiondate(yes)->approval
conditiondate(no)->updatelisterror
approval(yes)->compose
approval(no)->updatelisterror
```
