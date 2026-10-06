# Личный сайт

Сайт-визитка. Четыре страницы (главная, проекты, опыт работы, контакты) и общий блок с дополнительной информацией внизу. Статика на HTML и CSS без фреймворков и сборки.

## Запуск локально

Быстрый вариант без Docker.

```bash
cd public
python3 -m http.server 8000
```

Сайт откроется на http://localhost:8000.

Вариант в контейнере, так же, как он работает на сервере.

```bash
docker build -t site .
docker run -d --name site -p 8080:80 site
```

Сайт откроется на http://localhost:8080, проверка живости на http://localhost:8080/healthz. Остановить контейнер можно командой `docker rm -f site`.

## Публикация

При пуше в `main` workflow `.github/workflows/pages.yml` собирает образ, проверяет, что сайт отдаётся, и выкладывает папку `public` на GitHub Pages. Перед первым деплоем в настройках репозитория нужно выбрать Settings → Pages → Source → GitHub Actions.

## Структура

```
public/          содержимое сайта
  index.html
  projects.html
  experience.html
  contacts.html
  css/style.css
  img/
nginx.conf       конфиг nginx для контейнера
Dockerfile       образ на nginx:alpine с healthcheck
.github/         деплой на GitHub Pages
```
