## ⚪ ️ 2.5 Измерение и рефакторинг с использованием инструментов статического анализа

✅ **Делаем:**

Using static analysis tools helps by giving objective ways to improve code quality and keep your code maintainable. You can add static analysis tools to your CI build to abort when it finds code smells. Its main selling points over plain linting are the ability to inspect quality in the context of multiple files (e.g. detect duplications), perform advanced analysis (e.g. code complexity) and follow the history and progress of code issues. Two examples of tools you can use are [Sonarqube](https://www.sonarqube.org/) (2,600+ [stars](https://github.com/SonarSource/sonarqube)) and [Code Climate](https://codeclimate.com/) (1,500+ [stars](https://github.com/codeclimate/codeclimate))

Инструменты статического анализа это хороший способ улучшить качество кода и сделать его более легко поддерживаевым. Ты можешь добавить их в свою CI-сборку, чтобы она автоматически прерывалась в случае обнаружения "попахивающего кода".

Основные преимущества по сравнению с простым линтингом - это возможность проверять качество в контексте нескольких файлов (например, обнаруживать дубликаты), выполнять расширенный анализ (например, сложность кода) и отслеживать историю и прогресс проблем с кодом.

Пара примеров инструментов которые ты можешь использовать [Sonarqube](https://www.sonarqube.org/) (2,600+ [stars](https://github.com/SonarSource/sonarqube)) и [Code Climate](https://codeclimate.com/) (1,500+ [stars](https://github.com/codeclimate/codeclimate))

Благодарность:: <a href="https://github.com/TheHollidayInn" data-href="https://github.com/TheHollidayInn" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Keith Holliday](https://github.com/TheHollidayInn)</a>

<br/>

❌ **Иначе:** При низком качестве кода ошибки и производительность всегда будут проблемой, которую не может исправить ни одна новая библиотека, ни самые современные код-фичи.

<br/>

<details><summary>✏ <b>Пример кода</b></summary>

<br/>

### 👏 Правильно: CodeClimate, коммерческий инструмент, который может идентифицировать сложные методы:

![](https://img.shields.io/badge/🔧%20Example%20using%20Code%20Climate-blue.svg "Examples with CodeClimate")

![alt text](assets/bp-16-yoni-goldberg-quality.png " CodeClimat, a commercial tool that can identify complex methods:")

</details>
