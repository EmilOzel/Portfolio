---
title: "Uge 1 – Opsætning af portfolio"
date: 2026-08-19
weight: 1
draft: false
summary: "Opsætning af en Hugo-baseret udviklingslog i projektets repository."
tags: ["Hugo", "Dokumentation"]
---

[⌂ Til forsiden](/Portfolio/)

## Hvad tilføjede jeg i denne uge?

Jeg tilføjede et Hugo-portfolio til repositoryet og oprettede strukturen til ugentlige indlæg i udviklingsloggen.

## Hvilke nye teknologier brugte jeg?

Jeg brugte Hugo, Hugo Modules, Congo-temaet, GitHub Actions og GitHub Pages.

## Hvorfor strukturerede jeg det sådan?

Portfolioet ligger i samme repository som applikationen, så kode og ugentlige refleksioner udvikler sig sammen. Hver uge har sin egen Markdown-fil, hvilket gør loggen enkel at vedligeholde. Et GitHub Actions-workflow bygger og deployer siden, når ændringer pushes til `main`-branchen.

## Hvad fungerede godt?

Hugo gør det hurtigt at oprette og organisere indhold som Markdown-filer. Når loggen ligger i repositoryet, er det også let at se projektets historik ved siden af implementeringen. GitHub Pages gør det enkelt at udgive loggen uden separat hosting.

## Hvad var svært eller forvirrende?

Den første opsætning krævede, at både Hugo og Go var tilgængelige i terminalen. Det var også vigtigt at køre Hugo-kommandoer fra repositoryets rodmappe og ikke fra hjemmemappen. Deployment kræver desuden, at GitHub Pages bruger GitHub Actions som udgivelseskilde.

## Hvad vil jeg forbedre næste gang?

Jeg vil kontrollere de nødvendige værktøjer og terminalstier, før jeg begynder opsætningen. Derefter vil jeg tilføje ugentlige indlæg, efterhånden som applikationen udvikles.
