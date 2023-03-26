## Różne zmienne i funkcje w Power Automate



1. Approval:
	```json
		"body": {
			"responses": [
				{
					"responder": {
						"id": "024b855d-afa2-426c-adea-85bb95d2ce13",
						"displayName": "Przełożona Adele Vance",
						"email": "AdeleV@onmicrosoft.com",
						"tenantId": "000000-f4d0-4ba3-a314-7e9e366657b8",
						"userPrincipalName": "AdeleV@onmicrosoft.com"
					},
					"requestDate": "2023-03-15T13:04:31Z",
					"responseDate": "2023-03-15T13:05:06Z",
					"approverResponse": "Approve"
				}
			],
	```

	Imię i nazwisko zatwierdzającego:
	`body('Uruchom_i_czekaj_na_zatwierdzenie')['responses'][0]?['responder']?['displayName']`

	Data zatwierdzenia:
	`body('Uruchom_i_czekaj_na_zatwierdzenie')['responses'][0]?['responseDate']`

2. Warunki:
	zatwierdzony approval
	
	![image](/images/conditionApproval.png)

	Warunek sprawdzający kolumne(true/false), jeżeli wartość jest true dodaje tekst, jezeli false to nic nie dodaje (przydatne np do wniosków i innych plików typu PDF)
	`if(equals(triggerOutputs()?['body/NazwaKolumnyZSharepoint'],true),'tekst ktory ma sie wyswietlic','')`

3. Formatowie dat:
	`formatDateTime(triggerOutputs()?['body/Datarozpoczecia'], 'dd-MM-yyyy')`

