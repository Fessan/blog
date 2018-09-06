**[WIP]**

state-manager - STM

стейт-менеджер - СТМ

#### Журнал

* В редаксе много бойлерплейта
* Редакс медленно работает
* Приходится мемоизировать селекторы - еще больше бойлерплейта
* Почему нельзя описывать редьюсер и селектор одной сущностью?
* coach-stm
* стм - observable?
* редакс - фреймворк?
* как описывать взаимосвязи между узлами дерева (состояния)?
* пути
* курсоры
* атомы - как агрегаторы манипуляций над курсором к узлам
* что такое стм?
* дети и родители узла - те же подписчики.
* стримы - как надстройка бизнес-логики над атомами
* взаимосвязь между стримами - сложно-понимаемый граф (Дима пытается его разложить автоматически)
* подписки в стиле КА с помощью патерн-матчинга
* группировка подписчиков для ручного выделения этапов влияния данных на приложение
* стм - фреймворк бизнес-логики.

####

Ключевая задача менеджеров состояния - это observable data ("обозреваемые данные"), т.е. возможность следить за изменениями в какой-то структуре - стейте (state).

Основные проблемы возникают с (в погоне за лучшим API и выводом типов):
1. Установка новых значений в точечных частях стейта
2. Обновление подписчиков на точечные части стейта

[2] Часто стейт описывают как статическую модель, но при этом в приложении всегда используются динамические производные (computed value) от данных модели. Т.е. динамические производные - это проекция статической модели через призму бизнес-логики. Фундаментально, подходы по выводу динамических производных могут отличаться и реализовываться следующими способами:
  1. [*redux*] Производить обновление модели, т.е. стейта, производить оповещение подписчиков, на каждом подписчике вычислять производные данные индивидуально.
  2. [*effector*] Производить обновление модели, т.е. стейта, производить вычисления производных данных, оповещать подписчиков.
  3. [*pathon*] Производить обновление модели, вычислять производные данные, класть их вместе в стейт, производить оповещение подписчиков.
  
Главная сложность, при этом, заключается в минимизации производимых вычислений и уведомлении только тех подписчиков, для которых данные поменялись.