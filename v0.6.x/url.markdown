# URL

    Стабильность: 3 - Стабильно


В это модуле собраны инструменты для разрешения и разбора URL.
Вызовите `require('url')` чтобы его использовать.

Объекты разобранного URL имеют либо все либо некоторые из перечисленных полей,
в зависимости от их присутствия в строке URL. Части которых не было в URL
не будут присутствовать в объекте. Примеры показаны для URL

`'http://user:pass@host.com:8080/p/a/t/h?query=string#hash'`

* `href`: Полный URL который был разобран. Поля `protocol` и `host` должны состоять из строчных букв.
  
  Пример: `'http://user:pass@host.com:8080/p/a/t/h?query=string#hash'`
* `protocol`: Протокол запроса, состоит из строчных букв.
  
  Пример: `'http:'`
* `host`: Полный host, включая порт и информацию аутентификации, состоит из строчных букв.
  
  Пример: `'user:pass@host.com:8080'`
* `auth`: Информация для аутентификации.
  
  Пример: `'user:pass'`
* `hostname`: Имя хоста, состоит из строчных букв.

  Пример: `'host.com'`
* `port`: Номер порта.

  Пример: `'8080'`
* `pathname`: Секция пути, которая идёт после хоста и перед строкой параметров, включая начальный слеш если он есть.

  Пример: `'/p/a/t/h'`
* `search`: Строка запроса, включая ведущий знак вопроса.

  Пример: `'?query=string'`
* `path`: Состоит из `pathname` и `search`.

  Пример: `'/p/a/t/h?query=string'`
* `query`: Параметры из строки запроса, либо уже разобранный объект с параметрами.

  Пример: `'query=string'` or `{'query':'string'}`
* `hash`: "Якорь" URL, включая знак решётки.

  Пример: `'#hash'`

Модуль URL предоставляет следующие методы:

## url.parse(urlStr, [parseQueryString], [slashesDenoteHost])

Получает строку URL и возвращает объект.

Передайте `true` вторым аргументом, чтобы одновременно
разобрать строку запроса модулем `querystring`. По умолчанию `false`.

Передайте `true` третьим аргументом, чтоы строка `//foo/bar` разрешалась как
`{ host: 'foo', pathname: '/bar' }` вместо `{ pathname: '//foo/bar' }`.
По умолчанию `false`.


## url.format(urlObj)

Получает объект URL и возвращает отформатированный URL в виде строки.

* `href` игнорируется.
* `protocol` можно задавать как с символом `:` (двоеточие) в конце, так и без.
  * Протоколы `http`, `https`, `ftp`, `gopher`, `file` используются с суффиксом `://` (двоеточие-слеш-слеш).
  * Все остальные протоколы `mailto`, `xmpp`, `aim`, `sftp`, `foo` и т.д. используются с суффиксом `:` (двоеточие)
* `auth` используется только если не задан `host`.
* `hostname` используется только если не задан `host`.
* `port` используется только если не задан `host`.
* `host` используется вместо `auth`, `hostname` и `port`
* `pathname` можно задавать как с символом `/` (слеш) в начале, так и без.
* `search` будет использоваться вместо `query`
* `query` (объект, см. `querystring`) будет использоваться если отсутствует `search`.
* `search` можно задавать как с символом `?` (вопросительный знак) в начале, так и без.
* `hash` можно задавать как с символом `#` (символ диеза, решётки) в начале, так и без.

## url.resolve(from, to)

Получает базовый URL и относительный URL, и разрешает их как это сделал бы браузер для гиперссылки.
