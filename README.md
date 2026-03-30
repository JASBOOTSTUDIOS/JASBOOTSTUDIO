<p align="center">
  <img src="assets/jasboot-icon.png" alt="Jasboot — logo del lenguaje" width="140" height="140">
</p>

<h1 align="center">JASBOOTSTUDIO</h1>

<p align="center">
  <strong>Documentación oficial y pública de Jasboot</strong><br>
  Lenguaje de programación con memoria neuronal (JMN), máquina virtual e IR binario (<code>.jbo</code>).
</p>

<p align="center">
  <a href="https://github.com/JASBOOTSTUDIOS/sdk-dependiente">SDK en C (jbc + VM)</a>
  &nbsp;·&nbsp;
  <a href="docs/README.md">Índice de <code>docs/</code></a>
  &nbsp;·&nbsp;
  <a href="docs/lenguaje/inicio-rapido.md">Inicio rápido</a>
</p>

---

## Qué es Jasboot

**Jasboot** es un lenguaje pensado para combinar programación clásica (tipos, funciones, control de flujo, FFI) con un modelo de **memoria neuronal** integrado: conceptos persistentes, asociaciones y operaciones de alto nivel sobre un grafo de conocimiento. El código fuente usa extensión **`.jasb`**.

El flujo habitual de ejecución es:

1. **Compilar** con **`jbc`** (compilador en C): `.jasb` → **`.jbo`** (IR binario).
2. **Ejecutar** con **`jasboot-ir-vm`**, que interpreta el IR y enlaza la JMN y el resto del runtime.

