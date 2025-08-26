# goit-js-hw-08

Разберем этот код по шагам:

1. Поиск элемента галереи javascript

let containList = document.querySelector('.gallery'); Находит элемент с классом
gallery в DOM

Это будет контейнер для наших изображений

2. Создание HTML-разметки javascript const imagesList = images .map( ({ preview,
original, description }) => `<li class="gallery-item">
<a class="gallery-link" href="${original}"> <img
      class="gallery-image"
      src="${preview}"
      data-source="${original}"
      alt="${description}" /> </a>
</li>`
  )
  .join('');
map() преобразует массив объектов в массив HTML-строк

Деструктуризация {preview, original, description} извлекает нужные свойства

Для каждого изображения создается:

<li> с классом gallery-item

Ссылка <a> на оригинальное изображение

<img> с превью, атрибутом data-source (для модального окна) и alt-текстом

join('') объединяет массив строк в одну большую строку

3. Вставка в DOM javascript containList.insertAdjacentHTML('beforeend',
   imagesList); Добавляет созданную разметку в конец элемента галереи

beforeend - вставляет содержимое после последнего потомка

4. Обработчик кликов javascript containList.addEventListener('click', ev => {
   ev.preventDefault(); const { target } = ev; const bigImg =
   target.dataset.source; const altText = target.alt;

if (!bigImg) { return; } // ... открытие модального окна });
ev.preventDefault() - отменяет стандартное поведение ссылки

const { target } = ev - деструктуризация, получаем элемент, на который кликнули

target.dataset.source - получаем оригинальное изображение из data-атрибута

Проверка if (!bigImg) - если кликнули не по изображению (например, по пустому
месту), выходим

5. Открытие модального окна javascript const instance = basicLightbox.create(
   `<img src="${bigImg}" alt="${altText}" width="1112" height="640">` );
   instance.show(); Используется библиотека basicLightbox

Создается модальное окно с оригинальным изображением

Указываются фиксированные размеры 1112x640px

Потенциальные проблемы:

1. Делегирование событий Код может не работать, если:

Кликать по ссылке (<a>) вместо изображения

Кликать по пустому пространству в <li>

Решение: Проверять, что кликнули именно по изображению:

javascript containList.addEventListener('click', ev => { ev.preventDefault();

// Ищем ближайший элемент с классом gallery-image const imageElement =
ev.target.closest('.gallery-image'); if (!imageElement) return;

const bigImg = imageElement.dataset.source; const altText = imageElement.alt;

// остальной код... });
