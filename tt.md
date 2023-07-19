* [Помилки](#Помилки)
* [USERS](#USERS)
  * [Signup](#Signup)
  * [Signup](#Signin)
  * [Signout](#Signout)
* [ADVERTS](#ADVERTS)
  * [Create](#Create)
  * [Page](#Page)
  * [Advert](#Advert)
  * [SetFavorite](#SetFavorite)
* [Структури](#Структури)


<details open>
  <summary>
          
  # Помилки
          
  </summary>

### Тіло відповіді

```json
HTTP 400
{
    "errorCode": "код_помилки_зміїним_стилем",
    "errorMessage": "Юзер-френдлі опис помилки"
}
```

Усі помилки валідації даних повинні повертати код `400`

Спроби використання запитів, що не відповідають типу користувача (наприклад запис на урок вчителем) повинні повертати код `403`

Запити типу `GET` з валідним, але неіснуючим `id` повинні повертати код `404`

Помилки:

* `invalid_operation`
* `invalid_value`
* `invalid_shedule_day`
* `invalid_shedule_time_value`
* `invalid_tag`
* `invalid_id`
* `description_too_long`
* `user_already_exists`
* `invalid_credentials`
* `no_adverts_found`
* `not_found`

</details>

<details open>
<summary>

# USERS

</summary>

## Signup

Створення нового користувача.

### Параметри

* `name` (string) : Ім'я користувача. Складається з ненульової кількості літер, що можуть бути розділені пробілами.
* `email` (string) : Електронна пошта користувача. На одну пошту може бути зареєстрований тільки один користувач.
* `password` (string) : Пароль користувача. Складається з 8-24 довільних символів.

### Тіло запиту

```json
POST /users/signup
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "password": "123qwerty"
}
```

### Відповідь

```json
HTTP 200
{
    //TODO
}
```

### Помилки

* `user_already_exists`: пошта вже прив'язана до іншого користувача.
* `invalid_value:` д.п. відсутній символ '@' у пошті.

## Signin

Вхід користувача до системи.

### Параметри

* `email` (string) : Електронна пошта користувача.
* `password` (string) : Пароль користувача.

### Тіло запиту

```json
POST /users/signin
{
    "email": "john.smith@gmail.com",
    "password": "123qwerty"
}
```

#### Відповідь

```json
HTTP 200
{
    //TODO
}
```

### Помилки

* `invalid_credentials`: невірний пароль або відсутній користувач з `email` поштою.
* `invalid_value`: д.п. відсутній символ '@' у пошті.

## Signout

Вихід користувача з системи.

### Тіло запиту

```json
POST /users/signout
```

### Відповідь

```json
HTTP 200
{
    //TODO
}
```

### Помилки

Відсутні

</details>

<details open>
<summary>

  # ADVERTS
 
</summary>

## Create

Створення вчителем оголошення.

### Параметри

* `price` (float): Ціна уроку довжиною 1 годину в у.о.. Повинна бути більшою за 0.
* [avalLength](#link_avalLength) (array): Перелік можливих довжин уроку.
* [avalShedule](#link_avalshedule) (array): Перелік днів та інтервалів годин, у які може бути проведений урок.
* [tagsSpecialization](#link_tagsspecialization) (array): Перелік тегів, що визначають спеціалізацію вчителя.
* [tagsHobby](#link_tagsHobby) (array): Перелік тегів, що визначають хобі вчителя.
* [tagsSpokenLang](#link_tagsspokenLang) (array): Перелік тегів, що визначають мови, якими вчитель розмовляє.
* [tagsTeachingLang](#link_tagsteachingLang) (array): Перелік тегів, що визначають мови, які вчитель викладає.
* [tagsNativeLang](#link_tagsnativeLang) (array): Перелік тегів, що визначають рідні мови вчителя.
* `shortDescription` (string): Короткий опис оголошення (200 символів).
* `fullDescription` (string): Повний опис оголошення (1000 символів).

### Тіло запиту

```json
POST /adverts/create
{
    "price": 299.99,
    "avalLength": [ 30, 60, 120 ],
    "avalShedule": [ "monday" : [[13, 15.5], [18, 18.5]], "thursday" : [[8, 12]] ]
    "tagsSpecialization": [ "improvement", "basics" ],
    "tagsHobby": [ "fishing", "gardening", "board games" ],
    "tagsSpokenLang": [ "ukrainian", "english", "german" ],
    "tagsTeachingLang": [ "english", "german" ],
    "tagsNativeLang": [ "ukrainian" ],
    "shortDescription": "This is a short desctiption",
    "fullDescription": "This is a full desctiption"
}
```

### Відповідь
Ідентифікатор створеного оголошення.

* `id` (int): ідентифікатор створеного оголошення.

```json
HTTP 200
{
    "id": 541
}
```

### Помилки

* `invalid_operation`: користувач вже має оголошення.
* `invalid_value`: д.п. пустий перелік довжин уроку.
* `invalid_tag`: використання невалідного тегу, д.п. `"cheese"` у `tagsTeachingLang`.
* `description_too_long`: довжина опису перевищує максимальну.

## Page

Генерація сторінки оголошень

### Параметри

* `pageNum` (int): Номер сторінки. Нумераця починається з `1`.

### Тіло запиту

```json
GET /adverts/page
{
    "pageNum": 2
}
```

### Відповідь
Масив об'єктів `adverts`, що коротко описує `advertCount` оголошень.

* `advertCount` (int): кількість елементів масиву `adverts`, що описують оголошення.
* `advertId` (int): ідентифікатор оголошення.
* `teacherName` (string): ім'я вчителя.
* [tagsHobby](#link_tagsHobby) (array): Перелік тегів, що визначають хобі вчителя.
* [tagsSpokenLang](#link_tagsspokenLang) (array): Перелік тегів, що визначають мови, якими вчитель розмовляє.
* [tagsTeachingLang](#link_tagsteachingLang) (array): Перелік тегів, що визначають мови, які вчитель викладає.
* [tagsNativeLang](#link_tagsnativeLang) (array): Перелік тегів, що визначають рідні мови вчителя.
* `shortDescription` (string): Короткий опис оголошення.
* `rating` (float): рейтинг вчителя за 5-ти бальною шкалою.
* `profilePicture` (string): назва файлу профільного зображення. Зображення розміщене за шляхом //TODO
* `country` (string): код країни вчителя згідно [ISO 3166-1 alpha-3](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3).
* `certified` (bool): флажок, що вказує чи вчитель є офіційно сертифікованим.
* `isFavorite` (bool): флажок, що вказує чи оголошення є доданим до вподобаних.

```json
HTTP 200
{
    "advertCount": 10,
    "adverts":
    [
        {
            "advertId": 541,
            "teacherName": "John Smith",
            "tagsHobby": [ "fishing", "gardening", "board games" ],
            "tagsSpokenLang": [ "ukrainian", "english", "german" ],
            "tagsTeachingLang": [ "english", "german" ],
            "tagsNativeLang": [ "ukrainian" ],
            "shortDescription": "This is a short desctiption",
            "rating": 4.7,
            "profilePicture": "541.png",
            "country": "UKR.png",
            "certified": true,
            "isFavorite": false
        },..
    ]
}
```

### Помилки

* `invalid_value`: Номер сторінки менший `1`.
* `no_adverts_found`: Недостатньо оголошень для генерації сторінки. Д.п. спроба генерації сторінки `2` при розмірі сторінок `10` і загальній кількості оголошень `8`.

## Advert

Повний опис оголошення

### Параметри

* `advertId` (int): ідентифікатор оголошення.

### Тіло запиту

```json
GET /adverts/advert
{
    "advertId": 541
}
```

### Відповідь
Повний опис оголошення.

* `advertId` (int): ідентифікатор оголошення.
* `teacherName` (string): ім'я вчителя.
* `price` (float): Ціна уроку довжиною 1 годину в у.о..
* [avalLength](#link_avalLength) (array): Перелік можливих довжин уроку.
* [avalShedule](#link_avalshedule) (array): Перелік днів та інтервалів годин, у які може бути проведений урок.
* [tagsSpecialization](#link_tagsspecialization) (array): Перелік тегів, що визначають спеціалізацію вчителя.
* [tagsHobby](#link_tagsHobby) (array): Перелік тегів, що визначають хобі вчителя.
* [tagsSpokenLang](#link_tagsspokenLang) (array): Перелік тегів, що визначають мови, якими вчитель розмовляє.
* [tagsTeachingLang](#link_tagsteachingLang) (array): Перелік тегів, що визначають мови, які вчитель викладає.
* [tagsNativeLang](#link_tagsnativeLang) (array): Перелік тегів, що визначають рідні мови вчителя.
* `shortDescription` (string): Короткий опис оголошення.
* `fullDescription` (string): Повний опис оголошення.
* `rating` (float): рейтинг вчителя за 5-ти бальною шкалою.
* `profilePicture` (string): назва файлу профільного зображення. Зображення розміщене за шляхом //TODO
* `country` (string): код країни вчителя згідно [ISO 3166-1 alpha-3](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3).
* `certified` (bool): флажок, що вказує чи є вчитель офіційно сертифікований.
* `isFavorite` (bool): флажок, що вказує чи оголошення є доданим до вподобаних.
* `givenLessonsCount` (int): кількість проведених вчителем уроків.
* [tagsCallApps](#link_tagsCallApps) (array): Перелік тегів, що визначають які платформи можуть бути використані для проведення уроку. 

```json
HTTP 200
{
    "advertId": 541,
    "price": 299.99,
    "avalLength": [ 30, 60, 120 ],
    "avalShedule": [ "monday" : [[13, 15.5], [18, 18.5]], "thursday" : [[8, 12]] ]
    "tagsSpecialization": [ "improvement", "basics" ],
    "tagsHobby": [ "fishing", "gardening", "board games" ],
    "tagsSpokenLang": [ "ukrainian", "english", "german" ],
    "tagsTeachingLang": [ "english", "german" ],
    "tagsNativeLang": [ "ukrainian" ],
    "shortDescription": "This is a short desctiption",
    "fullDescription": "This is a full desctiption",
    "rating": 4.7,
    "profilePicture": "541.png",
    "country": "UKR.png",
    "certified": true,
    "isFavorite": false
    "givenLessonsCount": 72,
    "tagsCallApps": ["zoom", "skype"]
}
```

### Помилки

* `invalid_id`: Невалідний `id`
* `not_found`: Оголошення з ідентифікатором `id` не існує.

## SetFavorite

Додавання або вилучення оголошення з вподобаних.

### Параметри

* `advertId`: ідентифікатор оголошення,
* `favorite`: у який стан перевести флажок, що вказує чи оголошення є доданим до вподобаних. 

### Тіло запиту

```json
POST /adverts/setFavorite
{
    "advertId": 451,
    "favorite": true
}
```

### Відповідь
Cтан флажка, що вказує чи оголошення є доданим до вподобаних. 

* `favorite`: флажок, що вказує чи оголошення є доданим до вподобаних.

```json
HTTP 200
{
    "favorite": true
}
```

### Помилки

* `invalid_id`: Невалідний `id`
* `not_found`: Оголошення з ідентифікатором `id` не існує.
* `invalid_value`: Невалідне значення `favorite`.

</details>

<details open>
<summary>

# Структури

</summary>

<a name="link_avalLength"></a>
## avalLength
Перелік можливих довжин уроку. Складається з масиву цілих чисел `int`, що вказують на довжину урока в хвилинах.
`int` повинен бути рівним одному з наступних чисел: `30, 60, 90, 120`.\
Масив не може бути пустим.

```
"avalLength": [ int,.. ]
```

<a name="link_avalShedule"></a>
## avalShedule
Перелік днів та інтервалів годин, у які може бути проведений урок. Складається з іменованого масиву типу `day: [intervals]`,
де `day` є назвою дня англійською у нижньому регістрі, `[intervals]` є двовимірним масивом розміром `[n, 2]`, і позначає інтервали,
у які може бути проведений урок. Значення інтервалу повинні належати `[0, 24]` та можуть мати дробову частину `.5` для позначення 30 хвилин.\
Масив не може бути пустим.

```
"avalShedule": [ string: [ [float, float],.. ],.. ]
```

<a name="link_tagsSpecialization"></a>
## tagsSpecialization
Перелік тегів, що визначають спеціалізацію вчителя. Складається з масиву рядків що можуть набувати наступних значень.

```
"for business", "basics", "for_children", "improvement" //на міті домовимось які ще
```

Масив не може бути пустим.

```
"tagsSpecialization": [ string,.. ]
```

<a name="link_tagsHobby"></a>
## tagsHobby
Перелік тегів, що визначають хобі вчителя. Складається з масиву рядків що можуть набувати наступних значень.

```
"reading", "martial_arts", "woodworking", "gardening", "video_games", "fishing yoga", "traveling", "golf", "watching_sports", "board games", "writing", "running", "tennis", "volunteer work", "dancing", "painting", "cooking", "cycling", "movie watching", "podcasts", "television", "music"
```

Масив не може бути пустим.

```
"tagsHobby": [ string,.. ]
```

<a name="link_tagsSpokenLang"></a>
## tagsSpokenLang
Перелік тегів, що визначають мови, якими вчитель розмовляє. Складається з масиву рядків що можуть набувати наступних значень.

```
"albanian", "arabic", "armenian", "azerbaijani", "belarusian", "bulgarian", "chinese", "croatian", "czech", "danish", "dutch", "english", "estonian", "finnish", "french", "georgian", "german", "greek", "hungarian", "indian", "indonesian", "japanese", "korean", "latvian", "lithuanian", "macedonian", "malaysian", "mandarin", "moldovan", "mongolian", "norwegian", "pakistani", "polish", "portuguese", "romanian", "russian", "serbian", "slovak", "slovenian", "somali", "spanish", "swedish", "taiwanese", "turkish", "ukrainian", "uzbek", "vietnamese", "welsh"
```

Масив не може бути пустим.

```
"tagsSpokenLang": [ string,.. ]
```

<a name="link_tagsTeachingLang"></a>
## tagsTeachingLang
Перелік тегів, що визначають мови, якими вчитель розмовляє. Складається з масиву рядків що можуть набувати [наступних значень](#link_agsspokenLang) .\
Масив не може бути пустим.

```
"tagsTeachingLang": [ string,.. ]
```

<a name="link_tagsNativeLang"></a>
## tagsNativeLang
Перелік тегів, що визначають мови, якими вчитель розмовляє. Складається з масиву рядків що можуть набувати [наступних значень](#link_tagsspokenLang) .\
Масив не може бути пустим.

```
"tagsNativeLang": [ string,.. ]
```


<a name="link_tagsCallApps"></a>
## tagsCallApps
Перелік тегів, що визначають які платформи можуть бути використані для проведення уроку. Складається з масиву рядків що можуть набувати наступних значень.

```
"zoom", "google meet", "microsoft teams", "skype" //на міті домовимось які ще
```

</details>
