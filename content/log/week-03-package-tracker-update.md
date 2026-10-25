---
title: "Uge 3 – Data integration"
date: 2026-09-04
weight: 3
draft: false
summary: "Opsætning af projektet og integration med OpenRouteService."
tags: ["Java", "Maven", "Jackson", "API", "Hibernate"]
---

[⌂ Til forsiden](/Portfolio/)

## Hvad arbejdede jeg med?

I denne uge begyndte jeg at implementere Package Delivery Tracker.

Jeg oprettede packages til:

- Controllers
- Services
- DAOs
- Entities
- DTO'er
- Enums
- Exceptions
- Konfiguration

De tre centrale entities er:

- `User`
- `Parcel`
- `DeliveryEvent`

Jeg bruger navnet `Parcel`, fordi Java allerede har typen `java.lang.Package`.

## OpenRouteService

Jeg begyndte også på integrationen med OpenRouteService.

Når en pakke oprettes, sender API'et leveringsadressen til OpenRouteService. Tjenesten returnerer en formateret adresse samt latitude og longitude.

Java bruger `HttpClient` til requesten og Jackson til at oversætte JSON-svaret til et `OpenRouteDTO`.

## Hvorfor bruger jeg DTO'er?

DTO'er bruges til at modtage og sende data.

OpenRouteServices JSON-svar indeholder mange oplysninger. Projektet bruger kun:

- Den formaterede adresse
- Latitude
- Longitude

Derfor behøver DTO'en kun at indeholde de relevante felter.

## Hvad var svært?

Det var svært at forstå strukturen i JSON-svaret fra OpenRouteService.

Jeg skulle også være opmærksom på, at koordinaterne kommer i denne rækkefølge:

```text
longitude, latitude
```

## Hvad vil jeg arbejde videre med?

Jeg vil færdiggøre databaseoperationerne og relationerne mellem projektets entities.