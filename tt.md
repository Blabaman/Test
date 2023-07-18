HH# API

## Помилки

### Тіло відповіді

```json
HTTP 400
{
    "errorCode": "код_помилки_зміїним_стилем",
    "errorMessage": "Юзер-френдлі опис помилки"
}
```

Усі помилки валідації даних повинні повертати код `400`, код помилки `errorCode` та опис помилки `errorMessage`.

Спроби використання запитів, що не відповідають типу користувача (наприклад запис на урок вчителем) повинні повертати код `403`

Запити типу `GET` з невірним `id` повинні повертати код `404`

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

<details>
<summary>

## Реєстрація

</summary>

Створення нового користувача.

### Параметри

* `name` (string) : Ім'я користувача. Складається з ненульової кількості символів, що можуть бути розділені пробілами.

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

}
```

### Помилки

* `user_already_exists`: пошта вже прив'язана до іншого користувача.

* `invalid_value:` д.п. відсутній символ '@' у пошті.

</details>

## Вхід

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

}
```

### Помилки

* `invalid_credentials`: невірний пароль або відсутній користувач з `email` поштою.
* `invalid_value`: д.п. відсутній символ '@' у пошті.

## Вихід

Вихід користувача з системи.

### Тіло запиту

```json
POST /users/logout
```

### Відповідь

```json
HTTP 200
{

}
```

### Помилки

Відсутні

## Створення оголошення

Створення вчителем оголошення.

### Параметри

* `price` (float): Ціна уроку довжиною 1 годину в у.о.. Повинна бути більшою за 0.
* `avalLength` (JSON): Перелік можливих довжин уроку.
* `avalShedule` (JSON): Перелік днів та інтервалів годин, у які може бути проведений урок.
* `tagsSpecialization` (JSON): Перелік тегів, що визначають спеціалізацію вчителя.
* `tagsHobby` (JSON): Перелік тегів, що визначають хобі вчителя.
* `tagsSpokenLang` (JSON): Перелік тегів, що визначають мови, якими вчитель розмовляє.
* `tagsTeachingLang` (JSON): Перелік тегів, що визначають мови, які вчитель викладає.
* `tagsNativeLang` (JSON): Перелік тегів, що визначають рідні мови вчителя.
* `shortDescription` (string): Короткий опис оголошення (200 символів).
* `fullDescription` (string): Повний опис оголошення (1000 символів).

### Тіло запиту

```json
POST /adverts/create
{
    "price": 59.99,
    "avalLength": [ 30, 60, 120 ],
    "avalShedule": [ [13, 15.5], [18, 18.5] ],
    "tagsSpecialization": [ "improvement", "basics" ],
    "tagsHobby": [ "fishing", "gardening", "board games" ],
    "tagsSpokenLang": [ "ukrainian", "english", "german" ],
    "tagsTeachingLang": [ "english", "german" a],
    "tagsNativeLang": [ "ukrainian" ],
    "shortDescription": "This is a short desctiption",
    "fullDescription": "This is a full desctiption"
}
```

### Відповідь

```json
HTTP 200
{
    id: 541
}
```

### Помилки

* `invalid_operation`: користувач вже має огологшення.
* `invalid_value`: д.п. пустий перелік довжин уроку.
* `invalid_tag`: використання невалідного тегу, д.п. `"cheese"` у `tagsTeachingLang`.
* `description_too_long`: довжина опису перевищує максимальну.

### Схеми

avalLength

```json
avalLength {
    [int[, int]
}
```
