# Buzón de ideas · Invia Accounting

Una página interna donde el área de accounting de INVIA propone lugares para la
cena de fin de año y vota los de los demás, sin contraseña: quien tenga la liga
participa. Es un solo archivo, `index.html`, publicado en <https://mi-pagina-vicente-s7.netlify.app>.

## De dónde salen los datos

Nada de lo que se ve está escrito en el HTML: las propuestas salen de la tabla
`registros` y los votos de `votos`, en el proyecto `curso-ejemplo` de Supabase.
La página las lee desde el navegador con la llave `sb_publishable_` que está a la
vista en `index.html`. Cualquiera puede leer y agregar; nadie puede borrar ni
modificar, así que un voto no se puede quitar. Las columnas están en `CLAUDE.md`.

## Qué hay en `.claude`

`.claude/agents/revisor-antes-de-publicar.md`: un revisor que Claude usa cuando se
le pide. Lee el cambio antes de publicarlo, busca llaves secretas, código de más y
errores, y entrega un informe. No arregla nada.

## Para continuar

Abre una sesión de Claude sobre este repositorio y pide el cambio en español. Lee
antes `CLAUDE.md`: ahí están las reglas (trabajar en rama, Pull Request, fusionar
y desplegar) y lo que nunca se debe hacer. Cada fusión a `main` republica la
página sola; si deja de mostrar datos, Supabase se pausó y se despierta con
**Resume project**.
