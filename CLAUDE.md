# CLAUDE.md

Este archivo lo lee Claude cada vez que trabaja en esta carpeta, sin que se lo pidas.
Lo vas a llenar en la sesión. Por ahora trae solo las reglas que aplican desde el
primer minuto.

---

## 1. Qué es este proyecto y quién lo usa

*(Lo escribes tú en la sesión: dos líneas. Qué es la página, para quién es y cada
cuándo se usa.)*

## 2. De dónde sale cada cifra

Los datos de esta página viven en dos tablas de Supabase, en el proyecto
`curso-ejemplo`. Ninguna cifra ni ningún texto que se muestre se escribe a mano
en el HTML: todo sale de esas tablas o de lo que la persona escriba en el
formulario.

**`registros`** — una propuesta por renglón:

| Columna | Qué guarda |
|---|---|
| `id` | Número del renglón; lo pone la base de datos |
| `lugar` | Nombre del lugar propuesto |
| `nombre` | Quién lo propone |
| `mensaje` | Por qué lo recomienda |
| `creado_en` | Fecha y hora; la pone la base de datos |

**`votos`** — un voto por renglón:

| Columna | Qué guarda |
|---|---|
| `id` | Número del renglón |
| `registro_id` | A qué propuesta apunta |
| `votante` | Identificador del navegador que votó |
| `creado_en` | Fecha y hora |

Los votos se cuentan sumando renglones de `votos`, **no** con un número que sube.
Es a propósito: nadie puede modificar renglones, así que un contador sería
imposible. La consecuencia a tener presente es que **un voto no se puede quitar.**

La regla `unique (registro_id, votante)` impide votar dos veces por la misma
propuesta desde el mismo navegador. Es un voto por navegador, no por persona:
quien borre los datos de su navegador o entre desde otro aparato puede votar de
nuevo. Sin pedir que la gente inicie sesión, no se puede ir más lejos.

**Permisos de las dos tablas: cualquiera puede leer y agregar; nadie puede
borrar ni modificar.**

## 3. Cómo quiero que trabajes aquí

- Antes de un cambio grande, dame el plan por escrito y espera mi visto bueno.
- Un cambio a la vez. Enséñame qué cambió antes de escribirlo.
- Trabaja siempre en una rama, nunca directo sobre `main`.
- No publiques a producción sin que yo lo pida: fusionar es una decisión mía.
- **Si tienes acceso a mi base de datos, enséñame el SQL antes de correrlo y espera mi
  respuesta.** Crear o borrar tablas, agregar o quitar columnas y cambiar permisos no se
  deshacen con una rama: en cuanto corren, ya está.

## 4. Lo que nunca debes hacer

- **Nunca escribas en esta carpeta una llave que empiece con `sb_secret_` o que
  diga `service_role`.** La única llave que puede estar aquí es la que empieza
  con `sb_publishable_`, que está hecha para andar a la vista.
- No inventes datos. Si algo no está en la tabla, que la página diga que no hay
  nada todavía, no un ejemplo.
- No borres el historial ni fuerces cambios sobre lo ya publicado.

## 5. Mi regla de verificación

*(La escribes tú en la sesión: con qué frase cierras lo que entregas y qué tiene
que ser cierto para que puedas publicarlo.)*

## 6. Cómo vuelvo a abrir esto

- El repositorio: <https://github.com/vichoman1/mi-pagina-vicente-s7>
- Se abre pidiéndole a Claude una sesión sobre este repo; no hace falta descargarlo.
- La página publicada: <https://mi-pagina-vicente-s7.netlify.app>
  Se republica sola cada vez que algo entra a `main`; no hay que tocar Netlify.
- La base de datos: proyecto `curso-ejemplo` en supabase.com, en esta cuenta.

> **Si la página deja de mostrar datos después de una semana sin usarla**, casi
> siempre es que el proyecto gratuito de Supabase se pausó. Se despierta con el
> botón **Resume project**.
