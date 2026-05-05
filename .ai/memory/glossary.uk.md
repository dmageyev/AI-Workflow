# Глосарій (UK)

Основні терміни проєкту `AI-Workflow`.

| Термін (EN) | Переклад/Пояснення (UA) |
| ----------- | ---------------------- |
| Agent | Агент — AI-сутність з певною роллю (Architect, Orchestrator тощо) |
| Handoff | Передача контексту ("свідомості") між агентами або сесіями |
| Handoff Package | Набір артефактів для передачі: snapshot.yaml + handoff.md |
| Snapshot | Машинозчитуваний стан проєкту у форматі YAML |
| Orchestrator | Координатор агентів, відповідальний за стан |
| Work item | Одиниця роботи (задача) з id, title, status |
| ADR | Architecture Decision Record — запис архітектурного рішення |
| Quality Gate | Контрольний чекліст перед завершенням сесії |
| Session | Один робочий цикл (від відновлення контексту до handoff) |
| Phase | Фаза проєкту (bootstrap / planning / execution / done) |
| Artifact | Файл-результат роботи агента |
| Bootstrap | Ініціальна фаза — розгортання структури репозиторію |
| Memory | Довготривала пам'ять проєкту ([`.ai/memory/`](.)) |
| Log | Тимчасовий журнал сесій ([`.ai/logs/`](../logs/)) |
| Recovery Protocol | Процедура відновлення після аварійного завершення сесії без Handoff Package |
| Emergency Handoff | Мінімальний handoff, створений постфактум для аварійно завершеної сесії |
| Session Structure Check | CI-перевірка наявності snapshot.yaml + handoff.md у кожній папці сесії |
| CODEOWNERS | Файл [`.github/CODEOWNERS`](../../.github/CODEOWNERS) — визначає відповідальних за review по шляхах репо |
| delegates_to | Поле реєстру агентів: кому агент може делегувати задачу |
| escalates_to | Поле реєстру агентів: до кого агент ескалює при блокерах або архітектурних питаннях |
