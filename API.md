* [/](#/)
	* [GET /languages](#link_GET_/languages)
	* [GET /specializations](#link_GET_/specializations)
	* [GET /countries](#link_GET_/countries)
* [/users](#/users)
	* [GET /users/conversations](#link_GET_/users/conversations)
	* [GET /users/:id](#link_GET_/users/:id)
	* [PATCH /users](#link_PATCH_/users)
	* [PUT /users](#link_PUT_/users)
	* [POST /users/:id/feedback](#link_POST_/users/:id/feedback)
	* [POST /users/:id/conversation](#link_POST_/users/:id/conversation)
	* [GET /users/:id/conversation](#link_GET_/users/:id/conversation)
* [/adverts](#/adverts)
	* [POST /adverts](#link_POST_/adverts)
	* [GET /adverts](#link_GET_/adverts)
	* [GET /adverts/:id](#link_GET_/adverts/:id)
	* [PATCH /adverts/:id](#link_PATCH_/adverts/:id)
	* [PUT /adverts](#link_PUT_/adverts)
	* [PUT /adverts/:id/favorite](#link_PUT_/adverts/:id/favorite)
* [/auth](#/auth)
	* [POST /auth/signup](#link_POST_/auth/signup)
	* [POST /auth/signin](#link_POST_/auth/signin)
	* [POST /auth/logout](#link_POST_/auth/logout)
	* [POST /auth/refresh](#link_POST_/auth/refresh)
	
<details open>
<summary>
 
# /

</summary>

<a name="link_GET_/languages"></a>
## GET /languages

Отримання списку усіх існуючих мов.

### Параметри

### Приклад запиту

```json
GET /languages
{
	
}
```

### Відповідь

Масив об'єктів, де кожен об'єкт описує окрему мову.

### Приклад відповіді

```json
HTTP 200
[
    {
        "id": 1,					-- Ідентифікатор мови
        "alpha2": "en",					-- Назва мови згідно кодування alpha2
        "languageEn": "English",			-- Назва мови англійською
        "languageUa": "Англійська"			-- Назва мови українською
    },
    {
        "id": 2,
        "alpha2": "uk",
        "languageEn": "Ukrainian",
        "languageUa": "Українська"
    }
]
```

### Помилки

<a name="link_GET_/specializations"></a>
## GET /specializations

Отримання списку усіх існуючих спеціалізацій.

### Параметри

### Приклад запиту

```json
GET /specializations
{
	
}
```

### Відповідь

Масив об'єктів, де кожен об'єкт описує окрему спеціалізацію.

### Приклад відповіді

```json
HTTP 200
[
    {
        "id": 1,
        "specializationEn": "Speaking language",		-- Назва спеціалізації англійською
        "specializationUa": "Розмовна мова"			-- Назва спеціалізації українською
    },
    {
        "id": 2,
        "specializationEn": "Learning the basics",
        "specializationUa": "Вивчення азів"
    }
]
```

### Помилки

<a name="link_GET_/countries"></a>
## GET /countries

Отримання списку усіх існуючих країн.

### Параметри

### Приклад запиту

```json
GET /countries
{
	
}
```

### Відповідь

Отримання списку усіх існуючих країн.

### Приклад відповіді

```json
HTTP 200
[
    {
        "id": 1,				-- Ідентифікатор країни
        "alpha2": "UA"				-- Назва країни згідно кодування alpha2
    },
    {
        "id": 2,
        "alpha2": "GB"
    }
]
```

### Помилки

</details>



<details open>
<summary>
 
# /users

</summary>

<a name="link_GET_/users/conversations"></a>
## GET /users/conversations -- Доступно тільки адміну

Отримання списку усіх отриманих повідомлень поточним користувачем.

### Параметри

### Приклад запиту

```json
GET /users/conversations
{
	
}
```

### Відповідь

Масив об'єктів, де кожен об'єкт описує окреме повідомлення.

### Приклад відповіді

```json
HTTP 200
[
    {
        "id": 3,						-- Ідентифікатор повідомлення
        "message": "Test mail",					-- Зміст повідомлення
        "writtedAt": "2023-12-11T18:46:40.458Z",		-- Дата створення повідомлення
        "isReaded": false					-- Чи було повідомлення прочитане
    },
    {
        "id": 4,
        "message": "Test2 mail",
        "writtedAt": "2023-12-11T18:46:41.062Z",
        "isReaded": false
    }
]
```

### Помилки

* 401 - Unauthorized

<a name="link_GET_/users/:id"></a>
## GET /users/:id

Отримання інформації про даного користувача.

### Параметри

* id - ідентифікатор користувача

### Приклад запиту

```json
GET /users/2
{
	
}
```

### Відповідь

Опис користувача.

### Приклад відповіді

```json
HTTP 200
{
    "id": 2,							-- Ідентифікатор користувача
    "email": "13@email.com",					-- Пошта
    "firstName": "First Name#13",				-- Ім'я
    "lastName": "PatchedName",					-- Призвіще
    "role": "user",						-- Роль (user/admin)
    "isDeleted": true,						-- Чи є користувач софт-делітнутим
    "lastVisit": "2023-12-17T13:13:28.919Z",			-- Дата останнього логіну
    "registeredAt": "2023-12-11T17:47:03.832Z",			-- Дата реєстрації
    "rating": 2,						-- Рейтинг	
    "birthday": "1999-12-31T22:00:00.000Z",			-- День народження
    "sex": "male",						-- Стать 
    "photoPath": null,						-- Шлях до фото користувача
    "aboutMe": null,						-- Опис користувача
    "advert": {							-- Оголошення користувача
	"id": 2,						-- Див GET /adverts/:id
    	"price": "123",
    	"description": "TestDesc",
    	"imagePath": "http://res.cloudinary.com/.../hj4.jpg",
    	"createdAt": "2023-12-17T13:23:34.196Z",
    	"isDeleted": false
    },
    "feedbacksToMe": [						-- Відгуки про користувача
        {																							
            "id": 3,						-- Ідентифікатор відгука
            "mark": 2,						-- Оцінка
            "message": "Test Feedback",				-- Зміст відгуку
            "createdAt": "2023-12-17T13:13:28.919Z"		-- Дата створення відгука
        }
    ],
    "feedbacksFromMe": [					-- Відгуки, створені користувачем
        {
            "id": 1,
            "mark": 2,
            "message": "Test Feedback",
            "createdAt": "2023-12-17T13:12:36.626Z"
        }
    ],
    "country": {						-- Країна користувача
        "id": 3,						-- Див GET /countries
        "alpha2": "FR"
    },
    "favoriteAdverts": [					-- Оголошення, додані до вподобаних
        {							-- Див GET /adverts/:id
            "id": 2,
            "price": "123",
            "description": "TestDesc",
            "imagePath": "http://res.cloudinary.com/.../hj4.jpg",
            "createdAt": "2023-12-17T13:23:34.196Z",
            "isDeleted": false
        }
    ]
}
```

### Помилки

* 401 - Unauthorized
* 400 - User with id [:id] not found

<a name="link_PATCH_/users"></a>
## PATCH /users

Редагування інформації про даного користувача.

### Параметри

* email - Пошта
* firstName - Ім'я
* lastName - Призвіще
* country - Країна
* birthday - Дата народження
* sex - Стать
* aboutMe - Опис користувача
* photo - Файл фото користувача

### Приклад запиту

```json
PATCH /users
{
    "email" : "newMail@mail.com",
    "firstName" : "Олег"
    "lastName" : "Олегович",
}
```

### Відповідь

Відредагована інформація про даного користувача.

### Приклад відповіді

Див GET /users/:id

### Помилки

* 401 - Unauthorized

<a name="link_PUT_/users"></a>
## PUT /users

Відновлення/видалення поточного користувача (якщо в софт-деліті то відновити і навпаки).

### Параметри

### Приклад запиту
PUT /users
```json

{
	
}
```

### Відповідь

Відредагована інформація про даного користувача.

### Приклад відповіді

Див GET /users/:id

### Помилки

* 401 - Unauthorized

<a name="link_GET_/link_POST_/users/:id/feedback"></a>
## POST /users/:id/feedback

Додавання відгука до даного користувача.

### Параметри

* mark - Оцінка; Обов'язкове поле; Повиина мати цілочислене значення в межах [1; 5]
* message - Зміст відгуку; Обов'язкове поле;

### Приклад запиту

```json
POST /users/2/feedback
{
    "mark" : 5,
    "message" : "Дуже класно пояснює :D"
}
```

### Відповідь

Інформація про створений відгук.

### Приклад відповіді

```json
HTTP 200
{
    "id": 4,								-- Ідентифікатор відгука
    "mark": 5,								-- Оцінка
    "message": "Дуже класно пояснює :D",				-- Зміст відгуку
    "createdAt": "2023-12-17T13:13:28.919Z"				-- Дата створення відгука
}
```

### Помилки

* 400 - User with id [:id] not found
* 400 - Mark cannot exceed 5.
* 400 - Mark must be at least 1.
* 400 - Mark must be an integer.
* 400 - mark should not be empty
* 400 - message should not be empty
* 401 - Unauthorized

<a name="link_POST_/users/:id/conversation"></a>
## GET /languages

Надсилання повідомлення даному користувачу.

### Параметри

message - Зміст повідомлення; Обов'язкове поле;

### Приклад запиту

```json
POST /users/1/conversation
{
    "message" : "Привіт, як справи?"
}
```

### Відповідь

Інформація про створене повідомлення.

### Приклад відповіді

```json
HTTP 200
{
    "message": "Привіт, як справи",						-- Зміст повідмлення
    "isReaded": false,								-- Чи було повідомлення прочитане
    "id": 9,									-- Ідентифікатор пвідомленння
    "writtedAt": "2023-12-17T14:08:35.763Z"					-- Дата створення повідомлення
}
```

### Помилки

* 400 - User with id [:id] not found
* 400 - message should not be empty
* 401 - Unauthorized

<a name="link_GET_/users/:id/conversation"></a>
GET /users/:id/conversation

Отримання списку усіх отриманих повідомлень даним користувачем.

### Параметри

### Приклад запиту

```json
GET /users/:id/conversation
{
	
}
```

### Відповідь

Масив об'єктів, де кожен об'єкт описує окреме повідомлення.

### Приклад відповіді

```json
HTTP 200
[
    {
        "id": 3,								-- Ідентифікатор повідомлення
        "message": "Test mail",							-- Зміст повідомлення
        "writtedAt": "2023-12-11T18:46:40.458Z",				-- Дата створення повідомлення
        "isReaded": false							-- Чи було повідомлення прочитане
    },
    {
        "id": 4,
        "message": "Test2 mail",
        "writtedAt": "2023-12-11T18:46:41.062Z",
        "isReaded": false
    }
]
```

### Помилки

* 401 - Unauthorized
	
</details>



<details open>
<summary>
 
# /adverts

</summary>

<a name="link_POST_/adverts"></a>
## POST /adverts

Створення нового оголошення.

### Параметри

* description - Опис оголошення; Обов'язкове поле
* price - Ціна урока за годину в у.о.; Обов'язкове поле; Повинна бути в межах (0; 9999]
* spokenLanguages - Перелік мов, якими може проводитись урок; Обов'язкове поле
* teachingLanguages - Перелік мов, які можуть вивчатись на уроці; Обов'язкове поле
* image - Фото до оголошення; Обов'язкове поле
* updateUser - Додаткові поля користувача, напр lastName; Обов'язкове поле
* specializations - Перелік спеціалізацій викладача; Обов'язкове поле

### Приклад запиту

```json
POST /adverts
{
    "description": "TestDesc"
    "price": "123"
    "spokenLanguages": "[ 2, 5 ]"
    "teachingLanguages": "[ 2, 3, 4 ]"
    "image": undefined
    "updateUser": "{ "lastName" : "Name", "sex" : "male", "country" : 1, "birthday" : "2000-01-01" }"
    "specializations": "[ 1, 3 ]"
}
```

### Відповідь

Інформація про створене повідомлення.

### Приклад відповіді

Див. GET /adverts

### Помилки

* 400 - description should not be empty
* 400 - Price must be less than or equal to 9999
* 400 - Price must be greater than 0
* 400 - price must b	e a number conforming to the specified constraints
* 400 - price should not be empty
* 400 - spokenLanguages should not be empty
* 400 - teachingLanguages should not be empty
* 400 - specializations should not be empty
* 401 - Unauthorized
* 409 - User cannot have more then one advert
* 500 - Internal server error може виникати, якщо не заповнені додаткові поля користувача, напр. "lastName", "sex", тощо.

<a name="link_GET_/adverts"></a>
## GET /adverts

Отримання списку усіх оголошень.

### Параметри

### Приклад запиту

```json
GET /adverts
{
	
}
```

### Відповідь

Масив об'єктів, де кожен об'єкт описує окреме оголошення.

### Приклад відповіді

```json
HTTP 200
[
    {
        "id": 2,								-- Ідентифікатор оголошення
        "price": "123",								-- Ціна уроку за годину в у.о.
        "description": "TestDesc",						-- Опис оголошення
        "imagePath": "http://res.cloudinary.com/.../hj4.jpg",			-- Шлях до зображення
        "createdAt": "2023-12-17T13:23:34.196Z",				-- Дата створення 
        "isDeleted": false,							-- Чи є софт-видалене
        "user": {								-- Інформація про користувача, що створив оголошення
        "id": 2,								-- Див GET /users
        "email": "13@email.com",
        "firstName": "First Name#15",
        "lastName": "PatchedName",
        "role": "user",
        "isDeleted": true,
        "lastVisit": "2023-12-17T13:23:34.201Z",
        "registeredAt": "2023-12-11T17:47:03.832Z",
        "rating": 2,
        "birthday": "1999-12-31T22:00:00.000Z",
        "sex": "male",
        "photoPath": null,
        "aboutMe": null,
        "country": {
            "id": 1,
            "alpha2": "UA"
            },
        "feedbacksToMe": [
            {
                "id": 4,
                "mark": 2,
                "message": "Test Feedback",
                "createdAt": "2023-12-17T14:02:14.748Z",
                "toUser": {
                    "id": 2,
                    "email": "13@email.com",
                    "firstName": "First Name#15",
                    "lastName": "PatchedName",
                    "role": "user",
                    "isDeleted": true,
                    "lastVisit": "2023-12-17T13:23:34.201Z",
                    "registeredAt": "2023-12-11T17:47:03.832Z",
                    "rating": 2,
                    "birthday": "1999-12-31T22:00:00.000Z",
                    "sex": "male",
                    "photoPath": null,
                    "aboutMe": null
                    },
                    "fromUser": {
                        "id": 4,
                        "email": "15@email.com",
                        "firstName": "\"First Name#16\"",
                        "lastName": "PatchedName",
                        "role": "user",
                        "isDeleted": false,
                        "lastVisit": "2023-12-17T14:14:21.514Z",
                        "registeredAt": "2023-12-11T17:47:05.504Z",
                        "rating": 5,
                        "birthday": "1999-12-31T22:00:00.000Z",
                        "sex": "male",
                        "photoPath": "http://res.cloudinary.com/.../ypn.jpg",
                        "aboutMe": "TestDesc"
                    }
                },
                {
                    "id": 3,
                    "mark": 2,
                    "message": "Test Feedback",
                    "createdAt": "2023-12-17T13:13:28.919Z",
                    "toUser": {
                        "id": 2,
                        "email": "13@email.com",
                        "firstName": "First Name#15",
                        "lastName": "PatchedName",
                        "role": "user",
                        "isDeleted": true,
                        "lastVisit": "2023-12-17T13:23:34.201Z",
                        "registeredAt": "2023-12-11T17:47:03.832Z",
                        "rating": 2,
                        "birthday": "1999-12-31T22:00:00.000Z",
                        "sex": "male",
                        "photoPath": null,
                        "aboutMe": null
                    },
                    "fromUser": {
                        "id": 3,
                        "email": "14@email.com",
                        "firstName": "First Name#14",
                        "lastName": "Last Name#14",
                        "role": "user",
                        "isDeleted": false,
                        "lastVisit": "2023-12-17T13:13:28.917Z",
                        "registeredAt": "2023-12-11T17:47:04.603Z",
                        "rating": 5,
                        "birthday": null,
                        "sex": null,
                        "photoPath": null,
                        "aboutMe": null
                    }
                }
            ],
            "feedbacksFromMe": [
                {
                    "id": 1,
                    "mark": 2,
                    "message": "Test Feedback",
                    "createdAt": "2023-12-17T13:12:36.626Z",
                    "toUser": {
                        "id": 1,
                        "email": "admin@email.com",
                        "firstName": "ADMIN",
                        "lastName": null,
                        "role": "admin",
                        "isDeleted": false,
                        "lastVisit": "2023-12-17T13:13:10.944Z",
                        "registeredAt": "2023-12-11T17:46:59.772Z",
                        "rating": 2,
                        "birthday": null,
                        "sex": null,
                        "photoPath": null,
                        "aboutMe": null
                    },
                    "fromUser": {
                        "id": 2,
                        "email": "13@email.com",
                        "firstName": "First Name#15",
                        "lastName": "PatchedName",
                        "role": "user",
                        "isDeleted": true,
                        "lastVisit": "2023-12-17T13:23:34.201Z",
                        "registeredAt": "2023-12-11T17:47:03.832Z",
                        "rating": 2,
                        "birthday": "1999-12-31T22:00:00.000Z",
                        "sex": "male",
                        "photoPath": null,
                        "aboutMe": null
                    }
                }
            ]
        },
        "spokenLanguages": [							-- Перелік мов, якими може проводитись урок
            {									-- Див GET /languages
                "id": 2,
                "alpha2": "uk",
                "languageEn": "Ukrainian",
                "languageUa": "Українська"
            },
            {
                "id": 5,
                "alpha2": "fr",
                "languageEn": "French",
                "languageUa": "Французька"
            }
        ],
        "teachingLanguages": [							-- Перелік мов, які можуть вивчатись на уроці
            {									-- Див GET /languages
                "id": 2,
                "alpha2": "uk",
                "languageEn": "Ukrainian",
                "languageUa": "Українська"
            },
            {
                "id": 3,
                "alpha2": "de",
                "languageEn": "German",
                "languageUa": "Німецька"
            },
            {
                "id": 4,
                "alpha2": "pl",
                "languageEn": "Polish",
                "languageUa": "Польська"
            }
        ],
        "specializations": [							-- Перелік спеціалізацій викладача
            {									-- Див GET /specializations
                "id": 1,
                "specializationEn": "Speaking language",
                "specializationUa": "Розмовна мова"
            },
            {
                "id": 3,
                "specializationEn": "For children",
                "specializationUa": "Для дітей"
            }
        ]
    }
]
```

### Помилки

* 401 - Unauthorized

<a name="link_GET_/adverts/:id"></a>
## GET /adverts/:id

Отримання інформації про дане оголошення.

### Параметри

* id - ідентифікатор оголошення

### Приклад запиту

```json
GET /adverts/1
{
	
}
```

### Відповідь

Інформація про дане оголошення.

### Приклад відповіді

Див. GET /adverts

### Помилки

* 400 - Advert with id [:id] not found
* 401 - Unauthorized

<a name="link_PATCH_/adverts/:id"></a>
## PATCH /adverts/:id

Редагування інформації про дане оголошення.

### Параметри

* id - Ідентифікатор оголошення
* image - Картинка оголошення
* price - Ціна урока за годину в у.о.
* specializations - Перелік спеціалізацій викладача
* spokenLanguages - Перелік мов, якими може проводитись урок
* teachingLanguages - Перелік мов, які можуть вивчатись на уроці

### Приклад запиту

```json
PATCH /adverts/1
{
   "price" : 321
}
```

### Відповідь

Відредагована інформація про дане оголошення.

### Приклад відповіді

Див. GET /adverts

### Помилки

* 400 - Advert with id [:id] not found
* 401 - Unauthorized

<a name="link_PUT_/adverts"></a>
## PUT /adverts

Відновлення/видалення оголошення поточного користувача (якщо в софт-деліті то відновити і навпаки).

### Параметри

### Приклад запиту

```json
PUT /adverts
{
	
}
```

### Відповідь

Відредагована інформація про дане оголошення.

### Приклад відповіді

Див GET /adverts

### Помилки

* 401 - Unauthorized

<a name="link_PUT_/adverts/:id/favorite"></a>
## PUT /adverts/:id/favorite

Додавання оголошення до вподобаних.

### Параметри

* id - Ідентифікатор оголошення

### Приклад запиту

```json
PUT /adverts/:id/favorite
{
	
}
```

### Відповідь

Інформація про дане оголошення.

### Приклад відповіді

Див GET /adverts

### Помилки

* 400 - Advert with id [:id] not found
* 401 - Unauthorized
	
</details>



<details open>
<summary>
 
# /auth

</summary>

<a name="link_POST_/auth/signup"></a>
## POST /auth/signup

Реєстрація нового користувача.

### Параметри

* email - Пошта; Обов'язкове поле; Не може повторюватись між користувача
* password - Пароль; Обов'язкове поле; Розмір [6; 16] символів, повинен містити хоча б одну велику літеру та цифру
* firstName - Ім'я; Обов'язкове поле; Розмір [2; 20] символів
* lastName - Призвіще

### Приклад запиту

```json
POST /auth/signup
{
    "email" : "testmail@email.com",
    "password" : "...",
    "firstName" : "Олег"
}
```

### Відповідь

Інформація про створеного користувача та OAuth2.0 токени.

### Приклад відповіді

```json
HTTP 200
{
    {
    "user": {									--Див. GET /users/:id
        "email": "testmail@email.com",
        "firstName": "Олег",
        "lastName": null,
        "birthday": null,
        "sex": null,
        "photoPath": null,
        "aboutMe": null,
        "id": 7,
        "role": "user",
        "isDeleted": false,
        "lastVisit": "2023-12-17T14:56:43.279Z",
        "registeredAt": "2023-12-17T14:56:43.279Z",
        "rating": 5
    },
    "tokens": {	
        "accessToken": "...",
        "refreshToken": "..."
    }
}
```

### Помилки

* 400 - Email [email] has an invalid format
* 400 - email should not be empty
* 400 - email must be an email
* 400 - Password must have at least 6 and at most 16 characters, including at least one uppercase letter and one digit
* 400 - password should not be empty
* 400 - Name must have at least 2 and at most 20 characters
* 400 - firstName should not be empty
* 409 - User with email [email] already exists

<a name="link_POST_/auth/signin"></a>
## POST /auth/signin

Вхід користувача.

### Параметри

* email - Пошта; Обов'язкове поле
* password - Пароль; Обов'язкове поле

### Приклад запиту

```json
POST /auth/signin
{
    "email" : "testmail@email.com",
    "password" : "..."
}
```

### Відповідь

Інформація про залогіненого користувача та OAuth2.0 токени.

### Приклад відповіді

```json
HTTP 200
{
    {
    "user": {									--Див. GET /users/:id
        "email": "testmail@email.com",
        "firstName": "Олег",
        "lastName": null,
        "birthday": null,
        "sex": null,
        "photoPath": null,
        "aboutMe": null,
        "id": 7,
        "role": "user",
        "isDeleted": false,
        "lastVisit": "2023-12-17T14:56:43.279Z",
        "registeredAt": "2023-12-17T14:56:43.279Z",
        "rating": 5
    },
    "tokens": {	
        "accessToken": "...",
        "refreshToken": "..."
    }
}
```

### Помилки

* 400 - email should not be empty
* 400 - email must be an email
* 400 - password should not be empty
* 403 - Access denied

<a name="link_POST_/auth/logout"></a>
## POST /auth/logout

TODO

### Параметри

-

### Приклад запиту

```json

{
	
}
```

### Відповідь

	

### Приклад відповіді

```json
HTTP 200

```

### Помилки

-

<a name="link_POST_/auth/refresh"></a>
## POST /auth/refresh

TODO

### Параметри

-

### Приклад запиту

```json

{
	
}
```

### Відповідь

	

### Приклад відповіді

```json
HTTP 200

```

### Помилки

-
	
</details>
