---
title: Написание нового поста
date: 2019-08-08 14:10:00 +0800
categories:
  - Блогинг
  - Руководство
tags:
  - написание
---

Это руководство покажет, как писать посты в шаблоне _Chirpy_. Его стоит прочитать, даже если вы уже работали с Hugo, — многие функции требуют указания конкретных переменных.

## Имя файла и путь

Создайте новый файл командой `hugo new content/post/YYYY-MM-DD-TITLE.md`. Путь можно изменить, но все посты должны находиться в {{< filepath src="content/post" >}} корневого каталога.

## Front Matter

В начале поста необходимо заполнить [Front Matter](https://gohugo.io/content-management/front-matter/):

```yaml
---
title: ЗАГОЛОВОК
date: YYYY-MM-DD HH:MM:SS +/-TTTT
draft: true
---
```

Дополнительные поля по необходимости:
```yaml
categories: [КАТЕГОРИЯ, ПОДКАТЕГОРИЯ] # поддерживается не более двух категорий
tags: [ТЕГ]      # имена тегов всегда в нижнем регистре
pin: true         # пост будет закреплён вверху главной страницы
description: Привет, мир! # описание поста
```

> _layout_ поста по умолчанию установлен в `post`, поэтому добавлять переменную _layout_ в Front Matter не нужно.
{ .prompt-tip }

### Категории и теги

Поле `categories` может содержать не более двух элементов, а `tags` — от нуля до любого количества. Например:

```yaml
---
categories: [Животные, Насекомые]
tags: [пчела]
---
```

### Информация об авторе

Информацию об авторе обычно не нужно указывать в _Front Matter_ — она берётся из переменных `social.name` и первой записи `social.links` в файле конфигурации. Но её можно переопределить.

Добавьте данные автора в `data/authors/<language>.yaml`:

```yaml { file="data/authors/ru-RU.yaml" }
<author_id>:
  name: <полное имя>
  url: <домашняя_страница_автора>
```

Затем используйте `author` для одного или `authors` для нескольких:

```yaml
---
author: <author_id>                     # один автор
# или
authors: [<author1_id>, <author2_id>]   # несколько авторов
---
```

Чтобы не указывать автора в каждом посте, задайте глобального автора в {{< filepath src="config/_default/params.toml" >}}:

```yaml { file="config/_default/params.toml" }
author: <author_id>
```

> Автор, указанный в Front Matter конкретного поста, переопределяет глобальную настройку.
{ .prompt-info }

### Описание поста

По умолчанию первые слова поста используются для отображения на главной странице, в разделе «Похожие посты» и в XML RSS-ленты. Если вы хотите задать своё описание, используйте поле `description` в _Front Matter_:

```yaml
---
description: Краткое описание поста.
---
```

Текст `description` также отображается под заголовком на странице поста.

## Содержание (TOC)

По умолчанию **Содержание** (Table of Contents) отображается на правой панели поста. Чтобы отключить его глобально, перейдите в {{< filepath src="config/_default/params.toml" >}} и установите `toc = false`. Чтобы отключить TOC для конкретного поста:

```yaml
---
toc: false
---
```

## Комментарии

Глобальная настройка комментариев задаётся параметром `comments.provider` в {{< filepath src="config/_default/params.toml" >}}. После выбора системы комментарии будут включены для всех постов.

Чтобы отключить комментарии для конкретного поста:

```yaml
---
comments: false
---
```

## Медиа

Под медиа-ресурсами в _Chirpy_ понимаются изображения, аудио и видео.

### URL-префикс

> URL-префикс находится в разработке.
{ .prompt-warning }

Чтобы не дублировать URL-префиксы, задайте два параметра:

- Для CDN укажите `cdn` в {{< filepath src="config/_default/params.toml" >}}:

  ```yaml  { file="config/_default/params.toml" }
  cdn: https://cdn.com
  ```

- Для текущего поста/страницы задайте `media_subpath` в _front matter_:

  ```yaml
  ---
  media_subpath: /path/to/media/
  ---
  ```

Параметры `site.cdn` и `page.media_subpath` можно использовать по отдельности или совместно: `[site.cdn/][page.media_subpath/]file.ext`

### Изображения

#### Подпись

Добавьте атрибут `caption` после строки с изображением:

```markdown
![описание изображения](/path/to/image)
{ caption="Ваша подпись к изображению" }
```

#### Размер

Чтобы избежать сдвига макета при загрузке, указывайте ширину и высоту:

```markdown
![Desktop View](/assets/img/sample/mockup.png)
{ width="700" height="400" }
```

> Для SVG необходимо как минимум указать _ширину_, иначе изображение не отобразится.
{ .prompt-info }

#### Позиция

По умолчанию изображение центрируется. Можно использовать классы `normal`, `left`, `right`:

> После указания позиции подпись добавлять не следует.
{ .prompt-warning }

- **Обычная позиция** (выравнивание влево):

  ```markdown
  ![Desktop View](/assets/img/sample/mockup.png)
  { .normal }
  ```

- **Обтекание слева**:

  ```markdown
  ![Desktop View](/assets/img/sample/mockup.png)
  { .left }
  ```

- **Обтекание справа**:

  ```markdown
  ![Desktop View](/assets/img/sample/mockup.png)
  { .right }
  ```

#### Тёмный/светлый режим

Подготовьте два изображения и назначьте им класс `dark` или `light`:

```markdown
![Только светлый режим](/path/to/light-mode.png)
{ .light }
![Только тёмный режим](/path/to/dark-mode.png)
{ .dark }
```

#### Тень

```markdown
![Desktop View](/assets/img/sample/mockup.png)
{ .shadow }
```

#### Превью-изображение

Для изображения в шапке поста используйте разрешение `1200 x 630` (соотношение `1.91:1`):

```yaml
---
image:
  path: /path/to/image
  alt: альтернативный текст изображения
---
```

### Видео

#### Платформы

```hugo
{{</* embed/{Platform}.html id="{ID}" */>}}
```

| URL видео                                                                                          | Платформа  | ID             |
| -------------------------------------------------------------------------------------------------- | ---------- | :------------- |
| [https://www.**youtube**.com/watch?v=**H-B46URT4mg**](https://www.youtube.com/watch?v=H-B46URT4mg) | `youtube`  | `H-B46URT4mg`  |
| [https://www.**twitch**.tv/videos/**1634779211**](https://www.twitch.tv/videos/1634779211)         | `twitch`   | `1634779211`   |
| [https://www.**bilibili**.com/video/**BV1Q44y1B7Wf**](https://www.bilibili.com/video/BV1Q44y1B7Wf) | `bilibili` | `BV1Q44y1B7Wf` |

#### Видеофайлы

```hugo
{{</* embed/video.html src="{URL}" */>}}
```

Дополнительные атрибуты:

- `poster='/path/to/poster.png'` — постер во время загрузки
- `title='Текст'` — заголовок видео
- `autoplay=true` — автозапуск
- `loop=true` — зацикленное воспроизведение
- `muted=true` — без звука
- `types` — дополнительные форматы через `|`

### Аудио

```liquid
{{</*  embed/audio.html src="{URL}" */>}}
```

## Закреплённые посты

Чтобы закрепить один или несколько постов вверху главной страницы:

```yaml
---
pin: true
---
```

## Подсказки

Типы подсказок: `tip`, `info`, `warning`, `danger`. Добавляются классом `prompt-{type}` к цитате:

```md
> Текст подсказки.
{ .prompt-info }
```

## Синтаксис

### Встроенный код

```md
`часть встроенного кода`
```

### Выделение пути к файлу

```hugo
{{</* /path/to/a/file.extend */>}}
```

### Блок кода

````md
```
Это блок кода в виде обычного текста.
```
````

#### Язык

````markdown
```yaml
key: value
```
````

#### Имя файла

````markdown
```shell { file="path/to/file" }
# содержимое
```
````

## Математика

Используется [**MathJax**][mathjax]. По умолчанию не загружается — включите в Front Matter:

[mathjax]: https://www.mathjax.org/

```yaml
---
math: true
---
```

После включения:

- **Блочная математика**: `$$ math $$` с обязательными пустыми строками до и после `$$`
  - **Нумерация**: `$$\begin{equation} math \end{equation}$$`
  - **Ссылка на уравнение**: `\label{eq:label_name}` в блоке и `\eqref{eq:label_name}` в тексте
- **Строчная математика** (в строке): `$$ math $$` без пустых строк
- **Строчная математика** (в списке): `\$$ math $$`

## Mermaid

> Поддержка Mermaid находится в разработке.
{ .prompt-warning }

[**Mermaid**](https://github.com/mermaid-js/mermaid) — отличный инструмент для генерации диаграмм. Включите в Front Matter:

```yaml
---
mermaid: true
---
```

Затем оберните код диаграммы в ```` ```mermaid ```` и ```` ``` ````.

## Дополнительно

За дополнительной информацией обратитесь к [документации Hugo](https://gohugo.io/documentation/).
