---
title: "Uge 8 – Security"
date: 2026-10-09
weight: 8
draft: false
summary: "Arbejde med login, JWT og brugerroller."
tags: ["Security", "JWT", "Java"]
---

[⌂ Til forsiden](/Portfolio/)

## Hvad arbejdede jeg med?

I denne uge arbejdede jeg med security.

Projektet har tre brugerroller:

- `USER`
- `EMPLOYEE`
- `ADMIN`

Rollerne skal bestemme, hvad en bruger må gøre i API'et.

## Authentication og authorization

Authentication betyder, at API'et kontrollerer, hvem brugeren er.

Authorization betyder, at API'et kontrollerer, hvad brugeren har tilladelse til.

Reglerne skal være:

- En bruger må se sine egne pakker.
- En medarbejder må opdatere pakkestatus.
- En administrator må udføre administrative handlinger.

## Hvordan skal login fungere?

Ved login skal API'et:

1. Finde brugeren ud fra e-mail.
2. Kontrollere passwordet.
3. Oprette et JWT-token.
4. Sende tokenet til klienten.

Tokenet sendes derefter med requests:

```http
Authorization: Bearer <token>
```

## Passwords

Passwords må ikke gemmes som almindelig tekst.

De skal hashes, før de bliver gemt i databasen. Ved login sammenlignes passwordet med den gemte hash.

## Hvad var svært?

Det var svært at forstå forskellen mellem login, JWT-validering og kontrol af roller.

Jeg skulle også huske, at et JWT-token ikke må indeholde passwords eller andre hemmelige oplysninger.