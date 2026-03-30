# Estado actual del proyecto Jasboot

Documento consolidado del estado del proyecto; rutas actualizadas (2026-03-27).

---

## 1. Estructura del proyecto (solo componentes esenciales)

```
jasboot/
├── bin/
│   ├── jbc.exe / jbc.cmd   # Compilador estable (.jasb → .jbo)
│   └── jb.cmd              # Atajo: jbc + VM (salida en build/)
├── build/                  # Salida típica de jb.cmd (.jbo); se regenera al compilar
├── docs/
├── scripts/                # export GitHub, limpieza de artefactos
├── tests/
└── sdk-dependiente/
    ├── jasboot-jmn-core/   # JMN + platform_compat (build de la VM)
    ├── jasboot-ir/         # VM: ejecuta .jbo
    │   ├── src/
    │   ├── build_vm.bat
    │   └── Makefile
    ├── jas-compiler-c/     # Compilador estable (jbc)
    └── jas-runtime/        # Runtime auxiliar (C)
```

---

## 2. Componentes esenciales

| Componente | Ruta | Función |
|------------|------|---------|
| **VM** | `sdk-dependiente/jasboot-ir/` | Ejecuta binarios `.jbo`; depende de `jasboot-jmn-core/` (memoria neuronal, platform_compat). |
| **JMN / runtime** | `sdk-dependiente/jasboot-jmn-core/` | JMN, compatibilidad de plataforma; enlazado por la VM. |
| **Compilador (único soportado en árbol)** | `sdk-dependiente/jas-compiler-c/` → `bin/jbc.exe` | Compila `.jasb` → `.jbo`; implementación de referencia estable. |
| **CLI cómoda** | `bin/jb.cmd` | Compila con `jbc` y ejecuta el `.jbo` con la VM; escribe en `build/`. |

---

## 3. Cómo compilar y ejecutar

### Compilar la VM (una vez)

- **Windows:** `sdk-dependiente\jasboot-ir\build_vm.bat`
- **Linux/macOS:** `cd sdk-dependiente/jasboot-ir && make`

Requisitos: `gcc` (C11), árbol **`jasboot-jmn-core`** resuelto (ruta por defecto o `JASBOOT_JMN_ROOT`).

### Ejecutar un programa Jasboot

```
bin\jb.cmd archivo.jasb [argumentos...]
```

Ejemplo: `bin\jb.cmd hola.jasb`

`jb.cmd` compila `archivo.jasb` a `build/archivo.jbo` con **jbc** y ejecuta la VM. Si no pasas argumentos al programa, usa `jbc … -e` (mismo cwd que el `.jasb`). Con argumentos adicionales, compila y lanza la VM con `%2`…`%9`.

### Compilar manualmente (sin ejecutar)

```
bin\jbc.exe archivo.jasb -o archivo.jbo
sdk-dependiente\jasboot-ir\bin\jasboot-ir-vm.exe archivo.jbo
```

---

## 4. Dependencias

| Dependencia | Uso |
|-------------|-----|
| **gcc** (C11) | Compilador (jbc), VM y core |
| **jasboot-jmn-core/** | Memoria neuronal, platform_compat (obligatorio para la VM) |

---

## 5. Estado de cada componente

### VM (sdk-dependiente/jasboot-ir)
- ✅ Ejecuta IR binario estable
- ✅ JMN integrada
- ✅ Opcodes de IA (OP_MEM_*, etc.)
- ⚠️ Persistencia de cerebro.jmn parcial

### Compilador C (sdk-dependiente/jas-compiler-c)
- ✅ Implementación de referencia estable
- ✅ Cubre sintaxis amplia (vars, funciones, control de flujo)
- ✅ No requiere Python

---

## 6. Limpieza acumulada

**Eliminado (2026-03-27) — núcleo solo lenguaje:**
- Carpetas de producto / legado en raíz: `api/`, `core/`, `curso/`, `data/`, `escala/`, `generacion/`, `ingesta/`, `modulos-jasb/`, `publish/`, `replica/`, `sdk/`, `sdk-soberano/`, `temp_work/`, `export/`, artefactos `build/` sueltos.
- `sdk-dependiente/jas-ia/`, `sdk-dependiente/jasboot-ir/core/` (árbol duplicado).
- Documentación no esencial bajo `docs/`: `IA/`, `API/`, `KERNEL/`, `UI/`.
- Basura en raíz: logs, `.jbo` de prueba, `.exe` duplicados, `jasboot.ps1` (apuntaba a compilador Python eliminado).

**Eliminado (2026-03-25):**
- `sdk-soberano/jas-compiler/` (compilador en Jasboot duplicado; confundía con **jbc**)
- `bin/jb-soberano.cmd`; binarios redundantes `jbc_new.exe`, `jbc_test.exe`, `jbc_minimal.exe`, `jbc_build.exe`

**Eliminado (2026-02-18 y anteriores):**
- `archive/`, `historia-proyecto/`
- `jasboot-py/`, `jasboot/` (extensión VS Code)
- `sdk-soberano/jas-IA/`, `sdk-soberano/jas-ir/`, `sdk-soberano/jas-cli/`
- `sdk-dependiente/jas-compiler/` (compilador Python; reemplazado por jas-compiler-c)
- `jas-robustest/`, `jas-docs/`
- Archivos de debug (`debug_*.jasb`, `debug_tokens.py`)
- Documentación redundante (Sintaxis, historia, archive, reports, test, etc.)

**Actualizado:**
- `bin/jb.cmd`: compila y ejecuta siempre con **jbc** + VM (se eliminó la variante soberano/main.jbo).
- Referencias en [pipeline-osia.md](pipeline-osia.md).

---

## 7. Documentación pública (este repositorio)

Índice general: [README del árbol `docs/`](../README.md).

**Planes de trabajo, tablas de seguimiento y catálogos de tests** (roadmap por fases, checklist de compilador, de drivers/3D, calidad de tests, etc.) **no** se publican en GitHub: viven solo en el **monorepo de desarrollo** Jasboot, bajo `docs/PROYECTO/` y `docs/TECNICO/SDK/`.

| Documento | Contenido |
|-----------|-----------|
| [estado-actual.md](estado-actual.md) | Este documento |
| [pipeline-osia.md](pipeline-osia.md) | Orden de implementación hacia OS-IA |
| [independencia-host-v1.md](independencia-host-v1.md) | Capa de abstracción del host |
| [../tecnico/vm/vm-estable.md](../tecnico/vm/vm-estable.md) | VM oficial y uso |
| [../lenguaje/inicio-rapido.md](../lenguaje/inicio-rapido.md) | Sintaxis mínima (inicio rápido) |
| [contrato-runtime-v1.md](contrato-runtime-v1.md) | Semántica del runtime |
| [catalogo-errores-v1.md](catalogo-errores-v1.md) | Códigos de error |

---

**Última actualización:** 2026-03-29
