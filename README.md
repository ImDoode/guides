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

1. Использование принципа БЭМа для именования стилей. Облегчает чтение и понимание структуры .блок__элемент--модификатор

    Пример 1:
    ```html
    <div class="message">
      <h3 class="message__title">Заголовок сообщения</h3>
      <div class="message__text">Текст сообщения</div>
      <div class="message__text--error">Текст ошибки</div>
    </div>
    ```

    Пример 2:
    ```html
    <div class="news">
        <h3 class="news__title">Новости</h3>
        <ul class="news__list">
          <li class="news__item news-item">
            <h4 class="news-item__title">Заголовок новости</h4>
            <p class="news-item__text">Текст новости</p>
          </li>
          <li class="news__item"><!-- новость --></li>
        </ul>
    </div>
    ```

1. Не использовать `important` без весомых причин. Затрудняет поддержку вёрстки

    Плохо:
    ```html
    <div class="message">
        <div class="message__title">Nice code</div>
    </div>
    ```
    ```css
    .message__title { font-size: 20px !important; }
    ```
    Хорошо:
    ```html
    <div class="some-parent">
        <div class="title">Nice code</div>
    </div>
    ```
    ```css
    .message.message__title { font-size: 20px; }
    ```

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
