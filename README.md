# Классик AI

Материалы к конкурсу по алгоритмическому стихосложению [Классик AI](https://classic.sberbank.ai).

- [Постановка задачи](#Постановка-задачи)
- [Оценка качества](#Оценка-качества)
- [Данные](#Данные)
- [Формат решений](#Формат-решений)
- [Примеры решений](#Примеры-решений)

## Постановка задачи

Необходимо построить алгоритм, который сочиняет стих на заданную тему в стиле классических русских поэтов. Тема задается коротким предложением, либо несколькими характеризующими фразами. 

Рассмотрим, например, оригинальное стихотворение, известное каждому образованному соотечественнику.

**Автор**: М. Ю. Лермонтов

**Тема**: Дядя рассказывает о Бородинской битве, в которой он принимал участие, и сетует на нынешнее поколение.

**Стихотворение**: 

> Скажи-ка, дядя, ведь не даром <br>
> Москва, спаленная пожаром, <br>
> Французу отдана? <br>
> Ведь были ж схватки боевые, <br>
> Да, говорят, еще какие! <br> 
> Недаром помнит вся Россия <br>
> Про день Бородина!

Как стихотворение могло бы выглядеть, если бы Лермонтов писал про "чемпионат мира по футболу", "повсеместное распространение интернета", "избавление от тяжелой работы благодаря искусственному интеллекту" и сотни других тем, которые только могут прийти в голову? 

Участникам предлагается построить алгоритм, который будет генерировать короткие стихотворные произведения на произвольную тему, которая подается на вход алгоритму, в стиле 5 русских классиков (в скобках указаны идентификаторы поэтов):

1. [**Пушкин**, Александр Сергеевич](https://ru.wikipedia.org/wiki/Пушкин,_Александр_Сергеевич) (`pushkin`)
2. [**Есенин**, Сергей Александрович](https://ru.wikipedia.org/wiki/Есенин,_Сергей_Александрович) (`esenin`)
3. [**Маяковский**, Владимир Владимирович](https://ru.wikipedia.org/wiki/Маяковский,_Владимир_Владимирович) (`mayakovskij`)
4. [**Блок**, Александр Александрович](https://ru.wikipedia.org/wiki/Блок,_Александр_Александрович) (`blok`)
5. [**Тютчев**, Фёдор Иванович](https://ru.wikipedia.org/wiki/Тютчев,_Фёдор_Иванович) (`tyutchev`)

Тема — предложение или набор ключевых фраз, которые являются отправной точкой для сочинения. Тема представлена коротким текстом, не более чем из 1000 символов. Круг тем ограничен содержанием русской Википедии. Проще всего пояснить на примерах:

- Шторм топит маленький кораблик
- Музыка тихо играет вдалеке
- Аромат спелых яблок наполнил сад
- Я люблю Россию
- Я поздравляю друга с днем рождения
- Физики нашли бозон Хиггса в данных остановленного коллайдера Теватрон
- Компании, которые не используют искусственный интеллект, в скором времени просто-напросто перестанут существовать на рынке

Разумеется, соответствие сгенерированного стихотворения стилю поэта и заданной теме — субъективно.

Алгоритм можно реализовывать на любом языке программирования, главное чтобы он имел необходимый интерфейс и производил генерацию достаточно быстро на компьютере, сравнимом по мощности со средним современным ПК. Об интерфейсе и ограничениях смотрите [формат решений](#Формат-решений).


## Оценка качества

Чтобы иметь возможность отслеживать прогресс своих решений, а также сравнивать их с другими решениями участников, на протяжении соревнования будет проходить разметка решений через чат-бот. В роли разметчиков могут выступать любые желающие. Результаты работы алгоритмов генерации стихотворений будут оцениваться по двум критериям:

1. **Качество** стихосложения и соответствие стилю заданного классического поэта
2. **Полнота** раскрытия заданной темы в стихотворении

По каждому критерию будет предоставлена 5-балльная шкала. Алгоритм должен будет сочинить стихи на каждую тему из тестового набора. 

Темы, на которых будут тестироваться алгоритмы, будут составлены экспертами. Часть тем будет открыта и общедоступна, но для выявления лучшего алгоритма будет использован скрытый набор тем. Можно считать, что множества публичных и скрытых тем — однородны, получены случайным разбиением из одного набора.

Полученное в результате работы алгоритма стихотворение может быть **отклонено** разметчиками по следующим причинам:
- сгенерированный текст не является стихотворением на русском языке
- сгенерированный текст содержит нецензурную лексику
- сгенерированный текст содержит умышленно включенные оскорбительные фразы или подтекст

В случае отклонения стихотворения алгоритм получает минимальные оценки по обоим шкалам.

Участникам будет доступно API, через которое можно получить детальный отчет о проверке и разметке всех стихотворений.

## Данные

Участникам предоставляется собрание сочинений выбранных классических авторов. В файле [`data/classic_poems.json`](data/classic_poems.json) в формате JSON представлен список стихотворений с указанием идентификаторов авторов:

```json
[
    {
        "poet_id": "pushkin",
        "title": "Памятник",
        "content": "Я памятник себе воздвиг нерукотворный,\nК нему не зарастет народная тропа,..."
    },
    {
        "poet_id": "blok",
        "title": "* * *",
        "content": "Ночь, улица, фонарь, аптека,\nБессмысленный и тусклый свет..."
    },
    ...
]
```

В конкурсе допускается свободное использование любых других общедоступных материалов. 

Что может пригодиться:
- [Дамп Википедии на русском языке](https://dumps.wikimedia.org/ruwiki/latest/)
- [Национальный корпус русского языка](http://www.ruscorpora.ru)
- Набор вопросов-ответов к параграфам SberQuAD из [конкурса SDSJ-2017](https://github.com/sberbank-ai/data-science-journey-2017/tree/master/problem_B): [`sdsj2017_sberquad.csv`](https://bucketeer-db1966c9-c9f8-427d-ae61-659a91a9fca7.s3.amazonaws.com/public/sdsj2017_sberquad.csv)

## Формат решений

В проверяющую систему необходимо отправить код алгоритма, запакованный в ZIP-архив. Решения запускаются в изолированном окружении при помощи [Docker](https://www.docker.com/what-docker), время и ресурсы для тестирования ограничены. В простом случае, участнику нет необходимости разбираться с технологией Docker.

Пример архива с решением:
- [`base-python.zip`](https://bucketeer-db1966c9-c9f8-427d-ae61-659a91a9fca7.s3.amazonaws.com/public/classic-base-python.zip)
- [`phonetic-templates.zip`](https://bucketeer-db1966c9-c9f8-427d-ae61-659a91a9fca7.s3.amazonaws.com/public/classic-phonetic-templates.zip)

### Содержимое контейнера

В корне архива обязательно должен быть файл `metadata.json` следующего содержания:

```json
{
    "image": "sberbank/python",
    "entry_point": "python generator.py"
}
```

Здесь `image` — поле с названием docker-образа, в котором будет запускаться решение, `entry_point` — команда, при помощи которой запускается решение. Для решения текущей директорией будет являться корень архива.

Для запуска решений можно использовать существующие окружения:

- `sberbank/python` — Python3 с установленным большим набором библиотек ([подробнее](images/sberbank-python))
- `gcc` - для запуска компилируемых C/C++ решений (подробнее здесь)
- `node` — для запуска JavaScript
- `openjdk` — для Java
- `mono` — для C#

Подойдет любой другой образ, доступный для загрузки из [DockerHub](http://dockerhub.com). При необходимости, Вы можете подготовить свой образ, добавить в него необходимое ПО и библиотеки (см. [инструкцию по созданию Docker-образов](https://docs.docker.com/engine/reference/builder/)); для использования его необходимо будет опубликовать на DockerHub.


### Программный интерфейс

Решение должно быть выполнено в виде HTTP-сервера, доступного по порту `8000`, который отвечает на два вида запросов:

#### `GET /ready`

На запрос необходимо ответить кодом `200 OK` в случае, если решение готово к работе. Любой другой код означает, что решение еще не готово. У алгоритма есть ограниченное время на подготовку к работе, за которое можно прочитать данные с диска, создать в оперативной памяти необходимые структуры данных.

#### `POST /generate/<poet_id>`

Запрос на генерацию стихотворения. Идентификатор поэта, в стиле которого необходимо сочинить, указан в URL. Содержимое запроса — JSON с единственным полем `seed`, содержащим тему сочинения:

```json
{"seed": "регрессия глубокими нейронными сетями"}
```

В качестве ответа необходимо в отведенное время дать JSON со сгенерированным сочинением в поле `poem`:

```json
{"poem": "Ведь были сети боевые\nДа говорят еще какие\n..."}
```

Запрос и ответ должны иметь `Content-Type: application/json`. Рекомендуется использовать кодировку UTF-8.


### Ограничения

Контейнер с решением запускается в следующих условиях:

- решению доступны ресурсы
  - 8 Гб оперативной памяти
  - 4 vCPU
  - GPU Nvidia K80
- решение изолировано от интернета
- время на подготовку к работе: 120 секунд (после чего на запрос `/ready` необходимо отвечать кодом 200)
- время на один запрос `/generate/`: 5 секунд
- при тестировании запросы производятся последовательно (не более 1 запроса одновременно)
- максимальный размер упакованного и распакованного архива с решением: 2 Гб

Сгенерированное стихотворение (`poem`) должно удовлетворять формату:

  - размер стиха — **от 3 до 8 строк**
  - каждая строка содержит **не более 120 символов**
  - строки разделяются символом `\n`
  - пустые строки игнорируются

Тема сочинения (`seed`) по длине не превышает 1000 символов.

При тестировании используются стили только 5 перечисленных выше избранных поэтов.

### Пример работы

При помощи Python 3 и библиотеки [`requests`](http://docs.python-requests.org/en/master/).

```python
>>> import requests
>>> requests.get('http://localhost:8000/ready')
<Response [200]>
>>> resp = requests.post('http://localhost:8000/generate/lermontov', json={'seed': 'регрессия глубокими нейронными сетями'})
>>> resp
<Response [200]>
>>> data = resp.json()
>>> print(data['poem'])
Ведь были сети боевые
Да говорят еще какие
Не даром помнит регрессия
Про то какая глубина
```


## Примеры решений

В каталоге [`examples`](examples) можно найти примеры решений, готовые к отправке в систему.

- [`base-python`](examples/base-python): шаблон для Python
- [`examples/phonetic-templates`](examples/phonetic-templates): генератор на основе фонетических шаблонов

## Запуск примера 

### На основе фонетического шаблона

Для запуска примера должен быть установлен и настроен docker. 

```bash
docker-compose up phonetic
```

