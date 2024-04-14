---
title: "Bulova algebra"
date: "2023-10-07T19:48:14Z"
categories: ["references"]
tags: ["math", "sr"]
draft: false
---

## Definicija

Na skupu `B = {a, b, c, ...}` su definisane operacije:

- Operacija komplementiranja `~` : `(∀a ∈ B) ~a = b, b ∈ B`
  - Komplementiranje je zatvorenu na skupu `B`.
- Operacija sabiranja `+` : `(∀a, b ∈ B) a + b = c, c ∈ B`
  - Sabiranje je zatvorenu na skupu `B`.
- Operacija množenja `⋅` : `(∀a, b ∈ B) a ⋅ b = c, c ∈ B`
  - Množenje je zatvorenu na skupu `B`.

Skup `B` i ove tri operacije čine Bulovu algebru ako su zadovoljene sledeće aksiome.

## Aksiome

- Zakon asocijativnosti:
  - `(a + b) + c = a + (b + c)` i `(a ⋅ b) ⋅ c = a ⋅ (b ⋅ c)`
- Zakon komutativnosti:
  - `a + b = b + a` i `a ⋅ b = b ⋅ a`
- Zakon o neutralnom elementu:
  - `a + 0 = a` i `a ⋅ 1 = a`
- Zakon komplementarnosti:
  - `a + ~a = 1` i `a ⋅ ~a = 0`
- Zakon distributivnosti množenja prema sabiranju:
  - `a ⋅ (b + c) = a ⋅ b + a ⋅ c`
- Zakon distributivnosti sabiranja prema množenju:
  - `a + b ⋅ c = (a + b) ⋅ (a + c)`

## Konstante

- Konstanta `0` (false).
- Konstanta `1` (true).

## Prioriteti operacija i Bulovi izrazi

- Za operacije sabiranja i množenja važi simetričnost aksioma (sve što važi za `+` važi i za `⋅`).
- Prioritet operacija, od najvišeg prioriteta ka najnižem: komplementiranje, množenje, sabiranje.
- Bulov izraz: kombinacija simbola i operacija Bulove algebre.
- Iz simetričnosti aksioma potiče _princip dualnosti_.
- Izraz `Q^d` je dualan izrazu `Q`, i obrnuto, ako je `Q^d` dobijeno od `Q` na sledeći način:
  - Operacija sabiranja se zameni operacijom množenja i obrnuto.
  - Konstanta `1` se zameni konstantom `0` i obrnuto.
- Ako su `Q` i `R` dualni izrazi tada važi `Q(a, b, c, ...) = R(a, b, c, ...) ≡ Q^d(a, b, c, ...) = R^d(a, b, c, ...)`.

## Teoreme

_Dokazi teorema su izostavljeni iz digitalizovane verzije beležaka._

- `~0 = 1`
- `~1 = 0`
- `~~a = a`
- `a + 1 = 1`
- `a ⋅ 0 = 0`
- `~(a + b) = ~a ⋅ ~b`
- `~(a ⋅ b) = ~a + ~b`
- `a + ~a ⋅ b = a + b`
- `a ⋅ (~a + b) = a ⋅ b`
- `a + a = a`
- `a ⋅ a = a`

## Bulova algebra na skupu od dva elementa (prekidačka algebra)

- Skup elemenata prekidačke algebre _mora_ biti `{0, 1}` jer su to neutralni elementi za operacije sabiranja i množenja.
- U prekidačkoj algebri, operacije nose nazive:
  - `~` : negacija.
  - `+` : disjunkcija.
  - `⋅` : konjukcija.
- Sve aksiome i teoreme Bulove algebre važe i u prekidačkoj algebri.
