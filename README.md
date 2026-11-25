# encryption-keys-test

Klucze publiczne **Receiverów** [OpenCardAPI](https://opencardapi.org) do szyfrowania danych karty (JWE, pole `payment_means`).

> **Środowisko: test.** Klucze produkcyjne są w repozytorium [encryption-keys](https://github.com/OpenCardApi/encryption-keys). Oba repozytoria mają ten sam układ.

Specyfikacja: [opencardapi.org – 9. Klucze](https://opencardapi.org/#dok-klucze) oraz [11. Szyfrowanie danych karty (JWE)](https://opencardapi.org/#dok-payment-means).

## Układ repozytorium

```
encryption-keys-test/
└── <domena linku KSeF>/     # np. example.com dla linku https://example.com/ksef
    └── <kid>.json           # klucz publiczny w formacie JWK (RFC 7517)
```

Przykład:

```
encryption-keys-test/
└── example.com/
    └── example-key.json     # kid: "example-key"
```

```json
{
  "kty": "RSA",
  "use": "enc",
  "e": "AQAB",
  "alg": "RSA-OAEP-256",
  "n": "sUIAv8kBzFaUmviQobwWLcbu-JlWE2RbzgDHFve1WPUYPCefmIxSaCyRlQYvzJXw…",
  "kid": "example-key"
}
```

## Zasady

- Każdy Receiver ma katalog nazwany domeną swojego testowego linku KSeF.
- Każdy klucz to osobny plik `<kid>.json`. Nazwa pliku bez rozszerzenia jest równa polu `kid` w JWK.
- Wymagane pola JWK: `kty: "RSA"`, `use: "enc"`, `alg: "RSA-OAEP-256"`, `n`, `e`, `kid`.
- Repozytorium zawiera **wyłącznie klucze publiczne**. Klucz prywatny nigdy nie opuszcza Receivera.
- Używaj w testach innej pary kluczy niż na produkcji.
- Przy wymianie klucza Receiver publikuje nowy plik pod nowym `kid`, a stary usuwa, gdy przestanie być używany.

## Powiązane repozytoria

| Klucze | Produkcja | Test |
|---|---|---|
| Podpis Senderów (PEM) | [signing-keys](https://github.com/OpenCardApi/signing-keys) | [signing-keys-test](https://github.com/OpenCardApi/signing-keys-test) |
| Szyfrowanie Receiverów (JWK) | [encryption-keys](https://github.com/OpenCardApi/encryption-keys) | **encryption-keys-test** |

## Kontakt

Publikacja lub wymiana klucza, pytania do specyfikacji: [support@espago.com](mailto:support@espago.com).
