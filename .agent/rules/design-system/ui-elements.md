---
trigger: always_on
---

# 🧩 Elementos de UI

## 1. Button
| Variant | Light | Dark |
|---------|-------|------|
| primary | `bg-blue-600 hover:bg-blue-700 shadow-lg` | igual |
| secondary | `bg-gray-200` | `dark:bg-gray-700` |
| outline | `border + transparent bg` | `dark:border-[#232f48] dark:text-white` |
| ghost | `transparent hover:bg-gray-100` | `dark:hover:bg-gray-800` |

## 2. Input
| Estado | Light | Dark |
|--------|-------|------|
| default | `border-gray-300` | `dark:border-[#324467] dark:bg-[#0b101a]` |
| focus | `border-indigo-500 ring` | igual |
| error | `border-red-500` | igual |
| disabled | `opacity-50` | igual |

## 3. StatCard (Dashboard)
- **Título**: `text-sm text-muted` (light: `#637588`, dark: `#92a4c9`)
- **Valor**: `text-3xl font-bold`
- **Barra de progreso**: `h-2 rounded-full` con `bg-blue-500`

## 4. DeptCard
- **Gradiente**: light gray-50, dark `dark:bg-[#111722]`
- **Borde**: `dark:border-[#232f48]`
- **Badge estado**: `rounded-full` con colores semánticos
