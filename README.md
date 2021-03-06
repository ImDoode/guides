Всё изложенное здесь кому-то может показаться очевидным, если так -- просто воздержитесь от чтения.
Предложенные советы основаны на опыте работы с разными командами веб-разработчиков, и по собственному опыту могу сказать, что для некоторых это будет новая информация. 

# Лучшие практики вёрстки

0. Вся вёрстка должна быть на фронте в шаблонах и html, стили -- в файлах стилей, js -- в файлах js.
  Сталкивался с тем, что бэк генерирует вёрстку с инлайновыми стилями -- это ад и сильно замедляет разработку и поддержку кода

1. Никаких инлайновых стилей. Затрудняет поддержку вёрстки

    Плохо:
    ```html
    <div style="font-size: 20px; margin: 20px 0; color: #ccc;">Ugly code</div>
    ```
    Хорошо:
    ```html
    <div class="title">Nice code</div>
    ```
    ```css
    .title { font-size: 20px; margin: 20px 0; color: #ccc; }
    ```

1. Использование принципа БЭМа для именования стилей. Облегчает чтение и понимание структуры вёрстки. Почитать можно [тут](https://ru.bem.info/methodology/css/).
  Я предпочитаю использовать следующий формат:
    ```html
    <div class="users">
      <div class="users__list">
        <div class="users__item">User 1</div>
        <div class="usesr__item">User 2</div>
        <div class="users__item users__item--special">User 3</div>
        <div class="users__item">User 4</div>
      </div>
      <div class="users__control">
        <div class="users__button button button--accept">Add</div>
        <div class="users__button button button--reject">Remove</div>
      </div>
    </div>
    ```
    В данном случае мы видим блок `user`, в нём есть дочерние элементы `list`, `item`, `controls`, `button`, у дочернего элемента `item` есть модификатор `special`.

    Структура scss в данном случае будет выглядеть следующим образом
    ```scss
    .users {
      ...
      &__list { ... }
      &__item {
        ...
        &--special {}
      }
     }
    ```
    Всё просто, красиво и понятно!


1. Не использовать `important` без весомых причин. Затрудняет поддержку вёрстки

1. Стилизовать классы, а не айдишники и не элементы.
  Айди должен быть уникальным на странице и он имеет приоритет, как селектор -- это лишает нас гибкости в вёрстке.
  Стилизование элементов может аукнуться багами в будущем

    Плохо:
    ```html
    <div id="title">Ugly code</div>
    ```
    ```css
    #title { font-size: 20px; margin: 20px 0; color: #ccc; }
    ```
    Хорошо:
    ```html
    <div class="title">Nice code</div>
    ```
    ```css
    .title { font-size: 20px; margin: 20px 0; color: #ccc; }
    ```

1. Для жс-а использовать семантические селекторы с префиксом `.js-`, это избавит от появлений багов и облегчит поддержку вёрстки и кода.
  Так мы сразу видим элементы, с которыми у нас взаимодействует жс

    Плохо:
    ```html
    <div class="popup">Popup content</div>
    ```
    ```css
    .popup { position: absolute; left: 100px; top: 100px; width: 300px; height: 100px; background: #fff; }
    ```
    ```js
    $('.popup').dialog();
    ```
    Хорошо:
    ```html
    <div class="dialog-popup js-popup">Popup content</div>
    ```
    ```css
    .dialog-popup { position: absolute; left: 100px; top: 100px; width: 300px; height: 100px; background: #fff; }
    ```
    ```js
    $('.js-popup').dialog();
    ```

1. Не нужно усложнять селекторы в стилях, код должен быть легко читаем для всех, а не только для вас

1. Задел строку -- отрефачил строку. Не нужно плодить говнокод

# Лучшие практики JS
В интернете очень много информации по этому поводу, но я всё же постараюсь саккумулировать тут основные правила хорошего кода.

1. Не пишите строчки кода длинее 120 символов -- разбивайте и переносите, это повышает читаемость кода.

1. Откажитесь от jQuery в пользу натива. Чем больше приложение, тем больше будут заметны миллисекунды задержек выполнения кода. Сравнение скорости http://vanilla-js.com/.
[Removing jQuery from GitHub.com frontend](https://github.blog/2018-09-06-removing-jquery-from-github-frontend/)

1. Если данные используются дважды -- вынесите в переменную. Это касается функций, объектов DOM, результатов вычислений и тд

1. Давайте полные и понятные имена переменным и функциям. Оставьте сокращение кода для минификаторов.

    Плохо:
    ```js
    s = (q, e) => { ... }
    ```
    
    Хорошо:
     ```js
    search = (query, event) => { ... }
    ```

1. Избегайте лишней вложенности

    Нормально:
    ```js
    if (cond) {
      result = some_function();
    } else {
      result = other_function();
    }
    ```
    Хорошо:
    ```js
    result = (cond) ? some_function() : other_function();
    ```
    Другой кейс:

    Нормально:
    ```js
    if (cond) {
      result = some_function();
    } else { return }
    ```
    Хорошо:
    ```js
    if (!cond) return;
    result = some_function();
    ```


