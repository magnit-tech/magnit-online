О проекте Magnit iOS и используемых технологиях

### Весрия iOS
Приложение поддерживает минимальную iOS 12.

### Архитектура
В качестве используемого подхода к архитектуре приложения используется **CleanSwift**, где в основе presentation слоя лежит VIP (View-Interactor-Presenter). На русском можно ознакомиться [здесь](https://habr.com/ru/post/415725/).

### UI
В основе UI - **UIKit**. Для иерархий для экранов форм используется подход с CVC (Child View Controller), где каждая часть представлена в виде секции и помещена в UIStackView. Экраны-списки реализованы классическим путём с определением делегатов на уровне ViewController без менеджера для tableView/collectionView. Вёрстка осуществляется через xib-файлы с пост-настройкой стиля, констрейнтов и пр. в коде.

### Ветвление
Парадигма к подходу разработки - **gitflow**, с фиче-ветками, обязательным код-ревью.

### Ассеты
Особенности работы с ассетами. Если ассет экспортируем в векторный формат (svg), то такие ассеты добавляются в доску на **PaintCode** и экспортируются в StyleKit.swift файл в код репозитория. При отказе от iOS 12 сможем работать с svg нативно уже без **PaintCode**. Добавление новых ассетов происходит через ветку *assets*, и потом в фиче-ветку, ввиду того, что мерж-конфликты нерешабельны при параллельном добавлении ассетов в разные ветки.

### CI / CD
В качестве CI используется **Travis**.
Для сборок используется **fastlane**, в корне проекта есть папка со всеми конфигами.

### Тестирование
Для Unit-тестирования используется связка **Quick** & **Nimble** для декларативного описания тестов. **Sourcery** используетя для генерации mock-объектов. В небольшом количестве имеются некоторые UI-тесты, что реализованы с помощью **Robot pattern testing**.

### Локализация
В приложении используется русская и английская локализация. Процесс локализации осуществляется централизованно с помощью иснтурмента **POEditor**. После добавления новых локализованных строчек в проекте в POEditor нужно выполнить скрипт из репозитория и добавить полученные локализованные тексты в репозиторий.

### Работа с сетью
Для работы с сетью в основе лежит **Alamofire**, поверх которого есть обертка в виде APIClient с generics под ответ/запрос. Коммуникация между backend и frontend используется Swagger first approach, где backend предоставляет swagger.yaml, а frontend генериурет networking слой. Для генерации кода на Swift используется утилита **[SwagGen](https://github.com/yonaskolb/SwagGen)** с кастомным набором шаблонов.

### Зависимости

Зависимости устанавливаются через Cocoapods. Текущий список зависимостей таков:

> * pod 'Alamofire', '5.3.0'
> * pod 'AlamofireNetworkActivityIndicator', '3.1'
> * pod 'Cache'
> * pod 'Dip', '7.1.1'
> * pod 'Firebase/Analytics' # No specific version specified, as recommended by Firebase
> * pod 'Firebase/Crashlytics'
> * pod 'Firebase/Messaging'
> * pod 'KeychainAccess', '4.2.0'
> * pod 'Kingfisher', '5.14.0'
> * pod 'Locksmith', '4.0.0'
> * pod 'lottie-ios', '3.1.8'
> * pod 'MarkdownKit', '1.6'
> * pod 'OneTimePassword', '3.2.0'
> * pod 'SexyTooltip', '1.2.7'
> * pod 'SkeletonView', '1.10.0'
> * pod 'SnapKit', '5.0.1'
> * pod 'SwiftLint', '0.40.3'
> * pod 'YandexMobileAds/Dynamic', '2.16.0'
> * pod 'YandexMobileMetrica/Dynamic/Core', '3.12.0'
> * pod 'SwiftJWT'

> * // UI Testing
> * pod 'SBTUITestTunnelServer', '6.3.0', :configuration => ['Debug']
> * pod 'GCDWebServer', '3.5.4', :configuration => ['Debug']
> * pod 'SBTUITestTunnelCommon', '6.3.0', :configuration => ['Debug']


Решения о возможности внесения новых библиотек в проект должны приниматься коллегиально.