Todo el toolchain estable vive en el repositorio **[sdk-dependiente](https://github.com/JASBOOTSTUDIOS/sdk-dependiente)** (compilador, VM, núcleo JMN). **Este repositorio** concentra la **documentación legible por humanos**: sintaxis, semántica, VM, formatos y estado del proyecto.

---

## Qué encontrarás en este repositorio

| Área | Descripción |
|------|-------------|
| **[`docs/lenguaje/`](docs/lenguaje/)** | Referencia del lenguaje, conceptos y JMN, estándar de carpetas para proyectos `.jasb`, resumen de sintaxis. |
| **[`docs/tecnico/`](docs/tecnico/)** | VM, formato JMN, grafo **n_**, NGF, FFI, heap, evaluación de capacidades para drivers y gráficos 3D. |
| **[`docs/proyecto/`](docs/proyecto/)** | Estado del árbol de desarrollo, visión de capas hacia OS-IA, contratos de runtime, catálogo de errores, guías puntuales. |

Los **checklists internos**, el **catálogo maestro de instrucciones/tests** y tablas de seguimiento con casillas **no** se publican aquí: permanecen en el monorepo de trabajo del equipo (`docs/PROYECTO/`, `docs/TECNICO/SDK/` en el workspace completo Jasboot).

---

## Mapa rápido de documentos

### Lenguaje

| Documento | Contenido |
|-----------|-----------|
| [Inicio rápido](docs/lenguaje/inicio-rapido.md) | Sintaxis mínima para leer o escribir tus primeros `.jasb`. |
| [Referencia del lenguaje](docs/lenguaje/referencia-lenguaje.md) | Sintaxis y semántica alineadas con **jbc** (tipos, control de flujo, JMN, FFI, listas, matrices, etc.). |
| [Conceptos y JMN](docs/lenguaje/conceptos-y-jmn.md) | Paradigma de conceptos, memoria neuronal y operaciones asociadas. |
| [Estándar de proyectos](docs/lenguaje/estandar-proyectos.md) | Cómo organizar `src/`, `tests/`, `data/` y `docs/` en paquetes Jasboot. |

### Técnico (VM, formatos, compilador)

| Documento | Contenido |
|-----------|-----------|
| [VM estable](docs/tecnico/vm/vm-estable.md) | Comportamiento de la VM, JMN integrada, opcodes relevantes. |
| [Formato JMN](docs/tecnico/formato-jmn.md) | Persistencia y estructura de la memoria neuronal en fichero. |
| [Coexistencia memoria / n_grafo](docs/tecnico/coexistencia-memoria-n-grafo.md) | JMN clásica y grafo de triples **n_** en paralelo. |
| [Predicados n_grafo](docs/tecnico/predicados-estandar-n-grafo.md) | Predicados estándar sobre el grafo. |
| [Especificación NGF v1](docs/tecnico/spec-formato-ngf-v1.md) | Formato binario `.ngf`. |
| [Particionado n_grafo](docs/tecnico/estrategia-particionado-n-grafo.md) | Estrategia de partición del grafo. |
| [FFI — convención de llamada](docs/tecnico/sdk/ffi-convencion-llamada.md) | Llamar código nativo (DLL/SO) desde Jasboot. |
| [Heap y memoria](docs/tecnico/sdk/heap-memoria.md) | Reserva y liberación en VM. |
| [Capacidades drivers / 3D](docs/tecnico/sdk/capacidades-drivers-3d.md) | Qué ofrece hoy **jbc**+VM para bajo nivel y gráficos (texto explicativo). |

### Proyecto y contratos

| Documento | Contenido |
|-----------|-----------|
| [Estado actual](docs/proyecto/estado-actual.md) | Estructura del monorepo típico, componentes y cómo compilar/ejecutar. |
| [Pipeline OS-IA](docs/proyecto/pipeline-osia.md) | Orden de capas desde hardware hasta aplicaciones cognitivas. |
| [Independencia del host v1](docs/proyecto/independencia-host-v1.md) | Capa de abstracción respecto al sistema anfitrión. |
| [Contrato de runtime](docs/proyecto/contrato-runtime-v1.md) | Crear/leer/actualizar/olvidar conceptos y errores del runtime. |
| [Catálogo de errores](docs/proyecto/catalogo-errores-v1.md) | Identificadores y mensajes sugeridos en español. |
| [Alcance y shadowing](docs/proyecto/notas-alcance-y-shadowing.md) | Reglas de visibilidad de variables. |
| [Tipos función (diseño futuro)](docs/proyecto/pendiente-tipos-funcion.md) | Nota de diseño para funciones de orden superior nombradas. |
| [Flechas y `macro`](docs/proyecto/guia-flechas-y-macro.md) | Sintaxis `(x) => …`, IIFE y alias con `macro`. |

Índice detallado por carpetas: **[`docs/README.md`](docs/README.md)**.

---

## Código y compilación

Clona y construye el SDK desde **[JASBOOTSTUDIOS/sdk-dependiente](https://github.com/JASBOOTSTUDIOS/sdk-dependiente)**. Allí tienes `jas-compiler-c` (**jbc**), `jasboot-ir` (VM), `jasboot-jmn-core` y scripts de build para Windows.

Resumen operativo (después de compilar): compilar un programa con **`jbc`**, ejecutar el **`.jbo`** con **`jasboot-ir-vm`**, o usar atajos del propio árbol (`jb.cmd`, etc.) como se describe en [estado actual](docs/proyecto/estado-actual.md).

---

## Para quién es este repo

- **Programadores** que quieren aprender Jasboot o consultar la semántica oficial.
- **Mantenadores del compilador o la VM** que necesitan contratos y textos de referencia enlazables.
- **Colaboradores** que buscan el marco conceptual (JMN, n_grafo, FFI) sin hojas de trabajo internas.

---

## Organización en GitHub

| Recurso | Enlace |
|---------|--------|
| Documentación (este repo) | [github.com/JASBOOTSTUDIOS/JASBOOTSTUDIO](https://github.com/JASBOOTSTUDIOS/JASBOOTSTUDIO) |
| Toolchain C (jbc, VM, JMN) | [github.com/JASBOOTSTUDIOS/sdk-dependiente](https://github.com/JASBOOTSTUDIOS/sdk-dependiente) |

---

<p align="center">
  <sub>Icono del lenguaje: mismo activo visual usado en la extensión <strong>vscode-jasboot</strong> del SDK.</sub>
</p>
