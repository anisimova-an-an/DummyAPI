# DummyAPI

В данном документе представлено описание тестирования проекта DummyAPI

## Оглавление
1. [Описание проекта](#описание-проекта)
2. [Объект тестирования](#post)
   - [GET /post (Get List)](#get-post-get-list)
   - [POST /post/create (Create Post)](#post-postcreate-create-post)
3. [Майнд-карта](#майнд-карта)
4. [Коллекция POSTMAN](#коллекция-postman)
5. [Автотесты](#автотесты)
   
## Описание проекта

DummyAPI (https://dummyapi.io/) является сервисом для тестирования API. Для выполнения каждого запроса необходим app-id, который можно получить при регистрации на сайте и передать через хедер.
В качестве тестирования взят объект **Post**

### POST
_____
#### GET /post (Get List)
Позволяет получить список постов, отсортированных по дате создания.
- Доступен параметр для вывода определенной страницы.
- Доступен параметр для отображения определенного числа публикаций на странице.
- Доступен параметр для отображения публикаций, созданных в текущей среде (исключая базовые элементы).

**Response Body:**

**List**
```javascript
{
data: Array(Model)
total: number(total items in DB)
page: number(current page)
limit: number(number of items on page)
}
```
**Post Preview**
```javascript
{
id: string(autogenerated)
text: string(length: 6-50, preview only)
image: string(url)
likes: number(init value: 0)
tags: array(string)
publishDate: string(autogenerated)
owner: object(User Preview)
}
```
_____
#### POST /post/create (Create Post)
Позволяет создать новую публикацию, возвращает созданные данные записи.

**Request Body:**

**Post Create**
```javascript
{
text: string(length: 6-50, preview only)
image: string(url)
likes: number(init value: 0)
tags: array(string)
owner: string(User id)
}
```
**Response Body:**

**Post Preview**
```javascript
{
id: string(autogenerated)
text: string(length: 6-50, preview only)
image: string(url)
likes: number(init value: 0)
tags: array(string)
publishDate: string(autogenerated)
owner: object(User Preview)
}
```
**User Preview**
```javascript
{
id: string(autogenerated)
title: string("mr", "ms", "mrs", "miss", "dr", "")
firstName: string(length: 2-50)
lastName: string(length: 2-50)
picture: string(url)
}
```

## Майнд-карта
Майнд-карта представляет собой набор проверок для тестирования объекта **Post**. Подробные проверки расписаны для **Get List** и **Create Post**. Майнд-карту можно [скачать](https://github.com/anisimova-an-an/DummyAPI/blob/main/Майнд-карта.png)

_Майнд-карта для **Get List**_ 
![Alt-текст](https://github.com/anisimova-an-an/DummyAPI/blob/main/GetList.png "МК")

_Майнд-карта для **Create Post**_ 
![Alt-текст](https://github.com/anisimova-an-an/DummyAPI/blob/main/CreatePost.png "МК")

## Коллекция POSTMAN
На основе майнд-карты была составлена коллекция запросов в POSTMAN:
- [Ссылка на коллекцию](https://github.com/anisimova-an-an/DummyAPI/blob/main/Публикации.postman_collection.json)
- [Ссылка на окружение](https://github.com/anisimova-an-an/DummyAPI/blob/main/DummyAPI.postman_environment.json)

## Автотесты

Часть тестов коллекции была автоматизирована. Для этого была сформированна цепочка последовательных проверок:
1. Получение списка всех публикаций
2. Создание публикации (в результате этого теста создавалась переменная PostID, которая использовалась в остальных тестах)
3. Просмотр поста по ID
4. Внесение изменений в пост
5. Удаление поста
6. Просмотр ранее удаленного поста

В результате были созданы автотесты на проверку:
- Статус код ответа
- Допустимое время загрузки страницы
- Типы данных значений ключей
- Значения ключей
- Допустимое количество объектов в массиве

- [Ссылка на коллекцию автотестов](https://github.com/anisimova-an-an/DummyAPI/blob/main/Automatization.postman_collection.json)
- [Ссылка на окружение](https://github.com/anisimova-an-an/DummyAPI/blob/main/DummyAPI.postman_environment%20(1).json)

