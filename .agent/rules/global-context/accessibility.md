---
trigger: always_on
---

# ♿ Accesibilidad (WCAG) & Contraste

## Regla de Oro
**Borde siempre más oscuro/perceptible que el fondo.**

## Valores de Contraste
- **Light mode**: bg `#ffffff`, fg `#171717`, primary `#1980e6`.
- **Dark mode**: bg `#0a0a0a`, fg `#ededed`, muted `#92a4c9`, border `#324467`.

## Modo Oscuro - Valores Mínimos
- **Fondo mínimo**: `#101622` (body), `#111722` (cards).
- **Borde mínimo**: `#232f48` (separadores).
- **Hover**: `rgba(255,255,255,0.05)`.

## Prohibiciones
- ❌ **PROHIBIDO** usar colores sin contraste suficiente en modo oscuro.
- ✅ Usar siempre tokens semánticos definidos en el design system.
