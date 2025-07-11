О проекте Magnit iOS и используемых технологиях

## Версия iOS

Приложение поддерживает минимальную iOS 14.0.

## Настройка окружения

Необходимо установить зависимости
[brew](https://brew.sh)
[rvm](https://rvm.io/rvm/install)
Склонировать репозиторий, открыть в директорию проекта и выполнить следующие команды
`tuist install`
`tuist generate`

## Архитектура

В качестве используемого подхода к архитектуре приложения используется **CleanSwift**, где в основе presentation слоя лежит VIP (View-Interactor-Presenter). На русском можно ознакомиться [здесь](https://habr.com/ru/post/415725/).
Так же некоторая часть модулей поддерживает архитектуру Ribs, ознакомиться можно [здесь](https://github.com/uber/RIBs).

### Структура проекта

Основными директориями в проекте являются
* Assets - директория для различных видов ассетов
* Bootstrap - директория для базовых настроек проекта (Application, AppDelegate, etc)
* Core - директория для инфраструктурных сущностей, которые затрагивают весь проект, а так же для расширений (extensions)
* Debug - директория для всех сущностей, касаются фичей на стадии разработки: дебаг меню, dev toggles, etc
* Localization - директория для локализированных строк и обертки для работы с локализированными строками
* Modules - часть DI структуры, здесь собраны сервисы, которые используются как зависимости в других сущностях приложения
* Networking - директория для обертки вокруг работы с сетью
* Scenes - директория с экранами приложения и бизнес-логикой для них, согласно **CleanSwift**
* Sections - директория с секциями экранов "мой магнит" и "магнит сегодня"

### DI

В проекте используется в качестве DI зависимость DIP.
В [ModuleCenter](https://gitlab.com/magnit-online-services/app-loyalty/mobile/ios/-/blob/develop/Magnit/Modules/ModuleCenter.swift) регистрируются зависимости.
Из ModuleCenter зависимости забираются посредством метода `getModule`, который возвращает Optional, это сделано в угоду безопасности.

## UI

В основе UI - **UIKit**. Для иерархий для экранов форм используется подход с CVC (Child View Controller), где каждая часть представлена в виде секции и помещена в UIStackView. Экраны-списки реализованы классическим путём с определением делегатов на уровне ViewController без менеджера для tableView/collectionView. Раньше вёрстка осуществлялась через xib-файлы с пост-настройкой стиля, констрейнтов и пр. в коде, но сейчас такой подход больше не используется, по возможности верстку всех экранов переносим в код при помощи **AutoLayout** + **Constraints**

### Ассеты

В качестве ассетов (изображений) используются экспортируемые из Figma ассеты в векторном формате SVG. Именование происходит с префиксом в зависимости от назначения изображений - "ic_" иконки, "bg_" фоновые картинки, "img_" картинки общего назначения.

## Дизайн-система

В командах было принято за стандарт использовать все поступающие от дизайна элементы, цвета, отступы, шрифты и пр. из единого источника правды для композиции пользовательского интерфейса - это дизайн система. Обновляется и дополняется в отдельном [репозитории](https://gitlab.com/magnit-online-services/app-loyalty/mobile/design-system-ios), а поставляется в проект через pod.

## Локализация
В приложении используется русская и английская локализация. Процесс локализации осуществляется централизованно с помощью инструмента **POEditor**. После добавления новых локализованных строчек в проекте в POEditor нужно выполнить скрипт **updateStrings** из папки [scripts](https://gitlab.com/magnit-online-services/app-loyalty/mobile/ios/-/tree/develop/scripts) и добавить полученные локализованные тексты в репозиторий.

## Работа с сетью

Для работы с сетью в основе лежит **Alamofire**, поверх которого есть обертка в виде собственного [APIClient](https://gitlab.com/magnit-online-services/app-loyalty/mobile/ios/-/blob/develop/Magnit/Networking/Magnit/APIClient.swift) с generics под ответ/запрос. Для коммуникации между backend и frontend используется Swagger first approach, где backend предоставляет swagger.yaml, а frontend генериурет networking слой. Для генерации кода на Swift используется утилита **[SwagGen](https://github.com/yonaskolb/SwagGen)** с кастомным набором шаблонов.
Запуск генерации так же происходит посредством вызова скриптов **updateNetworkLayer**, **updatePostmanMocks** из папки [scripts](https://gitlab.com/magnit-online-services/app-loyalty/mobile/ios/-/tree/develop/scripts)

## Тестирование
Для Unit-тестирования используется связка **Quick** & **Nimble** для декларативного описания тестов. **Sourcery** используетя для генерации mock-объектов. В небольшом количестве имеются некоторые UI-тесты, что реализованы с помощью **Robot pattern testing**.

## DevToggles

Для разработки используются dev toggles, которые являются enum'ом с набором фичей, которые не должны быть видны в магазинной сборке, но работа над ними ведется.
В случае, если фича зарелижена, то тоггл удаляется как из enum'a, так и из входных точек фичи удаляются проверки.
Для установки значений и использования их в коде была написана небольшая [обертка](https://gitlab.com/magnit-online-services/app-loyalty/mobile/ios/-/blob/develop/Magnit/Debug/DevToggles/GrowthService.swift)

## FeatureFlags

Сейчас более активно ведётся разработка с использованием Feature Flags - это удалённое управление состоянием фичи (вкл/выкл) с сервера. Для добавления фиче флага в приложение используется модуль [FeatureFlags](https://gitlab.com/magnit-online-services/app-loyalty/mobile/ios/-/blob/develop/Magnit/Modules/FeatureFlags/FeatureFlagsModule.swift)

## Контроль версий

Для контроля версий кода используется git.
Парадигма к подходу разработки - **gitflow**, с фиче-ветками, обязательным код-ревью.
Для прохождения ревью требуется 2 аппрува от разработчиков со статусом CODEOWNER. Ревью преследует принципы сохранения выбранной архитектуры приложения, а так же принципам SOLID, DRY, YAGNI. Так же преследуется цель сохранения выбранного стиля кода.

## CI / CD

В качестве CI используется **Gitlab Pipelines**.
Для сборок используется **fastlane**, в корне проекта есть [папка](https://gitlab.com/magnit-online-services/app-loyalty/mobile/ios/-/tree/develop/fastlane) со всеми конфигами.
Скрипт запуска fastlane лежит в папке [scripts](https://gitlab.com/magnit-online-services/app-loyalty/mobile/ios/-/tree/develop/scripts).
Сертификаты для подписи приложения лежат в отдельном репозитории в зашифрованном виде. Для облегчения работы были написаны лейны `fastlane match_retrieve_debug` и `fastlane match_retrieve_acc` для разных окружений, которые мы используем.
Если сертификаты оказались невалидны по каким либо причинам, обновить их можно используя лейны `fastlane match_update_debug` и `fastlane match_update_acc` соответственно.

### Зависимости

Зависимости устанавливаются через Cocoapods. Текущий список зависимостей таков:

> * pod 'Alamofire', '5.5.0' # Работа с сетью
> * pod 'AlamofireNetworkActivityIndicator', '3.1' # Работа с сетью (индикация)
> * pod 'Cache' # Кеширование
> * pod 'Dip', '7.1.1' # DI
> * pod 'Firebase/Analytics' # Аналитика
> * pod 'Firebase/Crashlytics' # Краш репорты
> * pod 'Firebase/Messaging' # Пуш уведомления
> * pod 'KeychainAccess', '4.2.0' # Обертка для работы с защищенным хранилищем
> * pod 'Kingfisher', '5.14.0' # Обертка для удобной загрузки и кеширования изображений
> * pod 'Locksmith', '4.0.0' # Обертка для работы с защищенным хранилищем
> * pod 'lottie-ios', '3.1.8' # Сложные анимации
> * pod 'MarkdownKit', '1.6' # Парсер MarkDown
> * pod 'OneTimePassword', '3.2.0' # Генератор OTP (используется для QR кодов)
> * pod 'SexyTooltip', '1.2.7' # Тултипы
> * pod 'SkeletonView', '1.10.0' # Используется только в клубах для создания скелета экрана
> * pod 'SnapKit', '5.0.1' # Стили шрифтов и цветов
> * pod 'SwiftLint', '0.40.3' # Статический анализатор кода
> * pod 'YandexMobileAds/Dynamic', '2.16.0' # Аналитика
> * pod 'YandexMobileMetrica/Dynamic/Core', '3.12.0' # Аналитика
> * pod 'SwiftJWT' # Работа с JWT строками
> * pod 'Wormholy' # Утилита для логирования и просмотра https запросов с устройства

> * // Приватные репозитории
> * pod 'DesignSystem', :source => 'https://github.com/magnit-tech/magnit-podspec.git' # Выше упомянутая дизайн-система

> * // Unit-тестирование
> *  pod 'Quick', '3.0.0' # Вместе с Nimble используются для декларативного описания Unit-тестов
> *  pod 'Nimble', '9.0.1' #

> * // UI Testing
> * pod 'SBTUITestTunnelServer', '6.3.0', :configuration => ['Debug']
> * pod 'GCDWebServer', '3.5.4', :configuration => ['Debug']
> * pod 'SBTUITestTunnelCommon', '6.3.0', :configuration => ['Debug']


Решения о возможности внесения новых библиотек в проект должны приниматься коллегиально.
