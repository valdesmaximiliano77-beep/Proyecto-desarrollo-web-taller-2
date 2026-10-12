# Plazo · Agenda académica (React)

**Integrantes:** (completar)

**Problemática:** los estudiantes pierden el control de tareas, controles y proyectos de varias asignaturas. Plazo permite registrarlos, filtrarlos, cambiar su estado, ver el avance y detectar entregas que caen en feriado.

**Usuarios:** estudiantes universitarios.

**Funcionalidades:** panel con indicadores y entregas por vencer · crear, editar y eliminar actividades con validación · estados y **prioridades** (alta, media, baja) · filtros por asignatura, estado y prioridad · **calendario mensual** con entregas y feriados · avance por asignatura · datos guardados en el navegador · consulta de feriados.

**Tecnologías:** React 18, Vite, React Router, Bootstrap 5, CSS3, Fetch API, Git/GitHub/Git Flow.

## Cómo ejecutarlo
```bash
npm install
npm run dev
```

## Estructura
- `src/pages`: Panel, Actividades, Calendario, Asignaturas.
- `src/components`: Navbar, ResumenAvance, TarjetaActividad, FormularioActividad, BarraFiltros, AlertaFeriados.
- `src/data`: JSON con asignaturas y actividades iniciales.
- `src/services`: llamada a la API pública.
- `src/hooks`: `useAlmacenamiento` (estado + localStorage) y `useFeriados` (API con carga y error).
- `docs/diseno-previo.md`: mapa de navegación, wireframes, jerarquía visual, paleta y flujos.
- `src/utils`: cálculo de fechas y plazos.

## API pública: Nager.Date (feriados)
- **Documentación oficial:** https://date.nager.at/Api (verificar endpoint, límites y licencia antes de entregar)
- **Endpoint usado:** `GET https://date.nager.at/api/v3/PublicHolidays/{año}/CL`, sin clave.
- **Datos usados:** `date` y `localName`, transformados a `{ fecha, nombre }` en `src/services/feriadosApi.js`.
- **Dónde se muestran:** componente `AlertaFeriados` en el Panel y marcas en el Calendario (hook `useFeriados`).
- **Si falla:** se muestra un aviso y el resto de la app sigue funcionando; mientras carga, un mensaje de espera.
- **Por qué aporta:** avisa cuando una entrega pendiente coincide con un feriado.

## Uso de Inteligencia Artificial
Herramienta: Claude (Anthropic). Completar cada fila con lo que realmente ocurrió.

| Uso | Qué hizo la IA | Qué hice yo |
|---|---|---|
| Elegir la API y cómo aplicarla | Propuso la API de feriados y su integración con `useEffect` | (completar) |
| Migrar la app de HTML/JS a React | Generó la estructura de componentes, páginas, hook y servicio | (completar: revisión, cambios de nombres, pruebas) |
| Validación de fechas y formulario | Generó la validación y los límites de fecha | (completar) |
| Diseño previo | Propuso mapa de navegación, wireframes y paleta | (completar) |
| Prioridades y calendario | Generó el campo de prioridad, filtros y la vista de calendario | (completar) |

Prompt de ejemplo: (copiar uno real) · Cómo verifiqué el resultado: (completar) · Qué aprendí: (completar)

## Git Flow
Ramas `main` y `develop`; una rama `feature/` por funcionalidad, integrada con Pull Request.

## Limitaciones
Los datos viven en el navegador (localStorage), sin backend ni cuentas. La API de feriados depende de conexión a internet.
