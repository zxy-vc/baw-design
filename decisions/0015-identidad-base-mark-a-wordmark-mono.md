# ADR 0015 — Identidad base: Mark A + wordmark mono para BaW OS

**Estado:** aceptado  
**Fecha:** 2026-05-02  
**Decisor:** [[USER|Fran Durán]]  
**Repo:** `baw-design`

---

## Contexto

En la revisión visual inicial del sistema de diseño BaW, existían dos direcciones principales para el mark:

- **Mark A — desfase pronunciado:** tres capas isométricas con offset visible. Comunica capas operativas, floors de software y jerarquía.
- **Mark B — alineado a cubo:** lectura más literal de edificio/volumen. Más conservador e inmobiliario.

La exploración previa sugería Mark B si BaW se quería percibir como bienes raíces con software, y Mark A si BaW se quería percibir como software para bienes raíces.

Fran confirmó que, al verlo implementado, prefiere sustituir Mark B por **Mark A** como dirección base.

---

## Decisión

BaW OS adopta como dirección base:

1. **Mark:** Mark A — capas/isométrico con desfase pronunciado.
2. **Wordmark:** `BaW OS` en estilo mono/técnico se mantiene.
3. **Dirección de marca:** mezcla ordenada así:
   1. Sistema operativo técnico
   2. Real estate premium
   3. Hospitality discreto

---

## Consecuencias

- Los assets aprobados iniciales viven en `assets/logos/`:
  - `baw-mark-a.svg`
  - `baw-os-lockup.svg`
- Las referencias históricas en `references/claude-design-v1/` permanecen como exploración, no como fuente viva.
- Figma puede seguir usándose para revisar y comentar, pero el source of truth técnico queda en este repo.
- Las futuras pantallas de `baw-os` deben usar la dirección visual “OS técnico primero”, evitando que la marca se vuelva demasiado inmobiliaria o hospitality.

---

## Notas de implementación

Mark A no debe “corregirse” para alinearlo como cubo perfecto. El desfase es parte de la voz visual: operación por capas, sistema vivo, infraestructura detrás del edificio.

#baw #design-system #adr
