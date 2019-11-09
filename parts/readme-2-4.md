## ⚪ ️ 2.4 Тестируй миддлвары изолированно

✅ **Делаем:**

Миддлвары не тестируют потому что они являются малой частью системы и требуют работающего экспресс-сервера. Обе причины ошибочны - миддлвары влияют на все или на большинство запросов и могуть быть легко протестированы как чистые функции, которые получают объекты {req, res}.

Чтобы протестировать функцию-миддлвар, нужно вызвать ее и отслеживать через шпионы ([используя, например, Sinon](https://www.npmjs.com/package/sinon)) её взаимодействией с объектами {req, res}, чтобы убедиться, что функция правильно отработала.

Библиотека [node-mock-http](https://www.npmjs.com/package/node-mocks-http) идёт ещё дальше и предоставляет конструкторы для создания объяектов {req, res} и следит за их поведением.

`node-mock-http` может проверить, соответствует ли установленный http status для объекта res, ожиданиям (см. Пример ниже)

<br/>

❌ **Иначе:** Баг в Express-миддлваре === баг в большинстве запросов

<br/>

<details><summary>✏ <b>Пример кода</b></summary>

<br/>

### 👏 Правильно: Тестирование миддлвара в отдельности без сетевых вызовов и поднятия Express-сервера

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
//миддлвара, которую хотим протестировать
const unitUnderTest = require("./middleware");
const httpMocks = require("node-mocks-http");
//Jest синтаксис, эквивалентный describe() и it() в Mocha
test("Запрос без авторизационного заголовка должен вернуть 403 статус", () => {
  const request = httpMocks.createRequest({
    method: "GET",
    url: "/user/42",
    headers: {
      authentication: ""
    }
  });
  const response = httpMocks.createResponse();
  unitUnderTest(request, response);
  expect(response.statusCode).toBe(403);
});
```

</details>

<br/><br/>
