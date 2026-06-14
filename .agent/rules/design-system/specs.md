---
trigger: always_on
---

# ⚙️ Especificaciones Técnicas y Lógica

## 1. Tipografía y Radios
- **Font**: System font stack (`Arial, Helvetica, sans-serif`).
- **H1**: `text-4xl lg:text-6xl font-extrabold`.
- **H2**: `text-3xl font-bold`.
- **Body**: `text-lg`.
- **Small**: `text-sm`.
- **Páginas/Cards**: `rounded-2xl` (16px).
- **Inputs/Botones**: `rounded-xl` (12px).

## 2. Lógica de Desarrollo
- **Dark mode**: Únicamente via Tailwind `dark:` prefix.
- **Theme toggle**: useTheme hook + localStorage persistence.
- **Contraste**: Borde siempre más oscuro que el fondo.
- **cn()**: Usar `cn()` de `lib/utils.ts` para conditional classes (clsx + tailwind-merge).
