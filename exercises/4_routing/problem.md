# Сопоставление по образцу
В bishop каждый сервис привязан к определенному паттерну (`bishop.add(pattern, service)`). Вызываем мы действия с использованием маршрутов (`bishop.act(route, [payload])`).

В конечном итоге и паттерн, и маршрут преобразуются в объекты. Магия bishop состоит в том что он очень-очень быстро сопоставляет эти объекты и находит  совпадающие. Паттерны сопоставляются используя следующие правила:

1) паттерны с большим количеством свойств выигрывают
2) если найдено несколько подходящих паттернов с одинаковым количеством свойств - будет использован последний добавленый

# Правила наименования
Нет определенных правил по которым вы можете именовать свои маршруты/паттерны. Для простоты и унификации вы, например, можете выделять общую логику в файлы. Например, в файле `users.js` могут лежать сервисы с маршрутами `role: user, ...`, и т.п.

Как уже указывалось ранее, для наименования можно использовать как строку, так и объект. Эти сервисы идентичны: `bishop.add('role: test, cmd: echo')` и `bishop.add({ role: 'test', cmd: 'echo' })`

Кроме этого, в наименовании сервисов можно использовать регулярные выражения. Предположим, существует общий сервис авторизации пользователей `role: users, action: authentication` который принимает логин и пароль. Теперь нам нужно добавить другой способ, в котором предается токен. Вместо того чтобы править существующую логику, мы можем создать еще один сервис который будет вызываться при наличии токена: `role: users, action: authentication, token: /.*/`.

# Модификаторы маршрутов
В маршруты можно добавлять модификаторы которые либо модифицируют стандартное поведение, либо добавляют новое. Делается это с помощью добавления ключевых слов. `role: test, cmd: echo, $local: true` будет искать сервис подходящий под паттерн `role=test, cmd=echo` только в локальных паттернах. То есть, если такой сервис есть, но он находится на другом компьютере - он не будет вызван.

Некоторые из модификаторов:

* `$timeout` - указывает сколько времени в милисекундах можно выполнять сервис
* `$slow` - не вляет на выполнение, но логгирует медленные вызовы (полезно для отладки)
* `$local` - разрешает искать подходящий сервис только в локальном коде, игнорируя внешние транспорты
* `$nowait` - сообщает что сервис должен вернуть ответ об успешном получении сообщения вместо результата (например, мы выполняем долгую операцию и наша задача только убедиться в том что запрос доставлен, а результат нас не интересует)
* `$debug` - просит сервис вернуть дополнительную отладочную информацию вместе с ответом


# Задача
В предыдущем упражнении мы создали модуль с сервисом, подсчитывающим сумму. Создайте в этом модуле еще один сервис, который умножает результат на `2` если передать маршрут с дополнительным флагом `multiply: true`. Разрешите сервису выполняться не более 500 миллисекунд.