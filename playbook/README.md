# Playbook

## О чем раздел

Данный раздел должен отвечать на следующий ряд вопросов, которые могут возникнуть как у кандидата при найме так и текущему сотрудника:

* Какая у нас структура отдела?
* Какие есть команды или другие единицы орг. структуры отдела?
* Какие в отделе грейды у IT специалистов?
* Какие обязаности у инженера внутри своего грейда?
* Как повысить свой грейд?

Очень много информации было взято (скопировано) отсюда

* [avito: playbook](https://github.com/avito-tech/playbook)
* [bestdoctor: grades](https://github.com/best-doctor/grades)

## Структура отдела

### В Общем виде

![Организационная структура отдела](imgs/chart.jpeg)


### 2021

<details>
<summary>История тут</summary>

#### q1
```plantuml
@startuml

@startwbs
*[#lightskyblue] Online Department
** Retention Team
** MagnitPay Team
** DevOps Team
@endwbs
@enduml
```

#### q2

```plantuml
@startuml

@startwbs
*[#lightskyblue] Online Department
** Core&Retention Team
** MagnitPay Team
** DevOps Team
** Middleware Team
** MagnitMobile Team
@endwbs
@enduml
```

#### q3

```plantuml
@startuml

@startwbs
*[#lightskyblue] Online Department
** Core&Retention Team
** Activation&Acquisition Team
** MagnitPay Team
** DevOps Team
** Middleware Team
** MagnitMobile Team
@endwbs
@enduml
```

#### q4

```plantuml
@startuml

@startwbs
*[#lightskyblue] Online Department
** Core&Retention Team
** Activation&Acquisition Team
** MagnitPay Team
** MagnitMobile Team
** DevOps Team
** Middleware Team
** MagnitID Team
@endwbs
@enduml
```

</details>


### 2022

<details>
<summary>Планы тут</summary>

#### q1

```plantuml
@startuml

@startwbs

*[#lightskyblue] Online Department
** Retention Team
** Activation&Acquisition Team
** MagnitPay Team
** MagnitMobile Team
** DevOps Team
** Middleware Team
** MagnitID Team
** Platform Team
** ProductPromo Team

@endwbs
@enduml
```

#### q2

```plantuml
@startuml

@startwbs
*[#lightskyblue] Online Department

** MagnitPay Team
** MagnitMobile Team
** Release Team

**[#limegreen] Core Cluster
*** Core&Retention Team
*** Activation&Acquisition Team
*** Platform Team
*** ProductPromo Team
*** Web Team

**[#limegreen] Infra Cluster
*** DevOps Team
*** Middleware Team
*** MagnitID Team

@endwbs
@enduml
```

#### q3

```plantuml
@startuml

@startwbs
*[#lightskyblue] Online Department

** MagnitPay Team
** MagnitMobile Team
** Release Team
** Content Team

**[#limegreen] Core Cluster
*** Core&Retention Team
*** Activation&Acquisition Team
*** Platform Team
*** ProductPromo Team
*** Web Team

**[#limegreen] Infra Cluster
*** DevOps Team
*** Middleware Team
*** MagnitID Team

@endwbs
@enduml
```

#### q4

```plantuml
@startuml

@startwbs
*[#lightskyblue] Online Department

** MagnitPay Team
** MagnitMobile Team
** Release Team
** Content Team
** In-store Team

**[#limegreen] Core Cluster
*** Core&Retention Team
*** Activation&Acquisition Team
*** Platform Team
*** ProductPromo Team
*** Web Team

**[#limegreen] Infra Cluster
*** DevOps Team
*** Middleware Team
*** MagnitID Team

@endwbs
@enduml
```

</details>

## Наши Грейды

Изначально есть [гигиенический минимум](grades/minimum.md) которому должен соответствовать кандидат.

* [Junior](grades/junior.md)
    * [iOS](grades/ios/junior.md)
    * [Android](grades/android/junior.md)
    * [Golang](grades/golang/junior.md)
    * [Python](grades/python/junior.md)
* [Middle](grades/middle.md)
    * [iOS](grades/ios/middle.md)
    * [Android](grades/android/middle.md)
    * [Golang](grades/golang/middle.md)
    * [Python](grades/python/middle.md)
* [Senior](grades/senior.md)
    * [iOS](grades/ios/senior.md)
    * [Android](grades/android/senior.md)
    * [Golang](grades/golang/senior.md)
    * [Python](grades/python/senior.md)
* [TechLead](grades/techlead.md)
    * [iOS](grades/ios/techlead.md)
    * [Android](grades/android/techlead.md)
    * [Golang](grades/golang/techlead.md)
    * [Python](grades/python/techlead.md)
* [TeamLead](grades/teamlead.md)
* [ClusterLead](grades/clusterlead.md)

## Алгоритм роста грейдов

```plantuml
@startuml

start

:Junior;
:Middle;
:Senior;

if (Хочешь управлять командой?) then (да)
    : TeamLead;
    note left: управляет людьми
    :ClusterLead;
    note right: управляет большим блоком разработки, где в блоке n команд
    :HeadOfIT;
    note right: управляет отделом разработки, где в отделе n блоков и m команд
else (нет)
    :TechLead;
    note right: управляет архитектурой внутри своей предметной области
    :Architect;
    note right: управляет верхнеуровневой архитектурой
endif

stop
@enduml
```
