# Сайт приложения (GitHub Pages)

Готовые файлы для публичного сайта British Coins: политика конфиденциальности (нужна Google Play, App Store и AdMob) и `app-ads.txt` (подтверждение издателя AdMob).

| Файл | Что это | Адрес после публикации |
|---|---|---|
| `index.html` | страница приложения: название, описание, ссылки на политику и магазины | `https://<имя>.github.io/` |
| `privacy/index.html` | политика конфиденциальности (английский) | `https://<имя>.github.io/privacy/` |
| `privacy/ru/index.html` | политика конфиденциальности (русский) | `https://<имя>.github.io/privacy/ru/` |
| `app-ads.txt` | строка AdMob `google.com, pub-6639361628452632, DIRECT, f08c47fec0942fa0` | `https://<имя>.github.io/app-ads.txt` |
| `.nojekyll` | пустой: GitHub Pages отдаёт файлы как есть | — |

`<имя>` — имя вашего аккаунта (или организации) на GitHub.

**HTML не править руками.** Страницы политики собираются из `docs/privacy_policy.md` и `docs/privacy_policy_ru.md`: правка текста — в Markdown, затем `python tools/site/build_site.py` (проверка без записи — `--check`; тест `tools/site/tests/test_build_site.py` падает, если `site/` устарел). Ссылки на магазины, адрес почты и строка `app-ads.txt` — константы в начале `tools/site/build_site.py`.

## Опубликовать (один раз)

1. На GitHub: **New repository** → имя ровно **`<имя>.github.io`** → **Public** → Create.
   Важно: именно такой репозиторий (сайт пользователя) открывается в корне домена. В репозитории с другим именем сайт будет по адресу `https://<имя>.github.io/<репозиторий>/`, и AdMob не найдёт `app-ads.txt` — он ищет файл только в корне домена.
2. Скопировать **содержимое** папки `site/` (не саму папку) в корень репозитория — вместе с `.nojekyll`; этот `README.md` копировать не обязательно. Удобнее всего: клонировать репозиторий, скопировать файлы, `git add -A`, `git commit`, `git push`. Через сайт GitHub: **Add file → Upload files**, перетащить файлы и папку `privacy`.
3. Репозиторий → **Settings → Pages** → **Source: Deploy from a branch**, ветка **main**, папка **/ (root)** → **Save**.
4. Через 1–5 минут открыть адреса из таблицы: страница, обе политики и `app-ads.txt` (одна строка текста).

## Куда вписать адреса

| Где | Поле | Значение |
|---|---|---|
| Приложение | `lib/flavors/uk/config.dart` → `privacyPolicyUrl` (попросить агента; после этого в Настройках появится пункт «Политика конфиденциальности») | `https://<имя>.github.io/privacy/` |
| Google Play Console | **App content → Privacy policy** | `https://<имя>.github.io/privacy/` |
| Google Play Console | **Store presence → Store settings → Store listing contact details → Website** (по нему AdMob ищет `app-ads.txt`) | `https://<имя>.github.io` |
| App Store Connect | **App Privacy → Privacy Policy URL** | `https://<имя>.github.io/privacy/` |
| App Store Connect | **App Information → Marketing URL** (по нему AdMob ищет `app-ads.txt` для iOS) | `https://<имя>.github.io` |
| AdMob | **Apps → app-ads.txt**: через сутки после публикации приложения и сайта — «Check for updates» | — |

AdMob проверяет `app-ads.txt` до 24 часов; статус «not found», пока приложение не опубликовано в магазине (нет сайта разработчика в карточке) — это нормально.

## Обновить политику

1. Изменить `docs/privacy_policy.md` и `docs/privacy_policy_ru.md` (и дату вступления в силу в обоих).
2. `python tools/site/build_site.py`.
3. Скопировать изменённые файлы `site/privacy/...` в репозиторий сайта, `git push`. Адреса не меняются.
