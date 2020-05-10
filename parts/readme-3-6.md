## ⚪ ️ 3.6 Делаем заглушки для нестабильных и медленных ресурсов таких как бэкенд API

✅ **Делаем:** Во время написания основных тестов (не E2E), избегай обращения к любым ресурсам, которые находятся вне области твоего контроля и ответственности, таких как бэкенд API, и используй заглушки (stubs) вместо них. Вместо совершения реальных вызовов API используй какие-нибудь библиотеки для подмены ответов API (например [Sinon](https://sinonjs.org/), [Test doubles](https://www.npmjs.com/package/testdouble), и другие). Главное преимущество такого подхода — значительное снижение непредсказуемости: тестовый или стейджинговые API по своему определению являются не очень стабильными и будут время от времени класть твои тесты не смотря на то, что ТВОИ компоненты ведут себя правильно (продакшн-окружение бэкенда не предназначено для тестирования и обычно использует ограничения для количества и частоты запросов).

Использование заглушек для API позволит имитировать различные сценарии ответов, которые должны управлять поведением вашего компонента, например, когда данные не были найдены или когда API выдает ошибку. И последнее, но не менее важное: сетевые вызовы значительно замедляют тестирование.

<br/>

❌ **Иначе:** Средний тест выполняется не более нескольких мс, типичный вызов API - как минимум 100 мс>, что делает каждый тест примерно в 20 раз медленнее

<br/>

<details><summary>✏ <b>Пример кода</b></summary>

<br/>

### 👏 Правильно: Заглушка или перехват обращение к API

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Examples with React") ![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with react-testing-library")

```javascript
// тестируемый компонент
export default function ProductsList() {
  const [products, setProducts] = useState(false);

  const fetchProducts = async () => {
    const products = await axios.get("api/products");
    setProducts(products);
  };

  useEffect(() => {
    fetchProducts();
  }, []);

  return products ? (
    <div>{products}</div>
  ) : (
    <div data-testid="no-products-message">Нет товаров</div>
  );
}

// тест
test("When no products exist, show the appropriate message", () => {
  // Состояние
  nock("api").get(`/products`).reply(404);

  // Действие
  const { getByTestId } = render(<ProductsList />);

  // Утверждение
  expect(getByTestId("no-products-message")).toBeTruthy();
});
```

</details>

<br/>
