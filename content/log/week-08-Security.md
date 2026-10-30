---
title: "Uge 8 – Security"
date: 2026-10-09
weight: 8
draft: false
summary: "Implementering af registrering, login, JWT og brugerroller."
tags: ["Security", "JWT", "BCrypt", "Javalin"]
---

[⌂ Til forsiden](/Portfolio/)

## Hvad arbejdede jeg med?

I denne uge implementerede jeg security i API'et.

Projektet har tre brugerroller:

- `USER`
- `EMPLOYEE`
- `ADMIN`

Rollerne bestemmer, hvilke endpoints og pakker en bruger må tilgå.

## Authentication og authorization

Authentication betyder, at API'et kontrollerer, hvem brugeren er.

Authorization betyder, at API'et kontrollerer, hvad brugeren har tilladelse til.

Projektets regler er blandt andet:

- En almindelig bruger kan se sine egne pakker.
- En medarbejder kan registrere delivery events.
- En administrator kan udføre administrative handlinger.
- En bruger må ikke se en anden brugers pakke.

## Hvordan fungerer login?

Ved login udfører API'et disse trin:

1. Finder brugeren ud fra e-mail.
2. Sammenligner passwordet med den gemte BCrypt-hash.
3. Opretter et JWT-token.
4. Sender tokenet til klienten.

Tokenet sendes derefter med beskyttede requests:

```http
Authorization: Bearer <token>
```

## Hvad indeholder tokenet?

JWT-tokenet indeholder:

- Brugerens id
- Brugerens rolle
- Issuer
- Oprettelsestidspunkt
- Udløbstidspunkt

Tokenet indeholder ikke brugerens password eller password-hash.

`SecurityHandler` kontrollerer tokenet og sammenligner brugerens rolle med rollerne på den valgte route.

## Passwords

Passwords gemmes ikke som almindelig tekst.

`PasswordService` bruger BCrypt til at:

- Hashe passwords ved registrering
- Kontrollere passwords ved login

JWT-signaturen bruger en hemmelig nøgle fra miljøvariablen `JWT_SECRET`.

## Hvad var svært?

Det var svært at forstå forskellen mellem:

- Password-hashing
- Login
- JWT-oprettelse
- JWT-verifikation
- Kontrol af roller

Jeg gjorde derfor security-koden mere trinvis, så hver kontrol er tydelig og lettere at forklare.