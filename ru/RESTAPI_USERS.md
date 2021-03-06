﻿# Пользователи

Управление пользователями осуществляется в рамках клиента в котором созданы учетные данные. 
Роли пользователей в клиенте: 0 - пользователь, 1 - менеджер, 2 - аккаунт менеджер.
API позволяет манипулировать пользователями в роли "пользователь".

* **Сервер** - api.storyclm.com
* **Поддерживаемы клиенты** - работающие от имени пользователя, работающие от имени сервиса. 


### Create User

Создает и добавляет нового пользователя в клиент.
Пользователь создается в роли "User".
Поля "username" и "password" обязательны.

**Запрос:**

* **Method:** POST
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users

**Тело запроса:**
``` json
{
  "username": "test@test.com",
  "email": "test@test.com",
  "phone": "79190001095",
  "name": "Владимир Титов",
  "location": "Ставрополь",
  "birthDate": "",
  "gender": true,
  "password": "1234"
}
```
**Пример**: https://api.storyclm.com/v1/users

**Ответ:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:
``` json
{
  "id": "2f94a899-7059-4bac-beb1-a3708c8938f3",
  "password": "1234",
  "username": "test@test.com",
  "email": "test@test.com",
  "phone": "79190001095",
  "name": "Владимир Титов",
  "location": "Ставрополь",
  "birthDate": null,
  "gender": true
}
```
### Update User

Обновляет профиль пользователя.
Обновляются все поля профиля кроме "Username".
Объект обновляется целиком.
Поле "id" обязательно.

**Запрос:**

* **Method:** PUT
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users

**Тело запроса:**
``` json
{
  "id": "2f94a899-7059-4bac-beb1-a3708c8938f3",
  "email": "test@testtest.com",
  "phone": "79197900000",
  "name": "Кирилл Титов",
  "location": "Черкесск",
  "birthDate": "",
  "gender": false
}
```
**Пример**: https://api.storyclm.com/v1/users

**Ответ:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:
``` json
{
  "id": "2f94a899-7059-4bac-beb1-a3708c8938f3",
  "username": null,
  "email": "test@testtest.com",
  "phone": "79197900000",
  "name": "Кирилл Титов",
  "location": "Черкесск",
  "birthDate": null,
  "gender": false
}
```
### Get Users

Получает список пользователей клиента.
Каждый объект списка состоит из идентификатора пользователя, имени пользователя и идентификатора роли.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users

**Пример**: https://api.storyclm.com/v1/users

**Ответ:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:
``` json
[
  {
    "id": "a4be8f4a-96c5-49b8-87c9-51b0de7c869b",
    "username": "eklesia@gmail.com",
    "role": 2
  },
  {
    "id": "1f6f7f74-3407-4521-a19d-42fd0b85a8b9",
    "username": "wtselofan@yandex.ru",
    "role": 0
  },
  {
    "id": "abf8bc0e-3f65-4e06-8f98-43986ede5dd3",
    "username": "tselkofan1@yandex.ru",
    "role": 1
  },
  {
    "id": "fe84233b-0f47-4a7e-9ad8-bec78f4b5857",
    "username": "test@mail.com",
    "role": 0
  },
  {
    "id": "b1ae249b-22c4-4b0b-a9ec-66f0521a4715",
    "username": "rst-k169@ya.ru",
    "role": 0
  },
  {
    "id": "8b23dfb9-cfd7-4521-95a8-c9649ecf2d27",
    "username": "test@test.com",
    "role": 0
  }
]
```
### Get User

Получает профиль пользователя по идентификатору.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}
* **URL параметры:**
  * **\{ userId:string }** - идентификатор пользователя;

**Пример**: https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3

**Ответ:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:
``` json
{
  "id": "2f94a899-7059-4bac-beb1-a3708c8938f3",
  "username": "test@test.com",
  "email": "test@testtest.com",
  "phone": "79197900000",
  "name": "Кирилл Титов",
  "location": "Черкесск",
  "birthDate": null,
  "gender": false
}
```
### Password

Обновляет текущий пароль. Пароль должен быть не менее четырех символов.

**Запрос:**

* **Method:** PUT
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/password
* **URL параметры:**
  * **\{ userId:string }** - идентификатор пользователя;

**Тело запроса:**
``` json
{
  "password": "test",
}
```

**Пример**: https://api.storyclm.com/v1/users/73f329f8-50b4-414b-9b71-8f760b6dab8a/password

**Ответ:**

* **Тело ответа**:
``` json

```

### Exists

Проверяет существования пользователя в системе.
Вернет профиль если пользователь зарегистрирован и добавлен в клиент.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/exists?username={username}
* **URL параметры:**
  * **\{ username:string }** - имя пользователя;

**Пример**: https://api.storyclm.com/v1/users/exists?username=test@test.com

**Ответ:**

* **Тело ответа**:
``` json
{
  "id": "8b23dfb9-cfd7-4521-95a8-c9649ecf2d27",
  "username": "test@test.com",
  "email": "test@test.com",
  "phone": "79190001095",
  "name": "Владимир Титов",
  "location": "Ставрополь",
  "birthDate": null,
  "gender": true
}
```

### Add user to group

Добавляет пользователя в группу.

