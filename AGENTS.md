# AGENTS.md — AltServer-Linux

## Старт сессии

1. Выполнить `git status -sb`; отметить текущую ветку, целевой base/target если задан, и существующие незакоммиченные изменения.
2. Перед нетривиальными правками прочитать `README.md` и `CONTRIBUTING.md`; для подпапок дополнительно читать ближайший `AGENTS.md`.
3. Если задача затрагивает submodules: выполнить `git submodule status --recursive`; при грязном submodule проверить его `git status` и не нормализовать без команды пользователя.

## Инвариант проекта

Это Linux-порт AltServer поверх `upstream_repo`. Изменения должны легко отделяться от upstream и переноситься дальше: меньше слоёв, меньше переписывания, понятный diff.

Обычные зоны правок: `src/`, `shims/`, `makefiles/`, `scripts/`, документация. Не менять `libraries/*` и `upstream_repo` без явной задачи на submodule/upstream-правку; сначала искать решение в `src/`, `shims/` или правилах rewrite в `makefiles/`.

## Если задача затрагивает submodules

- `libraries/*`: только стабильные теги, без `rc`, `beta`, `alpha`.
- `upstream_repo`: явный SHA целевого upstream.
- Не оставлять dirty state или локальные detached-коммиты внутри submodules.
- Патч библиотеки — только если workaround в этом repo невозможен; дальше public fork и отдельный gitlink commit.

## Проверки

- Код или сборка: выполнить базовую сборку из `README.md` / `CONTRIBUTING.md`.
- Dependencies, `buildenv/` или платформенные флаги: выполнить Docker/CI-сборку либо явно написать, почему она не запускалась.
- Install, transport, mux или AFC/write path (`Writing to device...`): выполнить device matrix из `CONTRIBUTING.md`; указать USB/Wi‑Fi, `usbmuxd`/`netmuxd` и скорость в `MB/s = bytes / seconds / 1_000_000`.
- Для замеров сначала пробовать `scripts/device-bench.sh`.
- iOS trust/developer prompts считать ручными; не имитировать их автоматизацией.

## Безопасность и артефакты

Не коммитить секреты, pairing/provisioning материалы и сгенерированные артефакты; точный список — в `.gitignore` и `CONTRIBUTING.md`. Перед публикацией логов редактировать UDID, Apple account и локальные пути.

## Коммиты и PR

Если готовишь commit/PR: Conventional Commits, малые логические изменения, отдельно docs/build/runtime, краткая проверка в описании. Если нужная device-проверка не выполнена, написать это явно.
