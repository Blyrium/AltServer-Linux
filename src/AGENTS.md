# AGENTS.md (`src/`)

`src/` содержит Linux-замены для исходников из `upstream_repo/AltServer`. Перед правкой сверить соответствующий upstream-файл и вызывающие места.

- Держать изменения узко Linux-specific и сохранять upstream-поведение, если изменение поведения не является целью.
- Предпочитать маленький override или compatibility shim большому переписыванию flow.
- Для Anisette, install, transport, mux и AFC/write path описывать reproduction/проверку в commit или PR notes.
- В логах и примерах не печатать секреты, UDID и локальные пути.
