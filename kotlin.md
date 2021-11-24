## Описание приложения Magnit Android. Стек технологий.

### Версия Android
Приложение поддерживает минимальную версию Android SDK 23 (6.0)

### Стек технологий
- **Kotlin** основной язык разработки
- **Kotlin Coroutines** для фоновых операций и асинхронных задач
- **Navigation Component** и **single activity** для навигации
- **Retrofit** для сетевых запросов
- **Dagger2** для dependency injection
- **Kotlin Gradle DSL** для конфигурации сборки проекта
- **Moshi** для парсинга json
- **ViewBinding** для биндинга данных на view
- **jUnit 4** для unit тестирования
- **Espresso** и **mockserver** для instrumentation testing
- **FCM** для работы с push уведомлениями
- **Yandex AppMetrica** для сбора аналитических данных
- **Fastlane** для сборки проекта на базе GitLab CI/CD

### Архитектура
Проект следует принципам Uncle Bob's Clean Architecture и состоит из трех слоёв:
1. Presentation
2. Domain
3. Data

В качестве архитектурного паттерна проектирования используется [MVVM (Model-View-ViewModel)](https://ru.wikipedia.org/wiki/Model-View-ViewModel).

### Modules
В проекте используется многомодульный подход. Здесь можно выделить основные:
- App-модуль — связывает в себе все модули и имеет зависимости на Feature-модули и Core.
- Core-модуль — содержит вспомогательный код, необходимый для нескольких Feature-модулей. Это могут быть полезные обертки над используемыми библиотеками, общие компоненты presentation слоя, расширения или иные утилиты. Core-модуль ни от кого не зависит.
- Feature-модуль — модуль, содержащий конкретную фичу, изолированную от остальных в соответствии с бизнес-логикой. В общем случае он включает в себя presentation слой, DI и иные специфичные модулю данные. Feature-модуль имеет зависимость на Core-модуль.

### Feature toggles
При разработке нового функционала приложения используются toggles, управлять которыми можно как локально, так и server side, что дает дополнительную гибкость, стабильность и безопасность интеграции новых фич в проект.

### Локализация
Приложение на текущий момент может поддерживать две локализации - русскую и английскую. Процесс локализации и обновления строк происходит централизованно для всех платформ, через **POEditor**. Чтоюы запустить синхронизацию и обновление строк в проекте следует выполнить python скрипт и пакета tools проекта.

### Best practises
Для поддержания чистого и легко читаемого кода следует придерживаться следующих принципов и правил:
* [Kotlin style guide #1](https://developer.android.com/kotlin/style-guide)
* [Kotlin style guide #2](https://kotlinlang.org/docs/coding-conventions.html)
* [Coroutines](https://developer.android.com/kotlin/coroutines/coroutines-best-practices?utm_source=android_broadcast_te&utm_medium=post&utm_campaign=coroutines-luchshie-)
* [StateFlow and SharedFlow](https://developer.android.com/kotlin/flow/stateflow-and-sharedflow)
* [SOLID](https://ru.wikipedia.org/wiki/SOLID_(%D0%BE%D0%B1%D1%8A%D0%B5%D0%BA%D1%82%D0%BD%D0%BE-%D0%BE%D1%80%D0%B8%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D0%B5_%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5))
* [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)
* [KISS](https://ru.wikipedia.org/wiki/KISS_(%D0%BF%D1%80%D0%B8%D0%BD%D1%86%D0%B8%D0%BF))

> В дополнение ко всему следует использовать плагин для Android Studio [Detekt plugin](https://plugins.jetbrains.com/plugin/10761-detekt), настроенный на конфиги линтера проекта.

### Git-flow
- На каждую задачу создается feature branch. Обязательные ревью, как минимум 2 approve.
- Для именования коммитов и веток используется подход [Semantic Git Commit](https://gist.github.com/joshbuchea/6f47e86d2510bce28f8e7f42ae84c716)
- Версионирование релизов происходит по спецификации [Semantic Versioning](https://semver.org/)


### Сторонние библиотеки и ресурсы
В проекте не допускается использование экспериментального api различных библиотек, SDK и средств языка, а так же их alpha и beta версий. Для некоторых beta возможны исключения, но только по согласованию со всей командой (с обоснованием такой необходимости), и только из библиотек поставляемых Android SDK и Google. Решения о возможности внесения новых библиотек в проект должны приниматься коллегиально.
