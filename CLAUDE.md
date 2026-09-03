# CLAUDE.md

Este archivo lo lee Claude cada vez que trabaja en esta carpeta, sin que se lo pidas.
Lo vas a llenar en la sesión. Por ahora trae solo las reglas que aplican desde el
primer minuto.

---

## 1. Qué es este proyecto y quién lo usa

Es un buzón de sugerencias y votos para la cena de fin de año de mi área.
La usan mis compañeros del área de accounting de INVIA.

## 2. De dónde sale cada cifra

Los datos de esta página viven en dos tablas de Supabase, en el proyecto
`curso-ejemplo`. Ninguna cifra ni ningún texto que se muestre se escribe a mano
en el HTML: todo sale de esas tablas o de lo que la persona escriba en el
formulario.

**`registros`** — una propuesta por renglón. Estas son las columnas que acabó
teniendo, en el orden real de la tabla:

| Columna | Qué guarda |
|---|---|
| `id` | Número del renglón; lo pone la base de datos |
| `nombre` | Quién lo propone |
| `mensaje` | Por qué lo recomienda |
| `creado_en` | Fecha y hora; la pone la base de datos |
| `lugar` | Nombre del lugar propuesto |

`lugar` queda al final porque se agregó después: la tabla nació solo con `nombre`
y `mensaje`. `nombre`, `mensaje` y `lugar` pueden quedar vacías en la base; quien
obliga a llenar las tres es el formulario de la página, no la tabla.

**`votos`** — un voto por renglón:

| Columna | Qué guarda |
|---|---|
| `id` | Número del renglón |
| `registro_id` | A qué propuesta apunta; es el `id` de un renglón de `registros` |
| `votante` | Identificador del navegador que votó |
| `creado_en` | Fecha y hora |

Aquí no hay columnas opcionales: las cuatro son obligatorias. `registro_id` está
amarrado a `registros` con `on delete cascade`, así que si algún día se borrara
una propuesta se irían con ella sus votos; hoy no puede pasar, porque nadie tiene
permiso de borrar.

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

- Trabaja siempre en una rama, nunca directo sobre `main`.
- **Termina cada cambio de principio a fin, sin detenerte a pedirme permiso a la
  mitad.** En cualquier rama que trabajes: abre el Pull Request, fusiónalo a
  `main` y despliega a producción — la página en Netlify y la base de datos en
  Supabase. No me dejes un Pull Request abierto esperando mi respuesta.
- Un cambio a la vez, para que cada Pull Request se pueda leer solo.
- Enséñame el SQL que corriste y qué cambió, **después** de hacerlo. Informarme,
  sí; detenerte a esperar, no.
- Si algo te bloquea de verdad y no puedes terminar, dímelo y explica qué falta.
  Un cambio a medias sin avisar es peor que uno que no se empezó.

## 4. Lo que nunca debes hacer

- **Nunca escribas en esta carpeta una llave que empiece con `sb_secret_` o que
  diga `service_role`.** La única llave que puede estar aquí es la que empieza
  con `sb_publishable_`, que está hecha para andar a la vista.
- No inventes datos. Si algo no está en la tabla, que la página diga que no hay
  nada todavía, no un ejemplo.
- No borres el historial ni fuerces cambios sobre lo ya publicado.
- **La única excepción a la regla de terminar sin preguntar: destruir.** Borrar
  una tabla o una columna que ya tenga datos, o quitarle permisos a una tabla,
  no se deshace con nada. Eso sí me lo preguntas antes. Agregar y cambiar, no.

## 5. Mi regla de verificación

Cierro con "Verificado:" y una lista de lo que probé. No puedo publicar nada sin
haber abierto la página y comprobado que hace lo que dice. Si algo no lo pude
probar, lo digo en vez de darlo por bueno.

## 6. Cómo vuelvo a abrir esto

- El repositorio: <https://github.com/vichoman1/mi-pagina-vicente-s7>
- Se abre pidiéndole a Claude una sesión sobre este repo; no hace falta descargarlo.
- La página publicada: <https://mi-pagina-vicente-s7.netlify.app>
  Se republica sola cada vez que algo entra a `main`; no hay que tocar Netlify.
- La base de datos: proyecto `curso-ejemplo` en supabase.com, en esta cuenta.

> **Si la página deja de mostrar datos después de una semana sin usarla**, casi
> siempre es que el proyecto gratuito de Supabase se pausó. Se despierta con el
> botón **Resume project**.
