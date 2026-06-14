---
trigger: always_on
---

# 🎨 Index: Cubículo Digital Design System

Este directorio contiene las reglas canónicas de UI/UX para Cubículo Digital.

## 📂 Estructura de Reglas
1. **[Colores y Tokens](./colors.md)**: Paleta de colores light y dark.
2. **[Tipografía y Espaciado](./specs.md)**: Font stacks, tamaños, border-radius.
3. **[Componentes UI](./ui-elements.md)**: Button, Input, badges, cards.

## 📏 Regla de Oro de Contraste
- **Light mode**: bg `#ffffff`, fg `#171717`.
- **Dark mode**: bg `#0a0a0a`/`#101622`, fg `#ededed`.
- **Bordes**: `#e5e7eb` (light), `#324467` (dark).
- **Muted text**: `#92a4c9`.

## 🎯 Semantic Colors
- **Primary**: `#1980e6` (azul principal)
- **Success**: `#22c55e` (verde completado)
- **Warning**: `#f59e0b` (naranja en progreso)
- **Error**: `#ef4444` (rojo error)

## 🛑 Prohibiciones Estrictas
1. **No usar colores sin contraste suficiente** en dark mode.
2. **No usar inline styles** — siempre Tailwind utility classes + cn().
3. **No modificar tokens globales** sin actualizar este archivo.
