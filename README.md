<h1 align="center">glance-pokemon</h1>

<p align="center">
  <strong>A Glance widget that surfaces a random Pokémon with type-aware styling, stats, and species badges.</strong>
</p>

<p align="center">
  <a href="https://github.com/glanceapp/glance"><img src="https://img.shields.io/badge/Glance-custom--api-111827?style=flat-square" alt="Glance custom-api"></a>
  <a href="https://pokeapi.co"><img src="https://img.shields.io/badge/Source-Pok%C3%A9API-ef4444?style=flat-square" alt="Data source PokéAPI"></a>
  <a href="https://randomnumberapi.com"><img src="https://img.shields.io/badge/Source-RandomNumberAPI-2563eb?style=flat-square" alt="Random number source"></a>
  <img src="https://img.shields.io/badge/Format-YAML-ef4444?style=flat-square&logo=yaml&logoColor=white" alt="YAML">
  <img src="https://img.shields.io/badge/License-MIT-22c55e?style=flat-square" alt="MIT License">
</p>

<p align="center">
  <a href="#overview">Overview</a> •
  <a href="#quick-start">Quick Start</a> •
  <a href="#widget-details">Widget Details</a> •
  <a href="#references">References</a>
</p>

<p align="center">
  <img src="docs/pokemon-widget.png" alt="Random Pokemon widget preview" width="420">
</p>

---

## Overview

| Widget | Purpose | Best Fit | File |
|---|---|---|---|
| Random Pokemon | Show a random Pokemon with official artwork, type chips, base stats, height, weight, and optional legendary or mythical badges | `small` | `widgets/random-pokemon.yml` |

The widget is designed for a compact sidebar-style Glance placement and renders directly from public APIs without any additional backend or local service:

- random Pokemon selection through `randomnumberapi.com`
- Pokemon data and artwork from [PokeAPI](https://pokeapi.co)
- type-aware gradient accents around the artwork
- built-in fallbacks for random ID errors, Pokemon lookup errors, and missing artwork

### Data Flow

1. Glance requests a random Pokemon ID from `randomnumberapi.com`.
2. The widget loads the Pokemon record from `https://pokeapi.co/api/v2/pokemon/<id>`.
3. It loads the species record from `https://pokeapi.co/api/v2/pokemon-species/<id>`.
4. The template renders artwork, type colors, stats, physical attributes, and optional `Legendary` or `Mythical` badges.

---

## Quick Start

1. Copy `widgets/random-pokemon.yml` into your Glance `widgets/` folder.
2. Include the widget in `glance.yml`.
3. Reload Glance.

No environment variables are required.

```yaml
pages:
  - name: Fun
    columns:
      - size: small
        widgets:
          - $include: widgets/random-pokemon.yml
```

Reference config: `examples/glance.yml`

---

## Widget Details

### Random Pokemon (`widgets/random-pokemon.yml`)

<p align="center">
  <img src="docs/pokemon-widget.png" alt="Random Pokemon widget preview" width="420">
</p>

```yaml
- type: custom-api
  title: Random Pokemon
  cache: 5m
  url: https://www.randomnumberapi.com/api/v1.0/random?min=1&max=1025&count=1
  template: |
    # Random ID lookup, Pokemon data requests, species lookup, and rendering
    # are handled inside the template
    ...
```

### Behavior Notes

- the widget is tuned for a `small` Glance column
- each refresh selects a new random Pokemon and caches the result for `5m`
- the artwork circle, divider accents, and artwork shadow adapt to the Pokemon type palette
- dual-type Pokemon blend primary and secondary type colors in the accent treatment
- species data adds `Legendary` and `Mythical` badges when available
- official artwork falls back to the default sprite if the high-resolution image is missing
- if one of the public APIs is unavailable, the widget renders a clear error state instead of a broken card

---

## References

- **Dashboard platform:** [`glanceapp/glance`](https://github.com/glanceapp/glance)  
  Widget implementation targets Glance `custom-api` behavior and config style.

- **Pokemon data:** [`PokeAPI`](https://pokeapi.co)  
  Pokemon details, artwork references, species metadata, and type information.

- **Random ID source:** [`Random Number API`](https://randomnumberapi.com)  
  Used to select the random Pokedex number for each refresh.

- **Original widget inspiration:** `KintsugiUwU` on Discord (`kintsugiuwu`)  
  Credit for the original random Pokemon widget concept this version was built from.

---

## Disclaimer

This widget was developed with support from [OpenAI Codex](https://openai.com/codex) and a custom [glance-skill](https://github.com/nichtlegacy/glance-skill).

---

<p align="center">
  <strong><a href="LICENCE">MIT License</a></strong> © 2026
</p>