**Запрос:**

* **Method:** PUT
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/group/{groupId:int}
* **URL параметры:**
  * **\{ userId:string }** - идентификатор пользователя;
  * **\{ groupId:int }** - идентификатор группы;

**Пример**: https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/group/57

**Ответ:**

* **Тело ответа**:
``` json

```
### Remove user from group

Удаляет пользователя из группы.

**Запрос:**

* **Method:** DELETE
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/group/{groupId:int}
* **URL параметры:**
  * **\{ userId:string }** - идентификатор пользователя;
  * **\{ groupId:int }** - идентификатор группы;

**Пример**: https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/group/57

**Ответ:**

* **Тело ответа**:
``` json

```
### Add user to presentation

Предоставляет пользователю доступ к презентации.

**Запрос:**

* **Method:** PUT
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/presentation/{presentationId:int}
* **URL параметры:**
  * **\{ userId:string }** - идентификатор пользователя;
  * **\{ presentationId:int }** - идентификатор презентации;

**Пример**: https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/presentation/57

**Ответ:**

* **Тело ответа**:
``` json

```

### Add User To Presentations

Открывает пользователю доступ к группе презентаций. Группа презентаций должна представлять из себя коллекцию идентификаторов презентаций. Презентации должны пренадлежать текущему клиенту и быть активны. Пользователь не должен принадлежать ролям "Аккунт менеджер" и "Проджект менеджер". Открывая доступ пользователю к группе презентаций, доступ будет открыт только к тем презентациям, которые удовлетворяют выше перечисленным условиям. В результате будет возвращен список всех презентаций, к которым имеет доступ пользователь. Используя этот список, можно проверить к каким презентациям был открыт доступ пользователю.

**Запрос:**

* **Method**: POST
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/users/{userId}/presentations
* **URL параметры**:
  * **\{ userId:int }** - идентификатор пользователя;

**Тело запроса:**
``` json
[
	33,
	26,
	24
]
```
**Пример**: https://api.storyclm.com/v1/users/b1ae249b-22c4-4b0b-a9ec-66f0521a4715/presentations

**Пример ответа:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:

```JSON
[
  24,
  26,
  33
]
```
### Remove user from presentation

Лишает пользователя доступа к презентации.

**Запрос:**

* **Method:** DELETE
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/presentation/{presentationId:int}
* **URL параметры:**
  * **\{ userId:string }** - идентификатор пользователя;
  * **\{ presentationId:int }** - идентификатор презентации;

**Пример**: https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/presentation/57

**Ответ:**

* **Тело ответа**:
``` json

```
### Remove User From Presentations

Лишает пользователя доступа к группе презентаций. Группа презентаций должна представлять из себя коллекцию идентификаторов презентаций. Презентации должны пренадлежать текущему клиенту и быть активны. Пользователь не должен принадлежать ролям "Аккунт менеджер" и "Проджект менеджер". В результате будет возвращен список всех презентаций, к которым имеет доступ пользователь.

**Запрос:**

* **Method**: DELETE
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/users/{userId}/presentations?ids={presentationId}&ids={presentationId}&ids={presentationId}
* **URL параметры**:
  * **\{ presentationId:int }** - идентификатор презентации;
  * **\{ userId:string }** - идентификатор пользователя;

**Пример**: https://api.storyclm.com/v1/users/b1ae249b-22c4-4b0b-a9ec-66f0521a4715/presentations?ids=24&ids=26&ids=33

**Пример ответа:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:

```JSON
[]
```
### Synchronize Presentations For User

Предоставлет доступ пользователю к группе презентаций. Группа презентаций должна представлять из себя коллекцию идентификаторов презентаций. Независимо от того к ками презентациям имел доступ пользователь до синхронизации, после синхронизации он будет иметь доступ только к тем презентациям, которые есть в списке. Презентации должны пренадлежать текущему клиенту и быть активны. Пользователь не должен принадлежать ролям "Аккунт менеджер" и "Проджект менеджер". В результате будет возвращен список всех презентаций, к которым имеет доступ пользователь.

**Запрос:**

* **Method**: PUT
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/users/{userId}/presentations
* **URL параметры**:
  * **\{ presentationId:int }** - идентификатор презентации;

**Тело запроса:**
``` json
[
  24,
  33
]
```
**Пример**: https://api.storyclm.com/v1/users/b1ae249b-22c4-4b0b-a9ec-66f0521a4715/presentations

**Пример ответа:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:

```JSON
[
  24,
  33
]
```
### Presentations

Возвращает список презентаций доступ к которым имеет пользователь.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/presentations
* **URL параметры:**
  * **\{ userId:string }** - идентификатор пользователя;

**Пример**: https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/presentations

**Ответ:**

* **Тело ответа**:
``` json
[
  {
    "id": 32,
    "name": "Как улучшить качество жизни при хрони\u00adческой обструк\u00adтивной болезни легких"
  }
]
```

### Groups

Возвращает список групп членом которых является пользователь.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/groups
* **URL параметры:**
  * **\{ userId:string }** - идентификатор пользователя;

**Пример**: https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/groups

**Ответ:**

* **Тело ответа**:
``` json
[
  {
    "id": 57,
    "name": "Группа3"
  }
]
```
