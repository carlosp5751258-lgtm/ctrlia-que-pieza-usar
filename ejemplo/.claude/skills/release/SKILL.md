---
name: release
description: Prepara las notas de versión desde el último tag. Úsala cuando pidan notas de versión o changelog.
disable-model-invocation: true
---

1. Lista los commits desde el último tag con `git log $(git describe --tags --abbrev=0)..HEAD --oneline`.
2. Agrúpalos en Novedades, Correcciones y Documentación.
3. Escribe el resultado en CHANGELOG.md sin borrar lo anterior.
