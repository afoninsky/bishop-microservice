# Введение
Строго говоря, для функционирования архитектуры bishop логгирование не требуется. Однако, при создании полцоценного приложения нам с вероятностью 99% потребуется выводить или сохранять большое количество сообщений (ошибки, предупреждения, дебаг-информация и прочее).

Поэтому, в bishop встроена конфигурируемая библиотека логгирования pino (и это единственный сторонний компонент). Вы можете использовать ее, либо заменить на любую удобную вам.

# Примеры
Выводим сообщения уровня debug и выше (по умолчанию - info и выше):
```javascript
const bishop = require('bishop')({
  log: {
    name: 'my-app',
    level: 'debug'
  }
})
```

Заменяем стороннюю библиотеку на простой логгер встроеный в nodejs:
```javascript
const bishop = require('bishop')({
  defaultLogger: console
})
```

# Задача
В этом упражнении не будет задачи, поэтому просто выполните `bishop-in-action verify <любой файл>` чтобы перейти к следующему упражнению.

# Ссылки
* https://github.com/pinojs/pino - легковесная библиотека для логгирования