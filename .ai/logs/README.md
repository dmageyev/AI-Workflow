# Журнал сесій (Sessions Log)

Ця папка містить **Handoff Packages** — набори артефактів передачі контексту між сесіями.

## Формат

Кожна сесія зберігається у підпапці з іменем у форматі `YYYY-MM-DD-HHmm-topic`:

```text
.ai/logs/sessions/
  YYYY-MM-DD-HHmm-topic/
    snapshot.yaml   ← машинозчитуваний стан (YAML)
    handoff.md      ← людиночитаний підсумок (Markdown)
    [artifact-*.md] ← опціональні додаткові артефакти
```

## Шаблони

- [`snapshot.template.yaml`](../prompts/handoff/snapshot.template.yaml)
- [`handoff.template.md`](../prompts/handoff/handoff.template.md)

## Правила

- Одна папка = одна сесія.
- Нова сесія = нова папка (навіть якщо topic той самий, але дата інша).
- `HHmm` (UTC) у назві дозволяє мати кілька сесій в один день без колізій.
- Поле `version` у snapshot.yaml інкрементується в межах одного topic.
- Не видаляй старі сесії — вони є частиною інституційної пам'яті.

## Протокол handoff

Детальний опис: [`.ai/docs/03-handoff-protocol.md`](../docs/03-handoff-protocol.md)
