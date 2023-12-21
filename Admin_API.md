* [/admin](#/admin)
	* [GET /admin/users](#link_GET_/admin/users)
	* [GET /admin/adverts](#link_GET_/admin/adverts)
	* [GET /admin/feedbacks](#link_GET_/admin/feedbacks)
	* [GET /admin/languages](#link_GET_/admin/languages)
	* [GET /admin/specializations](#link_GET_/admin/specializations)
	* [GET /admin/countries](#link_GET_/admin/countries)
	* [PUT /admin/users/:id](#link_PUT_/admin/users/:id)
	* [PUT /admin/adverts/:id](#link_PUT_/admin/adverts/:id)
	* [PATCH /admin/users/:id](#link_PATCH_/admin/users/:id)
	* [PATCH /admin/adverts/:id](#link_PATCH_/admin/adverts/:id)
	* [PATCH /admin/languages/:id](#link_PATCH_/admin/languages/:id)
	* [PATCH /admin/specializations/:id](#link_PATCH_/admin/specializations/:id)
	* [PATCH /admin/countries/:id](#link_PATCH_/admin/countries/:id)
	* [POST /admin/languages](#link_POST_/admin/languages)
	* [POST /admin/specializations](#link_POST_/admin/specializations)
	* [POST /admin/countries](#link_POST_/admin/countries)
	* [DELETE /admin/languages/:id](#link_DELETE_/admin/languages/:id)
	* [DELETE /admin/specializations/:id](#link_DELETE_/admin/specializations/:id)
	* [DELETE /admin/countries/:id](#link_DELETE_/admin/countries/:id)

<details open>
<summary>
 
# /admin

</summary>

<a name="link_GET_/admin/users"></a>
# GET /admin/users

Отримання списку усіх користувачів.
	
### Параметри

### Приклад запиту

```json
GET /admin/users
{
	
}
```

### Відповідь

Масив об'єктів, де кожен об'єкт описує окремого користувача.

### Приклад відповіді

```json
HTTP 200
[
    {
        "id": 1,
        "email": "admin@email.com",
        "firstName": "ADMIN",
        "lastName": null,
        "role": "admin",
        "isDeleted": false,
        "lastVisit": "2023-12-20T22:53:43.864Z",
        "registeredAt": "2023-12-11T17:46:59.772Z",
        "rating": 2,
        "birthday": null,
        "sex": null,
        "photoPath": null,
        "aboutMe": null,
        "advert": null,
        "feedbacksToMe": [
            {
                "id": 1,
                "mark": 2,
                "message": "Test Feedback",
                "createdAt": "2023-12-17T13:12:36.626Z"
            },
            {
                "id": 2,
                "mark": 2,
                "message": "Test Feedback",
                "createdAt": "2023-12-17T13:13:10.944Z"
            }
        ],
        "feedbacksFromMe": [],
        "country": null,
        "favoriteAdverts": []
    },
    {
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
        "aboutMe": null,
        "advert": {
            "id": 2,
            "price": "123",
            "description": "TestDesc",
            "imagePath": "http://res.cloudinary.com/.../hj4.jpg",
            "createdAt": "2023-12-17T13:23:34.196Z",
            "isDeleted": false
        },
        "feedbacksToMe": [
            {
                "id": 3,
                "mark": 2,
                "message": "Test Feedback",
                "createdAt": "2023-12-17T13:13:28.919Z"
            },
            {
                "id": 4,
                "mark": 2,
                "message": "Test Feedback",
                "createdAt": "2023-12-17T14:02:14.748Z"
            },
            {
                "id": 5,
                "mark": 2,
                "message": "asdfaaaaa",
                "createdAt": "2023-12-17T14:09:06.357Z"
            }
        ],
        "feedbacksFromMe": [
            {
                "id": 1,
                "mark": 2,
                "message": "Test Feedback",
                "createdAt": "2023-12-17T13:12:36.626Z"
            }
        ],
        "country": {
            "id": 1,
            "alpha2": "UA"
        },
        "favoriteAdverts": [
            {
                "id": 2,
                "price": "123",
                "description": "TestDesc",
                "imagePath": "http://res.cloudinary.com/.../hj4.jpg",
                "createdAt": "2023-12-17T13:23:34.196Z",
                "isDeleted": false
            }
        ]
    }
]
```

### Помилки

* 401 - Unauthorized

<a name="link_GET_/admin/adverts"></a>
# GET /admin/adverts

Отримання списку усіх оголошеннь.
	
### Параметри

### Приклад запиту

```json
GET /admin/adverts
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
        "id": 1,
        "price": "123",
        "description": "TestDesc",
        "imagePath": "http://res.cloudinary.com/.../dmt.jpg",
        "createdAt": "2023-12-17T12:09:54.982Z",
        "isDeleted": true,
        "user": null,
        "spokenLanguages": [
            {
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
        "teachingLanguages": [
            {
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
        "specializations": [
            {
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
    },
    {
        "id": 2,
        "price": "123",
        "description": "TestDesc",
        "imagePath": "http://res.cloudinary.com/.../hj4.jpg",
        "createdAt": "2023-12-17T13:23:34.196Z",
        "isDeleted": false,
        "user": {
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
            "aboutMe": null,
            "country": {
                "id": 1,
                "alpha2": "UA"
            },
            "feedbacksToMe": [
                
                {
                    "id": 5,
                    "mark": 2,
                    "message": "asdfaaaaaa",
                    "createdAt": "2023-12-17T14:09:06.357Z",
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
                        "lastVisit": "2023-12-17T14:42:45.386Z",
                        "registeredAt": "2023-12-11T17:47:05.504Z",
                        "rating": 5,
                        "birthday": "1999-12-31T22:00:00.000Z",
                        "sex": "male",
                        "photoPath": "http://res.cloudinary.com/.../ypn.jpg",
                        "aboutMe": "TestDesc"
                    }
                },
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
                        "lastVisit": "2023-12-17T14:42:45.386Z",
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
                        "lastVisit": "2023-12-19T23:05:17.695Z",
                        "registeredAt": "2023-12-11T17:47:04.603Z",
                        "rating": 2,
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
                        "lastVisit": "2023-12-20T22:53:43.864Z",
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
        "spokenLanguages": [
            {
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
        "teachingLanguages": [
            {
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
        "specializations": [
            {
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
    },
```

### Помилки

* 401 - Unauthorized

<a name="link_GET_/admin/feedbacks"></a>
# GET /admin/feedbacks

Отримання списку усіх відгуків.
	
### Параметри

### Приклад запиту

```json
GET /admin/feedbacks
{
	
}
```

### Відповідь

Масив об'єктів, де кожен об'єкт описує окремий відгук.

### Приклад відповіді

```json
HTTP 200
[
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
            "lastVisit": "2023-12-20T22:53:43.864Z",
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
    },
    {
        "id": 2,
        "mark": 2,
        "message": "Test Feedback",
        "createdAt": "2023-12-17T13:13:10.944Z",
        "toUser": {
            "id": 1,
            "email": "admin@email.com",
            "firstName": "ADMIN",
            "lastName": null,
            "role": "admin",
            "isDeleted": false,
            "lastVisit": "2023-12-20T22:53:43.864Z",
            "registeredAt": "2023-12-11T17:46:59.772Z",
            "rating": 2,
            "birthday": null,
            "sex": null,
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
            "lastVisit": "2023-12-19T23:05:17.695Z",
            "registeredAt": "2023-12-11T17:47:04.603Z",
            "rating": 2,
            "birthday": null,
            "sex": null,
            "photoPath": null,
            "aboutMe": null
        }
    }
]
```

### Помилки

* 401 - Unauthorized

<a name="link_GET_/admin/languages"></a>
# GET /admin/languages

Отримання списку усіх мов.
	
### Параметри

### Приклад запиту

```json
GET /admin/languages
{
	
}
```

### Відповідь

Масив об'єктів, де кожен об'єкт описує окрему мову.

### Приклад відповіді

```json
HTTP 200

```

### Помилки

* 401 - Unauthorized

<a name="link_GET_/admin/specializations"></a>
# GET /admin/specializations

Отримання списку усіх спеціалізацій.
	
### Параметри

### Приклад запиту

```json
GET /admin/specializations
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
        "alpha2": "en",
        "languageEn": "English",
        "languageUa": "Англійська"
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

* 401 - Unauthorized

<a name="link_GET_/admin/countries"></a>
# GET /admin/countries

Отримання списку усіх країн
	
### Параметри

### Приклад запиту

```json
GET /admin/countries
{
	
}
```

### Відповідь

Масив об'єктів, де кожен об'єкт описує окрему країну.

### Приклад відповіді

```json
HTTP 200
[
    {
        "id": 1,
        "alpha2": "UA"
    },
    {
        "id": 2,
        "alpha2": "GB"
    }
]
```

### Помилки

* 401 - Unauthorized

<a name="link_PUT_/admin/users/:id"></a>
# PUT /admin/users/:id

Відновлення/видалення даного користувача (якщо в софт-деліті то відновити і навпаки).
	
### Параметри

### Приклад запиту

```json
PUT /admin/users/:id
{
	
}
```

### Відповідь

Відредагована інформація про даного користувача.

### Приклад відповіді

Див. GET /users/:id

### Помилки

* 401 - Unauthorized

<a name="link_PUT_/admin/adverts/:id"></a>
# PUT /admin/adverts/:id

Відновлення/видалення даного оголошення (якщо в софт-деліті то відновити і навпаки).
	
### Параметри

### Приклад запиту

```json
PUT /admin/adverts/:id
{
	
}
```

### Відповідь

Відредагована інформація про дане оголошення.

### Приклад відповіді

Див. GET /adverts

### Помилки

* 401 - Unauthorized

<a name="link_PATCH_/admin/users/:id"></a>
# PATCH /admin/users/:id

Відновлення/видалення даного користувача (якщо в софт-деліті то відновити і навпаки).
	
### Параметри

### Приклад запиту

```json
PATCH /admin/users/2
{
    "firstName" : "Better",
    "lastName" : "Name"
}
```

### Відповідь

Відредагована інформація про даного користувача.

### Приклад відповіді

Див. GET /users/:id

### Помилки

* 400 - User with id [id] not found
* 401 - Unauthorized

<a name="link_PATCH_/admin/adverts/:id"></a>
# PATCH /admin/adverts/:id

Редагування інформації про дане оголошення.
	
### Параметри

### Приклад запиту

```json
PATCH /admin/adverts/3
{
    "description" : "Better description"
}
```

### Відповідь

Відредагована інформація про дане оголошення.

### Приклад відповіді

Див. GET /adverts

### Помилки

* 400 - Advert with id [id] not found
* 401 - Unauthorized

<a name="link_PATCH_/admin/languages/:id"></a>
# PATCH /admin/languages/:id

Редагування інформації про дану мову.
	
### Параметри

### Приклад запиту

```json
PATCH /admin/languages/5
{
    "languageEn": "English"
}
```

### Відповідь

Відредагована інформація про дану мову.

### Приклад відповіді

Див. GET /languages

### Помилки

* 400 - Language with id [id] not found
* 401 - Unauthorized

<a name="link_PATCH_/admin/specializations/:id"></a>
# PATCH /admin/specializations/:id

Редагування інформації про дану спеціалізацію.
	
### Параметри

### Приклад запиту

```json
PATCH /admin/specializations/2
{
    "specializationUa": "Розмовна мова"
}
```

### Відповідь

Відредагована інформація про дану спеціалізацію.

### Приклад відповіді

Див. GET /specializations

### Помилки

* 400 - Specialization with id [id] not found
* 401 - Unauthorized

<a name="link_PATCH_/admin/countries/:id"></a>
# PATCH /admin/countries/:id

Редагування інформації про дану країну.
	
### Параметри

### Приклад запиту

```json
PATCH /admin/countries/4
{
    "alpha2": "UA"
}
```

### Відповідь

Відредагована інформація про дану країну.

### Приклад відповіді

Див. GET /countries

### Помилки

* 400 - Country with id [id] not found
* 401 - Unauthorized

<a name="link_POST_/admin/languages"></a>
# POST /admin/languages

Додавання нової мови.
	
### Параметри

### Приклад запиту

```json
POST /admin/languages
{
    "alpha2": "JP",				-- Назва мови згідно кодування alpha2
    "languageEn": "Japanese",			-- Назва мови англійською
    "languageUa": "Японська"			-- Назва мови українською
}
```

### Відповідь

Інформація про створену мову.

### Приклад відповіді

Див. GET /languages

### Помилки

* 400 - Field must be a string
* 400 - Field must be 2 characters long
* 400 - alpha2 should not be empty
* 400 - languageEn should not be empty
* 400 - languageUa should not be empty
* 400 - Language already exists in the database
* 401 - Unauthorized

<a name="link_POST_/admin/specializations"></a>
# POST /admin/specializations

Додавання нової спеціалізації.
	
### Параметри

### Приклад запиту

```json
POST /admin/specializations
{
    "specializationEn": "For children",		-- Назва спеціалізації англійською
    "specializationUa": "Для дітей"		-- Назва спеціалізації українською
}
```

### Відповідь

Інформація про створену спеціалізацію.

### Приклад відповіді

Див. GET /specializations

### Помилки

* 400 - specializationEn should not be empty
* 400 - specializationUa should not be empty
* 400 - Specialization already exists in the database
* 401 - Unauthorized

<a name="link_POST_/admin/countries"></a>
# POST /admin/countries

Додавання нової країни.
	
### Параметри

### Приклад запиту

```json
POST /admin/countries
{
    "alpha2": "JP"				-- Назва країни згідно кодування alpha2
}
```

### Відповідь

Інформація про створену країну.

### Приклад відповіді

Див. GET /countries

### Помилки

* 400 - Field must be a string
* 400 - Field must be 2 characters long
* 400 - alpha2 should not be empty
* 400 - Country already exists in the database
* 401 - Unauthorized

<a name="link_DELETE_/admin/languages/:id"></a>
# DELETE /admin/languages/:id

Видалення даної мови.
	
### Параметри

### Приклад запиту

```json
DELETE /admin/languages/:id
{
	
}
```

### Відповідь

Інформація про видалену мову.

### Приклад відповіді

Див. GET /languages

### Помилки

* 401 - Unauthorized

<a name="link_DELETE_/admin/specializations/:id"></a>
# DELETE /admin/specializations/:id

Видалення даної спеціалізації.
	
### Параметри

### Приклад запиту

```json
DELETE /admin/specializations/:id
{
	
}
```

### Відповідь

Інформація про видалену спеціалізацію.

### Приклад відповіді

Див. GET /specializations

### Помилки

* 401 - Unauthorized

<a name="link_DELETE_/admin/countries/:id"></a>
# DELETE /admin/countries/:id

Видалення даної країни
	
### Параметри

### Приклад запиту

```json
DELETE /admin/countries/:id
{
	
}
```

### Відповідь

Інформація про видалену країну.

### Приклад відповіді

Див. GET /countries

### Помилки

* 401 - Unauthorized

<details open>
