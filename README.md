# Dashboard de Ventas — Viajero Hostels Colombia

Dashboard interactivo de Performance AyB (Alimentos & Bebidas) para las 10 sedes de Viajero Hostels en Colombia: Bogotá, Cali, Cartagena Centro, Getsemaní, Guatapé, Medellín, Salento, San Andrés, Santa Marta y Tayrona.

## ¿Qué es esto?

Un único archivo `index.html` autocontenido que muestra ventas, cumplimiento de presupuesto y conversión de desayunos a partir de un archivo Excel de ventas, sin necesidad de backend ni base de datos.

## Estructura del dashboard

El dashboard tiene tres vistas, navegables desde el menú superior:

- **Sales Overview** — Ingresos totales, sede top, ranking de productos top por familia (Alimentos, Desayuno, Cócteles, Cerveza), mix por grupo mayor, evolución de venta diaria con ticket por huésped, y comportamiento por día de la semana.
- **Compliance Tracking** — Ranking de cumplimiento por sede (Ingresos, Costos, Ticket Noche Cama) comparando real vs. presupuesto, con evolución mensual.
- **Desayunos & Conversión** — Conversión real vs. meta de desayunos por sede y por mes.

## Flujo de actualización semanal

1. Se actualiza el archivo Excel (`VENTAS_COLOMBIA_-_JUNIO.xlsx` o el mes correspondiente) con los datos de ventas de la semana, en la hoja `VENTAS`.
2. Con ese Excel actualizado, se regenera el `index.html` (datos embebidos directamente en el archivo).
3. El `index.html` regenerado se sube a este repositorio, reemplazando el anterior.
4. GitHub Pages reconstruye el sitio automáticamente (1-2 minutos) y el dashboard publicado queda actualizado.

## Fuente de datos (hojas del Excel)

| Hoja | Contenido |
|---|---|
| `VENTAS` | Transacciones diarias por sede, grupo, familia y producto (venta con descuento y venta total) |
| `VENTAS POR HORAS` | Ventas desagregadas por franja horaria |
| `PPTO COL` | Presupuesto mensual de ingresos, costos y ticket por sede |
| `OCUPACION` | Noches-cama (huéspedes) diarias por sede — usada para calcular el ticket por huésped |
| `PERFORMANCE MENSUAL` | Ingresos y costos reales mensuales por sede (alimenta Compliance Tracking) |
| `META DESAYUNOS` | Meta de conversión y de unidades de desayuno por sede y mes |

## Notas importantes

- **Costo Real** en Compliance Tracking depende de que la hoja `PERFORMANCE MENSUAL` tenga la columna `REAL COSTO` llena para el mes en curso. Si está vacía, el dashboard muestra "Pendiente actualizar" en lugar de un dato incorrecto.
- **Ticket por huésped** en la gráfica de Venta por Día se calcula como ingresos del día (respetando los filtros de Grupo/Familia activos) dividido entre las noches-cama de ese día, tomadas de la hoja `OCUPACION`.
- El dashboard no requiere ningún proceso de build: es HTML/JS/CSS puro con los datos del Excel embebidos como JSON al momento de generarlo.

## Publicación

Este repositorio está desplegado con **GitHub Pages** desde la rama `main`. Cualquier cambio subido a `index.html` en main se refleja automáticamente en el sitio publicado.
