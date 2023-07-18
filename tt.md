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

</details open>

<details>
<summary>

# USERS

</summary>

## Реєстрація

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

[test](#ADVERTS)

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

</details>

<details open>
<summary>

  # ADVERTS
 
</summary>

## Створення оголошення

Створення вчителем оголошення.

### Параметри

* `price` (float): Ціна уроку довжиною 1 годину в у.о.. Повинна бути більшою за 0.
* [`avalLength`](#avallength) (array): Перелік можливих довжин уроку.
* [`avalShedule`](#avalshedule) (array): Перелік днів та інтервалів годин, у які може бути проведений урок.
* [`tagsSpecialization`](#tagsspecialization) (array): Перелік тегів, що визначають спеціалізацію вчителя.
* [`tagsHobby`](#tagsHobby) (array): Перелік тегів, що визначають хобі вчителя.
* [`tagsSpokenLang`](#tagsspokenLang) (array): Перелік тегів, що визначають мови, якими вчитель розмовляє.
* [`tagsTeachingLang`](#tagsteachingLang) (array): Перелік тегів, що визначають мови, які вчитель викладає.
* [`tagsNativeLang`](#tagsnativeLang) (array): Перелік тегів, що визначають рідні мови вчителя.
* `shortDescription` (string): Короткий опис оголошення (200 символів).
* `fullDescription` (string): Повний опис оголошення (1000 символів).

### Тіло запиту

```json
POST /adverts/create
{
    "price": 59.99,
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

<details>
<summary>

### Структури

</summary>

#### avalLength
Перелік можливих довжин уроку. Складається з масиву цілих чисел `int`, що вказують на довжину урока в хвилинах.
`int` повинен бути рівним одному з наступних чисел: `30, 60, 90, 120`.\
Масив не може бути пустим.

```
"avalLength": [ int,.. ]
```

#### avalShedule
Перелік днів та інтервалів годин, у які може бути проведений урок. Складається з іменованого масиву типу `day: [intervals]`,
де `day` є назвою дня англійською у нижньому регістрі, `[intervals]` є двовимірним масивом розміром `[n, 2]`, і позначає інтервали,
у які може бути проведений урок. Значення інтервалу повинні належати `[0, 24]` та можуть мати дробову частину `.5` для позначення 30 хвилин.\
Масив не може бути пустим.

```
"avalShedule": [ string: [ [float, float],.. ],.. ]
```

#### tagsSpecialization
Перелік тегів, що визначають спеціалізацію вчителя. Складається з масиву рядків що можуть набувати наступних значень.

<details>
<summary></summary>

```
"for business", "basics", "for_children", "improvement" //на міті домовимось які ще
```

</details>

Масив не може бути пустим.

```
"tagsSpecialization": [ string,.. ]
```

#### tagsHobby
Перелік тегів, що визначають хобі вчителя. Складається з масиву рядків що можуть набувати наступних значень.

<details>
<summary></summary>

```
"reading", "martial_arts", "woodworking", "gardening", "video_games", "fishing yoga", "traveling", "golf", "watching_sports", "board games", "writing", "running", "tennis", "volunteer work", "dancing", "painting", "cooking", "cycling", "movie watching", "podcasts", "television", "music"
```

</details>

Масив не може бути пустим.

```
"tagsHobby": [ string,.. ]
```

#### tagsSpokenLang
Перелік тегів, що визначають мови, якими вчитель розмовляє. Складається з масиву рядків що можуть набувати наступних значень.

<details>
<summary></summary>

```
"albanian", "arabic", "armenian", "azerbaijani", "belarusian", "bulgarian", "chinese", "croatian", "czech", "danish", "dutch", "english", "estonian", "finnish", "french", "georgian", "german", "greek", "hungarian", "indian", "indonesian", "japanese", "korean", "latvian", "lithuanian", "macedonian", "malaysian", "mandarin", "moldovan", "mongolian", "norwegian", "pakistani", "polish", "portuguese", "romanian", "russian", "serbian", "slovak", "slovenian", "somali", "spanish", "swedish", "taiwanese", "turkish", "ukrainian", "uzbek", "vietnamese", "welsh"
```

</details>

Масив не може бути пустим.

```
"tagsSpokenLang": [ string,.. ]
```

#### tagsTeachingLang
Перелік тегів, що визначають мови, якими вчитель розмовляє. Складається з масиву рядків що можуть набувати [наступних значень](#tagsspokenLang).\
Масив не може бути пустим.

```
"tagsTeachingLang": [ string,.. ]
```

#### tagsNativeLang
Перелік тегів, що визначають мови, якими вчитель розмовляє. Складається з масиву рядків що можуть набувати [наступних значень](#tagsspokenLang).\
Масив не може бути пустим.

```
"tagsNativeLang": [ string,.. ]
```


</details>
  
</details>
