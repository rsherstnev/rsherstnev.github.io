---
title: Начало работы
date: 2019-08-09 20:55:00 +0800
draft: false
description: >-
  Обзор основ Chirpy для быстрого старта.
  Вы узнаете, как установить, настроить и запустить свой первый сайт на Chirpy, а также развернуть его на сервере.
categories:
  - Блогинг
  - Руководство
tags:
  - начало работы
pin: true
---

> **ПРИМЕЧАНИЕ:** Это руководство не полностью перенесено из версии для Jekyll — используйте с осторожностью.
{ .prompt-warning }

## Создание репозитория сайта

При создании репозитория сайта у вас есть два варианта в зависимости от ваших потребностей:

### Вариант 1. Использование стартового шаблона (рекомендуется)

Этот подход упрощает обновления, изолирует ненужные файлы и отлично подходит для тех, кто хочет сосредоточиться на написании с минимальной настройкой.

1. Войдите в GitHub и перейдите к [**стартовому шаблону**][starter].
2. Нажмите кнопку <kbd>Use this template</kbd>, затем выберите <kbd>Create a new repository</kbd>.
3. Назовите новый репозиторий `<username>.github.io`, заменив `username` на ваш GitHub-логин в нижнем регистре.

### Вариант 2. Форк темы

Этот вариант удобен для изменения функций или дизайна, но усложняет обновления. Выбирайте его только если вы знакомы с Jekyll и планируете серьёзно модифицировать тему.

1. Войдите в GitHub.
2. [Сделайте форк репозитория темы](https://github.com/geekifan/jekyll-theme-chirpy/fork).
3. Назовите новый репозиторий `<username>.github.io`, заменив `username` на ваш GitHub-логин в нижнем регистре.

## Настройка окружения

После создания репозитория настройте среду разработки. Есть два основных способа:

### Dev Containers (рекомендуется для Windows)

Dev Containers предоставляют изолированное окружение на базе Docker, что предотвращает конфликты с системой и обеспечивает управление всеми зависимостями внутри контейнера.

**Шаги**:

1. Установите Docker:
   - На Windows/macOS: [Docker Desktop][docker-desktop].
   - На Linux: [Docker Engine][docker-engine].
2. Установите [VS Code][vscode] и расширение [Dev Containers][dev-containers].
3. Клонируйте репозиторий:
   - Для Docker Desktop: запустите VS Code и [клонируйте репозиторий в том контейнера][dc-clone-in-vol].
   - Для Docker Engine: клонируйте локально, затем [откройте в контейнере][dc-open-in-container] через VS Code.
4. Дождитесь завершения настройки Dev Containers.

### Нативная установка (рекомендуется для Unix-подобных ОС)

Для Unix-подобных систем можно настроить окружение нативно для оптимальной производительности.

**Шаги**:

1. Следуйте [руководству по установке Hugo](https://gohugo.io/installation/) и убедитесь, что установлен [Git](https://git-scm.com/).
2. Клонируйте репозиторий на локальный компьютер.
3. Выполните команду `hugo mod get` для установки зависимостей.

## Использование

### Запуск сервера

Для локального запуска сайта используйте команду:

```terminal
hugo serve
```

> Если вы используете Dev Containers, выполняйте команду в терминале **VS Code**.
{ .prompt-info }

Через несколько секунд локальный сервер будет доступен по адресу <http://127.0.0.1:1313>.

### Конфигурация

Обновите переменные в {{< filepath src="config/_default/params.toml">}} по необходимости. Типичные параметры:

- `avatar`
- `author`
- `social`

### Параметры социальных контактов

Параметры социальных контактов отображаются в нижней части боковой панели. Настройте их в {{< filepath src="config/_default/params.toml">}}.

### Настройка стилей

Для изменения стилей скопируйте файл стилей темы в аналогичный путь в вашем сайте Hugo и добавьте свои стили в конец файла.

## Развёртывание

Перед развёртыванием убедитесь, что `baseURL` в {{< filepath src="config/_default/hugo.toml">}} настроен корректно.

### Развёртывание через GitHub Actions

1. Перейдите в репозиторий на GitHub. Откройте вкладку _Settings_, затем _Pages_ в левом меню навигации. В разделе **Source** выберите [**GitHub Actions**][pages-workflow-src] из выпадающего списка.
2. Отправьте коммит в GitHub, чтобы запустить рабочий процесс _Actions_. После успешной сборки сайт будет развёрнут автоматически.

### Ручная сборка и развёртывание

Для самостоятельно размещённых серверов соберите сайт локально:

```console
$ hugo --minify
```

Загрузите сгенерированные файлы из папки `public/` на ваш сервер.

[starter]: https://github.com/geekifan/chirpy-starter
[pages-workflow-src]: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow
[docker-desktop]: https://www.docker.com/products/docker-desktop/
[docker-engine]: https://docs.docker.com/engine/install/
[vscode]: https://code.visualstudio.com/
[dev-containers]: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers
[dc-clone-in-vol]: https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-a-git-repository-or-github-pr-in-an-isolated-container-volume
[dc-open-in-container]: https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-an-existing-folder-in-a-container
