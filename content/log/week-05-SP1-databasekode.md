---
title: "Uge 5 – SP1 og databasekode"
date: 2026-09-18
weight: 5
draft: false
summary: "Arbejde med DAO-klasser, transaktioner og forretningsregler."
tags: ["Java", "JPA", "DAO", "PostgreSQL"]
---

[⌂ Til forsiden](/Portfolio/)

## Hvad arbejdede jeg med?

I denne uge samlede jeg flere af semesterets emner i Package Delivery Tracker.

Jeg arbejdede med:

- JPA og Hibernate
- DAO-klasser
- PostgreSQL
- Relationer mellem entities
- Transaktioner
- Forretningsregler

Jeg oprettede `UserDAO` og `ParcelDAO`.

## Hvad gør DAO-klasserne?

DAO-klasserne håndterer kommunikationen med databasen.

`UserDAO` kan:

- Oprette en bruger
- Finde en bruger efter id
- Finde en bruger efter e-mail

`ParcelDAO` kan:

- Oprette en pakke
- Hente pakker
- Hente pakker efter ejer
- Oprette delivery events
- Opdatere pakkestatus
- Slette en pakke

## Hvordan bruges transaktioner?

Når en pakke oprettes, bliver både pakken og dens første event gemt i samme transaktion:

```text
Opret pakke
→ Opret CREATED-event
→ Gem begge ændringer
```

Hvis noget fejler, bliver transaktionen rullet tilbage. Det forhindrer, at databasen gemmer en pakke uden dens første event.

## Hvilke regler tilføjede jeg?

Jeg tilføjede regler for gyldige statusændringer.

Eksempler:

```text
CREATED → PICKED_UP
PICKED_UP → IN_TRANSIT
IN_TRANSIT → AT_SORTING_CENTER
AT_SORTING_CENTER → OUT_FOR_DELIVERY
OUT_FOR_DELIVERY → DELIVERED
```

En leveret eller annulleret pakke kan ikke ændres til en ny status.

En pakke kan kun slettes, mens dens status er `CREATED`.

## Hvad var svært?

Det var svært at afgøre, hvad der skulle ligge i DAO'en, og hvad der skulle ligge i servicen.

Jeg valgte, at DAO'en håndterer databaseoperationerne, mens servicen håndterer validering, adgangskontrol og forretningsregler.