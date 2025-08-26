# goit-js-hw-08

Разберем этот код по частям:

1. Поиск элемента галереи javascript const gallery =
   document.querySelector('.gallery'); console.log(gallery); Находит элемент с
   классом gallery в DOM

console.log(gallery) - для отладки (показывает найденный элемент в консоли)

2. Создание HTML-разметки javascript

const galleryMarkup = images .map(({ preview, original, description }) => {
return
`<li class="gallery-item"> <a class="gallery-link" href="${original}"> <img class="gallery-image" src="${preview}" data-source="${original}" alt="${description}" width="360" height="200" /> </a> </li>`;
}) .join('');

Что происходит:

map() проходит по каждому объекту в массиве images

Деструктуризация ({ preview, original, description }) - извлекает нужные
свойства

Для каждого изображения создается HTML-строка с:

<li> - элемент списка

<a> - ссылка на оригинальное изображение

<img> - изображение с атрибутами:

src="${preview}" - маленькое превью

data-source="${original}" - оригинальное изображение (для модального окна)

alt="${description}" - описание для доступности

width="360" height="200" - фиксированные размеры

join('') объединяет массив строк в одну большую строку

3. Вставка в DOM javascript gallery.insertAdjacentHTML('beforeend',
   galleryMarkup); Добавляет созданную разметку в конец элемента галереи

beforeend - внутри элемента, после последнего потомка

4. Обработчик кликов javascript gallery.addEventListener('click', function
   (event) { event.preventDefault(); const image =
   event.target.closest('img.gallery-image'); if (!image) return; const
   biggerImage = image.dataset.source; const instance =
   basicLightbox.create(` <img src="${biggerImage}" width="1112" height="640"> `);
   instance.show(); }); Пошагово:

event.preventDefault() - отменяет переход по ссылке

event.target.closest('img.gallery-image') - ищет ближайший элемент изображения с
классом gallery-image

Это нужно, если кликнули не прямо по img, а по другому элементу внутри ссылки

if (!image) return; - если кликнули не по изображению, выходим из функции

image.dataset.source - получает оригинальное изображение из data-атрибута

basicLightbox.create() - создает модальное окно с большим изображением

instance.show() - показывает модальное окно

Как это работает вместе: Загрузка страницы: Создается галерея из миниатюр

Клик по изображению:

Отменяется переход по ссылке

Находится соответствующее большое изображение

Открывается в модальном окне

Преимущества:

Экономия трафика (загружаются только маленькие изображения)

Быстрая загрузка страницы

Удобный просмотр больших версий

Пример результата: Для первого изображения создается такой HTML:

html

<li class="gallery-item">
    <a class="gallery-link" href="https://cdn.pixabay.com/photo/2019/05/14/16/43/rchids-4202820_1280.jpg">
        <img
            class="gallery-image"
            src="https://cdn.pixabay.com/photo/2019/05/14/16/43/rchids-4202820__480.jpg"
            data-source="https://cdn.pixabay.com/photo/2019/05/14/16/43/rchids-4202820_1280.jpg"
            alt="Hokkaido Flower"
            width="360" height="200"
        />
    </a>
</li>
Код эффективен и использует современные подходы JavaScript! 🚀
