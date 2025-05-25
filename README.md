# 📘 Documento Técnico - App de Gestor de Hábitos (MVP)

## 🔖 Propósito

Desarrollar una app web simple para gestionar hábitos diarios. La app debe ser funcional sin conexión, persiste los datos localmente, y tiene una experiencia centrada en el uso diario personal. Se enfoca en funcionalidades esenciales.

## 🧰 Stack Tecnológico

- **Frontend**: Astro
- **Componentes interactivos**: React (o Preact)
- **Estilos**: TailwindCSS
- **Persistencia**: `localStorage`
- **Sin backend**

---

## 📊 MVP - Funcionalidades Incluidas

### Hábitos

- Crear hábitos con:
  - Nombre (obligatorio, máx. 30 caracteres, único visualmente)
  - Color (con valor por defecto)
- Editar hábito (nombre, color)
- Eliminar hábito (borra también registros)

### Registro diario

- Ver lista de hábitos activos del día
- Marcar/desmarcar hábitos como completados (toggle)
- Estado se guarda por fecha en `localStorage`

### Visualización de progreso

- Vista de hábitos completados hoy
- Vista semanal de progreso (7 días)
- Indicador de racha (días consecutivos completando todos los hábitos)

### UX/UI

- Mobile-first, interfaz limpia
- Indicaciones visuales si no hay hábitos
- Confirmaciones para eliminar hábitos
- Indicación de datos locales, no sincronizados

---

## 🗃️ Modelado de datos

### Habit

```ts
interface Habit {
  id: string;
  name: string;
  color: string;
}
```
### HabitRecord

```ts
interface HabitRecord {
  date: string; // formato YYYY-MM-DD
  habitId: string;
  completed: boolean;
}
```

- Se almacena como arrays serializados en `localStorage`
- Claves sugeridas: `habits`, `records`

---

## 📖 Casos de uso clave (MVP)

| Caso de uso              | Descripción                             |
| ------------------------ | --------------------------------------- |
| Crear hábito             | Crear uno nuevo con nombre y color      |
| Editar hábito            | Modificar nombre/color de uno existente |
| Eliminar hábito          | Borrar hábito y registros asociados     |
| Ver hábitos de hoy       | Listado con posibilidad de marcar       |
| Marcar hábito como hecho | Toggle de estado completado             |
| Ver progreso semanal     | Mostrar barra o lista de 7 días         |
| Ver racha                | Mostrar cantidad de días consecutivos   |

---

## 🚫 Exclusiones del MVP

- Personalización profunda (etiquetas, iconos)
- Exportar/importar datos
- Backend / sincronización cloud
- PWA
- Vista mensual o de calendario

---

## 🎉 Iteraciones futuras posibles

- ✅ Sistema de gamificación:

  - Cada hábito otorga puntos al completarse
  - Los puntos pueden canjearse por recompensas reales
  - Visualización de puntos actuales y recompensas
  - Reglas de validación para evitar abuso

- Exportación/importación de datos (JSON)

- Instalación como PWA

- Historial completo con calendario

- Personalización de frecuencia por hábito (no solo diario)

---

## 🔄 Estados y comportamiento esperado

| Estado                  | Comportamiento                             |
| ----------------------- | ------------------------------------------ |
| Sin hábitos             | Mostrar mensaje de bienvenida              |
| Día sin registros       | Todos los hábitos están "no completados"   |
| Hábito eliminado        | Sus registros también se eliminan          |
| Datos corruptos         | Reset con fallback limpio y mensaje        |
| Cambio de fecha/sistema | El día actual se recalcula automáticamente |

---

## 📆 Navegación y pantallas previstas

1. **Inicio (Hoy)**

   - Lista de hábitos
   - Marcar como completado
   - Botón para agregar hábito

2. **Agregar / editar hábito**

   - Formulario con validación

3. **Estadísticas**

   - Progreso semanal
   - Racha

---

## ⚠️ Riesgos conocidos

- Dependencia total de `localStorage` (datos pueden borrarse)
- Cambio de zona horaria puede afectar fecha actual
- Eliminar hábitos borra su historial, sin posibilidad de recuperarlo

---

