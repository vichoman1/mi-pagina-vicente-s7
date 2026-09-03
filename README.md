# Buzón de ideas · Invia Accounting

Página pública de uso interno: el área de accounting de INVIA propone lugares
para la cena de fin de año y vota las propuestas, sin contraseña. Es un solo
archivo, `index.html`, publicado en <https://mi-pagina-vicente-s7.netlify.app>.

**De dónde salen los datos.** Ninguna propuesta ni cifra de votos está escrita
en el HTML: salen de las tablas `registros` y `votos` del proyecto
`curso-ejemplo` de Supabase, leídas desde el navegador con la llave
`sb_publishable_` que está a la vista en `index.html`. Cualquiera puede leer y
agregar; nadie puede borrar ni modificar, así que un voto no se puede quitar.
Las columnas de las dos tablas están en `CLAUDE.md`.

**Qué hay en `.claude`.** Solo `agents/revisor-antes-de-publicar.md`: define al
revisor que Claude usa cuando se le pide, que lee el cambio antes de publicarlo,
busca llaves secretas, código de más y errores, y entrega un informe sin
arreglar nada.

**Para continuar.** Abre una sesión de Claude sobre este repositorio y pide el
cambio en español; lee antes `CLAUDE.md`, con las reglas de trabajo y lo que
nunca se debe hacer. Fusionar a `main` republica la página sola, y el plan
gratuito de Netlify da unas veinte publicaciones al mes: revisa en la vista
previa de la rama, que es gratis, y fusiona poco. Si la página deja de mostrar
datos, Supabase se pausó: se despierta con **Resume project**.
