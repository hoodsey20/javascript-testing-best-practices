## ⚪ ️ 3.4 Используй фреймворки со встроенной поддержкой асинхронных события, откажись от setTimeOut.

✅ **Делаем:** Во многих случаях точное время выполнения юнит-теста не известно(например, анимация приостанавливает появление элемента) - в таком случае вместо использования setTimeOut отдавай предпочтение специальным методам, которые предоставляются большинством платформ для тестирования. Некоторые библиотеки дают возможность дождаться окончания операции (например [Cypress cy.request('url')](https://docs.cypress.io/guides/references/best-practices.html#Unnecessary-Waiting)), другие предоставляют API для работы с асинхронными действиями как [@testing-library/dom method wait(expect(element))](https://testing-library.com/docs/guide-disappearance).

Подчас, более элегантным решением будет использовать заглушку (stub) вместо обращения к медленном API, и затем, когда момент отклика становится точно известен, компонент может быть явно перерисован.

Когда тестируемый компонент зависит от другого, который использует внутри себя setTimeOut, может быть ползным [ускорить время](https://jestjs.io/docs/en/timer-mocks). Стоит избегать использования setTimeOut, потому что это делает твои тесты медленные или слишком рискованными (когда мы можем выставить слишком корроткое время таймера и не дождаться нужного нам события).

Всякий раз, когда setTimeOut и опрос (polling) неизбежны, и нет никакой поддержки со стороны инфраструктуры тестирования, некоторые библиотеки npm, такие как [wait-for-expect](https://www.npmjs.com/package/wait-for-expect) могут предоставить решения с большей определенностью.
<br/>

❌ **Иначе:** При использовании честного setTimeOut тесты будут на порядок медленнее. При попытке выставить setTimeOut на слишком короткое время тест может быть провален, если тестируемое устройство не ответило своевременно. Так что подход с использованием setTimeOut сводится к компромиссу между нестабильностью и плохой работой.

<br/>

<details><summary>✏ <b>Пример кода</b></summary>

<br/>

### 👏 Правильно: E2E API которое выполняется только после того как асинхронная операция была выполнена (Cypress)

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Examples with React") ![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Examples with react-testing-library")

```javascript
// используем Cypress
cy.get("#show-products").click(); // переходим к продуктам
cy.wait("@products"); // ждём пока нужны роут подгрузится
// код на этой строчке начнёт выполнятся только после того как загрузится роут
```

### 👏 Правильно: Библиотека для тестирования которая ждёт появленя необходимых DOM элементов

```javascript
// @testing-library/dom
test("movie title appears", async () => {
  // изначально нужного элемента ещё нет

  // ждём пока появится
  await wait(() => {
    expect(getByText("the lion king")).toBeInTheDocument();
  });

  // дожидаемся появления и возвращаем результат
  const movie = await waitForElement(() => getByText("the lion king"));
});
```

### 👎 Неправильно: кастомный код с ожиданием события

```javascript
test("movie title appears", async () => {
  // изначально нужного элемента ещё нет

  // кастомная логика ожидания появления
  const interval = setInterval(() => {
    const found = getByText("the lion king");
    if (found) {
      clearInterval(interval);
      expect(getByText("the lion king")).toBeInTheDocument();
    }
  }, 100);

  // дожидаемся появления и возвращаем результат
  const movie = await waitForElement(() => getByText("the lion king"));
});
```

</details>

<br/>
