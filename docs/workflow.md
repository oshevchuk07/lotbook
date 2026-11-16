# Як працювати з проектом

Шпаргалка для себе. Команди для PowerShell. Якщо забув, що робити далі, відкривай цей файл і `docs/STATUS.md`.

## Мова

- Код, ідентифікатори, **коментарі в коді**, коміти, назви PR, ADR, README, CLAUDE.md: **англійською**
- `plan.md`, `STATUS.md`, `workflow.md`, devlog, stage-файли: українською

## Цикл одного кроку

1. **Вибери крок** зі stage-файлу (або з issue). Зрозумій критерій завершення.
2. **Оновись і створи гілку:**
   ```powershell
   git switch main
   git pull
   git switch -c feat/stock-movement-entity
   ```
   Префікси гілок: `feat/`, `fix/`, `docs/`, `chore/`, `refactor/`, `test/`.
3. **Працюй дрібними комітами** (коли зроблено логічний шматок, який можна описати одним рядком):
   ```powershell
   git status
   git add -p
   git commit -m "feat(inventory): add stock movement entity"
   ```
4. **Тест перед комітом** для логіки з правилами (гроші, ledger, калькулятор).
5. **Запуш і відкрий PR:**
   ```powershell
   git push -u origin HEAD
   ```
   Далі на GitHub: Compare & pull request, заповни шаблон. Якщо встановлено GitHub CLI: `gh pr create`.
6. **Заповни чекліст у PR**, перевір, що CI зелений.
7. **Merge → Squash and merge.** У повідомленні squash залиш формат Conventional Commits.
8. **Очисти:**
   ```powershell
   git switch main
   git pull
   git branch -d feat/stock-movement-entity
   git fetch --prune
   ```
9. **Закрий крок:** відміть у stage-файлі, оновити `STATUS.md`, запис у devlog (можна в тому ж PR до мержу).

## Формат коміту (Conventional Commits)

```
<type>(<scope>): <short description in English, imperative>
```

Типи: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`, `build`.
Scope: назва модуля (`inventory`, `purchasing`, `sales`, `pricing`, `mobile`, `infra`, `docs`).
Приклад: `fix(purchasing): round shared costs to minor units`.

## Що і куди оновлювати

| Що сталося | Що оновити |
|---|---|
| Прийняв архітектурне рішення | новий ADR у `docs/adr/` |
| З'явився новий термін або правило домену | `docs/domain.md` |
| Завершив крок | відмітка в stage-файлі, `STATUS.md` |
| Завершив сесію | запис у `docs/devlog/`, `STATUS.md` |
| Змінився загальний план | `docs/plan.md` + рядок у changelog внизу |
| Змінилась команда запуску/тестів | `README.md`, секція Commands у `CLAUDE.md` |
| Завершив етап | ретро (у stage-файлі), тег, оновити `plan.md` |

Правило: оновлення docs входить у Definition of Done кроку, не відкладай.

## Завершення етапу

1. Усі пункти stage-файлу відмічені, критерій завершення виконано
2. Ретро в кінці stage-файлу: що спрацювало, що ні, що міняємо в плані
3. Оновлено `plan.md` (і changelog) та ADR
4. Створи наступний stage-файл із проміжними кроками
5. Тег:
   ```powershell
   git switch main
   git pull
   git tag -a stage-1-done -m "Stage 1: core API"
   git push origin stage-1-done
   ```

## Якщо щось пішло не так

**Закомітив у `main` замість гілки (ще не запушив):**
```powershell
git switch -c feat/my-work      # нова гілка з твоїми комітами
git switch main
git reset --hard origin/main    # повертає main до стану на GitHub
git switch feat/my-work
```
Перед `reset --hard` переконайся, що коміти вже є в новій гілці (`git log --oneline -3`).

**Забув створити гілку, а зміни ще не закомічені:**
```powershell
git switch -c feat/my-work      # незакомічені зміни переїдуть із тобою
```

**Гілка відстала від `main`:**
```powershell
git fetch origin
git rebase origin/main          # або git merge origin/main, якщо ще не впевнений
```

**Не пам'ятаю, де я:**
```powershell
git status
git branch --show-current
git log --oneline -5
```
і відкрий `docs/STATUS.md`.

## Початок сесії з чатом або агентом

Дай контекст-пакет: `CLAUDE.md`, `docs/STATUS.md`, поточний stage-файл, два останні записи devlog, релевантні ADR.

Шаблон першого повідомлення:

```
Починаю сесію з проектом Lotbook.
Контекст: [вставити STATUS.md і поточний stage-файл].
Сьогодні роблю крок: [назва кроку].
```

Наприкінці сесії попроси: «Склади запис devlog і оновлений STATUS.md».

## Правила, які легко забути

- Ніколи не коміть у `main` напряму
- Один крок = одна гілка = один PR
- Секрети й `.env` не в репозиторій
- Ядро домену пишеш сам, агент пояснює й рев'юїть
- Нова залежність: спершу обговорити, потім додати
