## ⚪ ️ 3.1. Отделяй UI от функциональности

✅ **Делаем:** Детали пользовательского интерфейса это помеха при тестировании логики компонентов. Получаем из разметки нужные для тестирования данные абстрактным способом, не слишком связанным с графической реализацией. Пишем утверждения тестов только на чистых данных (туда не должны попадать HTML / CSS) и отключем анимацию, которая может замедлять выполнение тестов. Может возникнуть соблазн избежать рендеринга и тестировать "бэк-часть" пользовательского интерфейса (например, сервисы, экшоны, состояние стора), но это приведет к фейковым тестам, которые не похожи на реальность и не выявят случаев, когда правильные данные даже не доходят до в пользовательского интерфейса.

<br/>

❌ **Иначе:** Чистые вычисленные данные теста могут быть готовы через 10 мс, но весь тест будет длиться 500 мс (100 тестов = 1 мин) из-за модной но ненужной в данном случае анимации.

<br/>

<details><summary>✏ <b>Пример кода</b></summary>

<br/>

### 👏 Правильно: Отделяем данные от деталей UI-реализации

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Examples with React") ![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Examples with react-testing-library")

```javascript
test("Когда у списка юзеров выставлен флаг показа только VIP, дожны отрисоваться только VIP юзеры", () => {
  // Состояние
  const allUsers = [
    { id: 1, name: "Yoni Goldberg", vip: false },
    { id: 2, name: "John Doe", vip: true }
  ];

  // Действие
  const { getAllByTestId } = render(
    <UsersList users={allUsers} showOnlyVIP={true} />
  );

  // Утверждение - сначала вытаскиваем из разметки необходимые данные для теста
  const allRenderedUsers = getAllByTestId("user").map(
    uiElement => uiElement.textContent
  );
  const allRealVIPUsers = allUsers
    .filter(user => user.vip)
    .map(user => user.name);
  expect(allRenderedUsers).toEqual(allRealVIPUsers); //сравниваем данные с данными, детали разметки не важны
});
```

<br/>

### 👎 Неправильно: В тесте смешались данные и представление

```javascript
test("Когда у списка юзеров выставлен флаг показа только VIP, дожны отрисоваться только VIP юзеры", () => {
  // Состояние
  const allUsers = [
    { id: 1, name: "Yoni Goldberg", vip: false },
    { id: 2, name: "John Doe", vip: true }
  ];

  // Действие
  const { getAllByTestId } = render(
    <UsersList users={allUsers} showOnlyVIP={true} />
  );

  // Утверждение - смешали UI и данные
  expect(getAllByTestId("user")).toEqual(
    '[<li data-testid="user">John Doe</li>]'
  );
});
```

</details>

<br/><br/>
