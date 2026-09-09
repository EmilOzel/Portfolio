---
title: "Uge 3 – Opdatering af projekt efter møde"
date: 2026-09-04
weight: 1
draft: false
summary: ""
tags: ["Java", "Maven", "Jackson", "API", "Hibernate"]
---

[⌂ Til forsiden](/Portfolio/)

## Hvad tilføjede jeg i denne uge?

I denne uge begyndte jeg at implementere Package Delivery Tracker-applikationen ud fra planen fra uge 2.

Jeg konfigurerede projektet til Java 25 og oprettede en Maven-struktur med packages til:

- Controllers
- Services
- Entities
- DTO'er
- Enums
- Exceptions
- Konfiguration
- Utilities

Jeg begyndte også på projektets datamodel. De tre centrale entities bliver `User`, `Parcel` og `DeliveryEvent`.
Jeg bruger navnet `Parcel` i stedet for `Package`, fordi Java allerede indeholder typen `java.lang.Package`.

Jeg oprettede enums til brugerroller og pakkestatusser:

```java
public enum Role {
    USER,
    EMPLOYEE,
    ADMIN
}