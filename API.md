* [Помилки](#Помилки)
* [Auth](#Auth)
  * [Signup](#Signup)
  * [Signin](#Signin)
  * [Signout](#Signout)
* [Adverts](#Adverts)
  * [Adverts (POST)](#Adverts (POST))
  * [Adverts (GET)](#Adverts (GET))
  * [Adverts/id](#Adverts/id)
* [Users](#Users)
  * [Users (GET)](#Users (GET))
  * [Users/id](#Users/id)
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

# Auth

</summary>

## Signup

Створення нового користувача.

### Параметри

* `name` (string) : Ім'я користувача. Складається з ненульової кількості літер, що можуть бути розділені пробілами.
* `email` (string) : Електронна пошта користувача. На одну пошту може бути зареєстрований тільки один користувач.
* `password` (string) : Пароль користувача. Складається з 8-24 довільних символів.

### Тіло запиту

```json
POST /auth/signup
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "password": "123qwerty"
}
```

### Відповідь

* `email` (string) : Електронна пошта користувача.
* `name` (string) : Ім'я користувача.
* `id` (int) : Унікальний ідентифікатор користувача
* `role` (string) : Роль користувача. Може мати значення **user** або **admin**
* `isDeleted` (bool) : Флажок, що вказує чи користувач є софт-видаленим.

```json
HTTP 201
{
   "user": {
        "email": "john.smith@gmail.com",
        "name": "John Smith",
        "id": 10,
        "role": "user",
        "isDeleted": false
    },
    "tokens": {
        "accessToken": "xxx",
        "refreshToken": "yyy"
    }
}
```

## Signin

Вхід користувача до системи.

### Параметри

* `email` (string) : Електронна пошта користувача.
* `password` (string) : Пароль користувача.

### Тіло запиту

```json
POST /auth/signin
{
    "email": "john.smith@gmail.com",
    "password": "123qwerty"
}
```

#### Відповідь

* `email` (string) : Електронна пошта користувача.
* `name` (string) : Ім'я користувача.
* `id` (int) : Унікальний ідентифікатор користувача
* `role` (string) : Роль користувача. Може мати значення **user** або **admin**
* `isDeleted` (bool) : Флажок, що вказує чи користувач є софт-видаленим.

```json
HTTP 200
{
   "user": {
        "email": "john.smith@gmail.com",
        "name": "John Smith",
        "id": 10,
        "role": "user",
        "isDeleted": false
    },
    "tokens": {
        "accessToken": "xxx",
        "refreshToken": "yyy"
    }
}
```

## Signout

Вихід користувача з системи.

### Тіло запиту

```json
POST /auth/signout
```

### Відповідь

```json
HTTP 200
{
    
}
```

</details>

<details open>
<summary>

# Adverts
 
</summary>

## Adverts (POST)

Створення вчителем оголошення.

### Параметри

* `price` (float): Ціна уроку довжиною 1 годину в у.о.. Повинна бути більшою за 0.
* `imagePath` (string): Шлях до зображення.
* ~~[avalLength](#link_avalLength) (array): Перелік можливих довжин уроку.~~
* ~~[avalShedule](#link_avalshedule) (array): Перелік днів та інтервалів годин, у які може бути проведений урок.~~
* ~~[tagsSpecialization](#link_tagsspecialization) (array): Перелік тегів, що визначають спеціалізацію вчителя.~~
* [hobbies](#link_tagsHobby) (array): Перелік тегів, що визначають хобі вчителя.
* [spokenLanguages](#link_tagsspokenLang) (array): Перелік тегів, що визначають мови, якими вчитель розмовляє.
* [teachingLanguages](#link_tagsteachingLang) (array): Перелік тегів, що визначають мови, які вчитель викладає.
* ~~[tagsNativeLang](#link_tagsnativeLang) (array): Перелік тегів, що визначають рідні мови вчителя.~~
* `shortDescription` (string): Короткий опис оголошення (200 символів).
* ~~`fullDescription` (string): Повний опис оголошення (1000 символів).~~

### Тіло запиту

```json
POST /adverts
{
   "shortDescription" : "Meaningful description",
   "price" : 10,
   "imagePath" : "flag.jpg",
   "hobbies" : [ {"hobby": "Програмування"}, {"hobby": "Плавання"} ],
   "spokenLanguages":[ {"language": "Українська"}, {"language": "English"} ],
   "teachingLanguages":[ {"language": "English"} ]
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

## Adverts (GET)

Повертає усі видимі оголошення

### Параметри


### Тіло запиту

```json
GET /adverts/
{
}
```

### Відповідь

Масив елеменів, що описують оголошення, а також користувачів якому вони належать.

* `id` (int): унікальний ідентифікатор оголошення.
* `price` (float): Ціна уроку довжиною 1 годину в у.о.. Повинна бути більшою за 0.
* `shortDescription` (string): Короткий опис оголошення (200 символів).
* `imagePath` (string): Шлях до зображення.
* `createdAt` (string): Дата створення оголошення.
* `isDeleted` (bool) : Флажок, що вказує чи оголошення є софт-видаленим.
* [hobbies](#link_tagsHobby) (array): Перелік тегів, що визначають хобі вчителя.
* [spokenLanguages](#link_tagsspokenLang) (array): Перелік тегів, що визначають мови, якими вчитель розмовляє.
* [teachingLanguages](#link_tagsteachingLang) (array): Перелік тегів, що визначають мови, які вчитель викладає.

```json
HTTP 200
{
   [
     {
        "id": 6,
        "price": "33.33",
        "shortDescription": "35",
        "imagePath": "1111",
        "createdAt": "2023-09-09T17:24:16.830Z",
        "isDeleted": false,
        "user": {
            "id": 13,
            "email": "fam111ily@gmail.ua",
            "name": "Lalala",
            "role": "user",
            "isDeleted": false
        },
        "hobbies": [
            {
                "hobby": "Шахи"
            },
            {
                "hobby": "Танці"
            },
            {
                "hobby": "Шоу по тв"
            }
        ],
        "spokenLanguages": [],
        "teachingLanguages": []
    },
    {
        "id": 7,
        "price": "1509.999",
        "shortDescription": "polski jezyk тест",
        "imagePath": "image789.jpg",
        "createdAt": "2023-09-09T17:24:16.830Z",
        "isDeleted": false,
        "user": {
            "id": 14,
            "email": "fam11l1ily@gmail.ua",
            "name": "Lalala",
            "role": "user",
            "isDeleted": false
        },
        "hobbies": [
            {
                "hobby": "Шахи"
            },
            {
                "hobby": "58"
            },
            {
                "hobby": "Розробка"
            },
            {
                "hobby": "Вокал"
            }
        ],
        "spokenLanguages": [
            {
                "language": "ukrainian"
            },
            {
                "language": "polski"
            },
            {
                "language": "english"
            }
        ],
        "teachingLanguages": [
            {
                "language": "ukrainian"
            },
            {
                "language": "polski"
            },
            {
                "language": "english"
            }
        ]
    }
  ]
}
```

## Adverts/id

Опис оголошення з даним ідентифікатором, а також користувача якому воно належить

### Параметри

* `advertId` (int): ідентифікатор оголошення.

### Тіло запиту

```json
GET /adverts/6
{

}
```

### Відповідь

Повний опис оголошення.

* `id` (int): унікальний ідентифікатор оголошення.
* `price` (float): Ціна уроку довжиною 1 годину в у.о.. Повинна бути більшою за 0.
* `shortDescription` (string): Короткий опис оголошення (200 символів).
* `imagePath` (string): Шлях до зображення.
* `createdAt` (string): Дата створення оголошення.
* `isDeleted` (bool) : Флажок, що вказує чи оголошення є софт-видаленим.
* [hobbies](#link_tagsHobby) (array): Перелік тегів, що визначають хобі вчителя.
* [spokenLanguages](#link_tagsspokenLang) (array): Перелік тегів, що визначають мови, якими вчитель розмовляє.
* [teachingLanguages](#link_tagsteachingLang) (array): Перелік тегів, що визначають мови, які вчитель викладає.

```json
HTTP 200
{
    "id": 6,
    "price": "33.33",
    "shortDescription": "35",
    "imagePath": "1111",
    "createdAt": "2023-09-09T17:24:16.830Z",
    "isDeleted": false,
    "user": {
        "id": 13,
        "email": "fam111ily@gmail.ua",
        "name": "Lalala",
        "role": "user",
        "isDeleted": false
    },
    "hobbies": [
        {
            "hobby": "Шахи"
        },
        {
            "hobby": "Танці"
        },
        {
            "hobby": "Шоу по тв"
        }
    ],
    "spokenLanguages": [],
    "teachingLanguages": []
}
```

</details>

<details open>
<summary>
 
# Users

</summary>

## Users (GET)

Повертає усіх видимих користувачів, а також їхні оголошення (якщо є).

### Параметри

### Тіло запиту

```json
GET /users
{

}
```

### Відповідь

* `email` (string) : Електронна пошта користувача.
* `name` (string) : Ім'я користувача.
* `id` (int) : Унікальний ідентифікатор користувача
* `role` (string) : Роль користувача. Може мати значення **user** або **admin**
* `isDeleted` (bool) : Флажок, що вказує чи користувач є софт-видаленим.

```json
HTTP 200
    {
        "id": 5,
        "email": "Dedefc@gmail.ua",
        "name": "Lalala",
        "role": "user",
        "isDeleted": false,
        "advert": {
            "id": 4,
            "price": "333333",
            "shortDescription": "35",
            "imagePath": "23",
            "createdAt": "2023-09-09T17:24:16.830Z",
            "isDeleted": true
        }
    },
    {
        "id": 6,
        "email": "f@gmail.ua",
        "name": "Lalala",
        "role": "user",
        "isDeleted": false,
        "advert": null
    },
    {
        "id": 32,
        "email": "oouuttBflli@gmail.ua",
        "name": "BBBBB",
        "role": "user",
        "isDeleted": false,
        "advert": null
    }
```

## Users/id

Опис користувача з даним ідентифікатором, а також оголошення яке йому належить (якщо є)

### Параметри

### Тіло запиту

```json
GET /users/1
{

}
```

### Відповідь

* `email` (string) : Електронна пошта користувача.
* `name` (string) : Ім'я користувача.
* `id` (int) : Унікальний ідентифікатор користувача
* `role` (string) : Роль користувача. Може мати значення **user** або **admin**
* `isDeleted` (bool) : Флажок, що вказує чи користувач є софт-видаленим.

```json
    "id": 1,
    "email": "deddfc@gmail.ua",
    "name": "Lalala",
    "role": "user",
    "isDeleted": true,
    "advert": {
        "id": 1,
        "price": "33.33",
        "shortDescription": "35",
        "imagePath": "23",
        "createdAt": "2023-09-09T17:24:16.830Z",
        "isDeleted": true
    }
```

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
