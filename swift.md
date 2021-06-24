О проекте Magnit iOS и используемых технологиях

### Весрия iOS
Приложение поддерживает минимальную iOS 12.

### Архитектура
В качестве используемого подхода к архитектуре приложения используется **CleanSwift**, где в основе presentation слоя лежит VIP (View-Interactor-Presenter). На русском можно ознакомиться [здесь](https://habr.com/ru/post/415725/).

### UI
В основе UI - **UIKit**. Для иерархий для экранов форм используется подход с CVC (Child View Controller), где каждая часть представлена в виде секции и помещена в UIStackView. Экраны-списки реализованы классическим путём с определением делегатов на уровне ViewController без менеджера для tableView/collectionView. Вёрстка осуществляется через xib-файлы с пост-настройкой стиля, констрейнтов и пр. в коде.

### Ассеты
Особенности работы с ассетами. Если ассет экспортируем в векторный формат (svg), то такие ассеты добавляются в доску на **PaintCode** и экспортируются в StyleKit.swift файл в код репозитория. При отказе от iOS 12 сможем работать с svg нативно уже без **PaintCode**. Добавление новых ассетов происходит через ветку *assets*, и потом в фиче-ветку, ввиду того, что мерж-конфликты нерешабельны при параллельном добавлении ассетов в разные ветки.

### Локализация
В приложении используется русская и английская локализация. Процесс локализации осуществляется централизованно с помощью инструмента **POEditor**. После добавления новых локализованных строчек в проекте в POEditor нужно выполнить скрипт updateStrings из папки [scripts](https://github.com/magnit-tech/magnit-ios/tree/develop/scripts) и добавить полученные локализованные тексты в репозиторий.

### Работа с сетью
Для работы с сетью в основе лежит **Alamofire**, поверх которого есть обертка в виде APIClient с generics под ответ/запрос. Коммуникация между backend и frontend используется Swagger first approach, где backend предоставляет swagger.yaml, а frontend генериурет networking слой. Для генерации кода на Swift используется утилита **[SwagGen](https://github.com/yonaskolb/SwagGen)** с кастомным набором шаблонов.
Запуск генерации так же происходит поспредством вызова скриптов updateNetworkLayer, updatePostmanMocks из папки [scripts](https://github.com/magnit-tech/magnit-ios/tree/develop/scripts)

### Тестирование
Для Unit-тестирования используется связка **Quick** & **Nimble** для декларативного описания тестов. **Sourcery** используетя для генерации mock-объектов. В небольшом количестве имеются некоторые UI-тесты, что реализованы с помощью **Robot pattern testing**.

### Ветвление
Парадигма к подходу разработки - **gitflow**, с фиче-ветками, обязательным код-ревью.

### CI / CD
В качестве CI используется **GitHub Actions**.
Для сборок используется **fastlane**, в корне проекта есть [папка](https://github.com/magnit-tech/magnit-ios/tree/develop/fastlane) со всеми конфигами.
Скрипт запуска fastlane лежит в папке [scripts](https://github.com/magnit-tech/magnit-ios/tree/develop/scripts).

### Зависимости

Зависимости устанавливаются через Cocoapods. Текущий список зависимостей таков:

> * pod 'Alamofire', '5.3.0' # Работа с сетью
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

> * // UI Testing
> * pod 'SBTUITestTunnelServer', '6.3.0', :configuration => ['Debug']
> * pod 'GCDWebServer', '3.5.4', :configuration => ['Debug']
> * pod 'SBTUITestTunnelCommon', '6.3.0', :configuration => ['Debug']


Решения о возможности внесения новых библиотек в проект должны приниматься коллегиально.
