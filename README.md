# Entregas · Agenda académica (React)

**Integrantes:** Maximiliano Valdés

## Descripción de la problemática

Los estudiantes universitarios pierden el control de tareas, controles y proyectos de varias asignaturas. Plazo permite registrarlos, filtrarlos, cambiar su estado, ver el avance y detectar entregas que caen en feriado.

## Usuarios objetivo

Estudiantes universitarios.

## Funcionalidades principales

- Panel con indicadores de avance y entregas por vencer.
- Crear, editar y eliminar actividades, con validación del formulario.
- Estados (pendiente, en progreso, completada) y **prioridades** (alta, media, baja).
- Filtros por asignatura, estado y prioridad.
- **Calendario mensual** con entregas y feriados.
- Avance por asignatura.
- Datos guardados en el navegador (localStorage).
- Consulta de feriados mediante una API pública.

## Tecnologías utilizadas

React 18, Vite, React Router, Bootstrap 5, CSS3, Fetch API, Git, GitHub y Git Flow.

## Cómo ejecutarlo

Requiere tener Node.js instalado.

```bash
npm install
npm run dev
```

## Estructura general

- `src/pages`: Panel, Actividades, Calendario, Asignaturas.
- `src/components`: Navbar, ResumenAvance, TarjetaActividad, FormularioActividad, BarraFiltros, AlertaFeriados.
- `src/data`: JSON con asignaturas y actividades iniciales.
- `src/services`: llamada a la API pública.
- `src/hooks`: `useAlmacenamiento` (estado + localStorage) y `useFeriados` (API con carga y error).
- `src/utils`: cálculo de fechas y plazos.
- `docs/diseno-previo.md`: mapa de navegación, wireframes, jerarquía visual, paleta y flujos.

## Evolución desde el proyecto inicial

Plazo parte de la Actividad Evaluada 1 (HTML, Bootstrap y JavaScript puro). Así se tradujo cada parte a React:

| Proyecto inicial | Plazo (React) |
|---|---|
| `renderIndicadores()` dibujaba las tarjetas y la barra de avance | Componente `ResumenAvance` |
| Formulario con `validar()` y la variable `editandoId` | Componente `FormularioActividad` y estado `idEdicion` en la página Actividades |
| `renderLista()` creaba cada tarjeta con plantillas de texto | Componente `TarjetaActividad` y `.map()` con `key` |
| Selects de filtro con `addEventListener` | Componente `BarraFiltros` con estado (`useState`) |
| `diasRestantes()` y `textoPlazo()` | `src/utils/fechas.js` (más `esUrgente`) |
| Array `actividades` en memoria | Estado en `App` guardado en localStorage (`useAlmacenamiento`) |
| Lista de asignaturas | Página Asignaturas, ahora con avance por asignatura |

**Novedades de la versión React:** navegación entre cuatro páginas (React Router), prioridades, calendario mensual, persistencia en localStorage y consumo de una API pública de feriados.

## API pública: Nager.Date (feriados)

- **Documentación oficial:** https://nagerholidays.com/api
- **Endpoint usado:** `https://date.nager.at/api/v3/PublicHolidays/{año}/CL`
- **Método HTTP:** GET
- **Parámetros:** año (se consultan el actual y el siguiente) y código de país `CL`.
- **Datos usados:** `date` y `localName`, transformados a `{ fecha, nombre }` en `src/services/feriadosApi.js`.
- **Dónde se muestran:** componente `AlertaFeriados` en el Panel y marcas en el Calendario (hook `useFeriados`).
- **Si falla:** se muestra un aviso y el resto de la app sigue funcionando; mientras carga, un mensaje de espera.
- **Restricciones y autenticación:** no requiere clave. La documentación oficial indica que no hay límite de solicitudes; la app realiza 2 por carga. El servicio no garantiza disponibilidad, por eso la app maneja el error.
- **Licencia y condiciones de uso:** Nager.Date es de código abierto. Según sus [términos de servicio](https://nagerholidays.com/legal/termsofservice), la API es gratuita para proyectos privados o sin fines de lucro (el uso comercial requiere patrocinio) y no puede usarse para operar un portal propio de feriados. Este proyecto es académico y sin fines de lucro. Los términos no exigen atribución, pero se cita la fuente: Nager.Date.
- **Justificación funcional:** avisa cuando una entrega pendiente coincide con un feriado, algo que una agenda común no hace.

## Uso de Inteligencia Artificial

**Herramienta:** Claude (Anthropic).

### 1. Elección de la API
- **Propósito:** encontrar una API pública pertinente para una agenda académica.
- **Prompt (resumido):** "Necesito una API pública para una agenda académica hecha con React, que sea relevante para este caso."
- **Resultado:** propuso la API de feriados Nager.Date y su integración con `useEffect`.
- **Modificación humana:** adopté la API propuesta y probé en el navegador que funcionara.

### 2. Migración de elementos a componentes JSX
- **Propósito:** pasar algunos elementos de mi proyecto inicial (formulario, tarjetas de actividad, filtros e indicadores de avance) a componentes React.
- **Prompt (resumido):** "Ayúdame a pasar algunos elementos de mi proyecto inicial (HTML, CSS y JavaScript) a componentes React con JSX."
- **Resultado:** convirtió esos elementos en componentes JSX, que utilicé como ejemplo.
- **Modificación humana:** a partir de ese ejemplo, convertí por mi cuenta el resto de los componentes y probé la aplicación en el navegador, donde funcionó correctamente.

### 3. Jerarquía visual y colores
- **Propósito:** mejorar la jerarquía visual usando el verde lima como color base.
- **Prompt (resumido):** "Quiero mejorar la jerarquía visual de la web usando el verde lima como color base. ¿Qué cambios de color en el CSS y qué reubicación de elementos recomiendas?"
- **Resultado:** sugirió ajustes de colores en el CSS y cambios de ubicación de algunos bloques.
- **Modificación humana:** decidí el color base y pedí su opinión antes de aplicar los cambios.

### 4. README y comandos de Git
- **Propósito:** redactar el README y recordar los comandos de Git Flow.
- **Prompt (resumido):** "Con base en este proyecto, redacta un README que cumpla los siguientes requerimientos: [requisitos del enunciado]. Te entrego la información relevante del proyecto: [descripción, API, tecnologías]."
- **Resultado:** estructura del README y comandos de Git para `main`, `develop`, ramas `feature/` y Pull Requests.
- **Modificación humana:** completé yo la información de integrantes, API y este reporte.

### Aprendizaje
Aprendí a convertir elementos de mi proyecto inicial en componentes JSX y, a partir de ese ejemplo, logré hacer por mi cuenta el resto de los componentes. También aprendí a utilizar e integrar una API pública con `fetch` y a conocerla de verdad (endpoint, parámetros, datos que devuelve y condiciones de uso), ya que al comienzo solo me la mostró la IA. Por último, recordé y comprendí mejor conceptos de jerarquía visual que no tenía del todo claros.

## Git Flow

Ramas `main` y `develop`; una rama `feature/` por funcionalidad, integrada con Pull Request.

## Limitaciones conocidas

- Los datos viven en el navegador (localStorage): no hay backend, cuentas ni sincronización entre dispositivos.
- La API de feriados depende de la conexión a internet y solo se consultan los feriados de Chile.