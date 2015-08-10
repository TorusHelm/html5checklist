#Чеклист верстки

Для того чтобы отдавать вёрстку клиенту, достаточно соблюдения первых 5&nbsp;пунктов. 
Для выдачи в&nbsp;продакшен&nbsp;&mdash; первых 6.

*Подробности по&nbsp;каждому пункту: http://habrahabr.ru/post/114256/*

1. **Соответствие макету**
2. **Кроссбраузерность, кодировка и&nbsp;DOCTYPE**
3. **Валидность (включая CSSLint и JSHint), доступность, микроформаты**
4. **Независимость блоков в&nbsp;CSS: минимизация каскада, использование техник БЭМ**
5. **Сайт должен нормально смотреться во&nbsp;всех стандартных разрешениях от&nbsp;1024 и&nbsp;выше, не&nbsp;иметь горизонтального скролла и&nbsp;вписываться в&nbsp;экран мобильных устройств**
6. Корректная работа при вбивании реального текста, надёжность вёрстки
7. CSS должен быть написан с&nbsp;использованием препроцессоров (LESS/Sass/Stylus). Желательно использование систем сборки (Grunt/Gulp) и&nbsp;построцессоров (PostCSS/Autoprefixer).
8. Проверка и&nbsp;оптимизация скорости загрузки: https://github.com/delka/WebPerformanceChecklist
9. Наличие Win/Mac/Linux-аналогов шрифтов
10. Доступность при выключенных(загружающихся) картинках
11. HTML5&nbsp;формы, линковка, валидация
12. Семантичность. Отсутствие глупостей в&nbsp;html и&nbsp;css, единообразие, аккуратность
13. Правильная структура заголовков (H1,H2,… и&nbsp;т.д. и&nbsp;TITLE)
14. Работоспособность при выключенном (незагруженном) JavaScript
15. Работоспособность при выключенном Flash
16. Отсутствие багов при увеличенном шрифте

<h2>12. Подробнее: &quot;плохо&quot;/&quot;хорошо&quot;</h2>
Важно понимать что семантика&nbsp;&mdash; может быть не&nbsp;только в&nbsp;используемых элементах, но&nbsp;и&nbsp;в&nbsp;именах классов. И&nbsp;БЭМ-иерархия классов&nbsp;&mdash; это новый уровень семантики.

<b>Плохо:</b>
<ul><li><strong>Самое страшное, к&nbsp;счастью уже редкое&nbsp;&mdash; <code>float: left</code> для всех блоков.</strong> Безумный верстальщик эмулирует привычные ячейки таблиц, расставляя блоки как кирпичи друг за&nbsp;другом. Вон из&nbsp;профеcсии! Проверяется: Web Developer Outline &rarr; Float elements, если всё в&nbsp;красных блоках, вёрстку нужно выкидывать на&nbsp;помойку.</li>
<li>Отступы между блоками на&nbsp;сайте должны быть за&nbsp;счёт margin у&nbsp;блоков, а&nbsp;не&nbsp;выпирающих наружу margin у&nbsp;содержимого блоков.</li>
<li>Плохо&nbsp;&mdash; отсутствие тайтлов.</li>
<li>Плохо&nbsp;&mdash; отсутствие alt у&nbsp;картинок.</li>
  <li>Плохо&nbsp;&mdash; хаки для браузеров внутри main.css (как без фильтров, так и&nbsp;с&nbsp;ними). Без фильтров&nbsp;&mdash; это когда когда просто пишем <code>{zoom: 1;}</code> — это&nbsp;оч. плохо, т.к. будет применяться ко&nbsp;всем&nbsp;IE, а&nbsp;не&nbsp;только к&nbsp;тому, в&nbsp;котором проблема. С&nbsp;фильтрами&nbsp;&mdash; когда пишут <code>(* html, *+html и т.д.)</code> — плохо, потому что это засоряет код, делает его менее читабельным, а&nbsp;какие-то хаки могут быть и&nbsp;вообще невалидными и&nbsp;нарушать прогон CSSLint. Conditional Comments&nbsp;&mdash; тоже плохо, хотя раньше считалось хорошей техникой, плохо т.к. это увеличение кол-ва css-файлов и&nbsp;главное&nbsp;&mdash; это разнесение кода в&nbsp;разные места. Сейчас рекомендуется использовать специальные классы типа <code>html.ie7, html.ie8,…</code> (из&nbsp;HTML5&nbsp;Boilerplate), Modernizer-детектирование фич (классы вида <code>html.js.flexbox.canvas.no-touch…</code>) и&nbsp;JS-детектирование браузера и&nbsp;платфорым (например CSS Browser Selector генерирующий классы вида <code>html.webkit.chrome.chrome25.win.win8…</code>)</li>
<li>Плохо&nbsp;&mdash; не&nbsp;проверять tabindex в&nbsp;формах.</li>
<li>Плохо&nbsp;&mdash; писать стили не&nbsp;думая о&nbsp;логике размещения элементов. Например, если элемент всегда находится сверху, у&nbsp;него должен быть большой z-index, нельзя надеяться на&nbsp;то&nbsp;что сейчас всё нормально смотрится&nbsp;&mdash; стили должны быть железобетонными. Если элемент всегда должен находится на&nbsp;каком-то месте, в&nbsp;независимости от&nbsp;окружающих его элементов&nbsp;&mdash; это position: absolute; а&nbsp;не&nbsp;float и&nbsp;т.д.
Блоки независящие друг от&nbsp;друга не&nbsp;должны быть внутри одного блока (например телефон компании и&nbsp;поиск по&nbsp;сайту). Блоки независящие по&nbsp;расположению друг от&nbsp;друга должны быть position absolute, а&nbsp;не&nbsp;float&rsquo;ится.</li>
<li>Очень плохо&nbsp;&mdash; презентационные классы (right, red).</li>
<li>Нежелательно когда вёрстка содержить пустые блоки для презентационных целей, для этого существуют псевдоэлементы</li>
<li>Плохо когда нет базовых стилей у&nbsp;стандартных элементов. Т.е. просто h1,h2,ul,table,etc без классов должны смотреться красиво и&nbsp;органично. Проще говоря&nbsp;&mdash; используйте Normalize, a&nbsp;не&nbsp;Reset CSS.</li>
<li>Плохо когда нет постепенного уточнения стилей для текста, когда стиль выписывается для каждого элемента отдельно, а&nbsp;за&nbsp;его пределами&nbsp;&mdash; внешний вид может быть кардинально другой. Речь о&nbsp;ситуации когда например текст, написанный без абзацев, имеет вообще не&nbsp;тот стиль что у&nbsp;всех элементов в&nbsp;блоке. Надо вести стили снизу вверх, постепенно уточняя&nbsp;их. Тут важно не&nbsp;путать стили для текста и&nbsp;стили для блоков. Для текста&nbsp;&mdash; каскад это добро, для блоков сайта&nbsp;&mdash; нужно использовать БЭМ.</li>
<li>Ещё хуже&nbsp;&mdash; чересчур детализированные глобальные стили. Например <code>a {font: italic 10px Tahoma;}</code> /* Ненависть! Ненависть! НЕНАВИСТЬ!!11 */ Потом приходится переопределять стиль ссылок для каждого блока.</li>
<li>Размеры и&nbsp;позиционирование элемента должны указываться в&nbsp;одних единицах измерения. Т.е. высота/ширина блока в&nbsp;px&nbsp;и&nbsp;margin/padding в&nbsp;em&nbsp;&mdash; это странно и&nbsp;скорей всего ошибка. Line-height&nbsp;&mdash; лучше задавать коэффициентом (1/1.2/1.4... т.е. без указания единицы измерения&nbsp;&mdash; это цифра на&nbsp;которую умножается font-size и&nbsp;получится межстрочный интервал). Если задали font-size/height в&nbsp;em&nbsp;&mdash; значит задаём и&nbsp;margin/padding тоже в&nbsp;em. Классический пример: список dl-dt-dd, где dt&nbsp;и&nbsp;dd&nbsp;ставятся друг на&nbsp;против друга с&nbsp;помощью подтягивания dd&nbsp;отрицательным margin вверх. Или&nbsp;&mdash; выделили padding&rsquo;ом место под position: absolute какого-то текстового блока. У&nbsp;текстовых элементов (абзацей, ячеек таблиц) задаём padding и&nbsp;height в&nbsp;em (чтоб корректно увеличивать размер шрифта) .</li>
<li><s>Плохо</s>(недопустимо!) вешать стили на&nbsp;селекторы вложенных стандартных тэгов, без классов. Т.е. допустим пишем что-то типа <code>h2&nbsp;a span {какая-то крепкая штука, типа картинки с&nbsp;графикой, что закрывает текст в заголовке}</code>, а&nbsp;потом клиент в&nbsp;визиге внезапно вбивает такое сочетание! И&nbsp;получаем невероятный баг. На просто одиночные теги для вывода текста из БД — можно, но используя блок .b-text (смотри BEM CSS).</li>
<li>Плохо&nbsp;&mdash; напрямую задавать визуальное отображение элементов через&nbsp;js: <code>$('.element').css(color,"#f00")</code>. Это должно делаться через установку/смену классов.</li></ul>

<b>Хорошо:</b>
<ul><li><strong><a href="http://getbem.com/">БЭМ</a></strong>! Важно понимать что это методология, а&nbsp;не&nbsp;инструменты. Для обычных сайтов достаточно вёрстки по&nbsp;<a href="http://delka.github.io/talks/webcamp/2015/bem/">BEM CSS</a>, без использования библиотеки блоков и&nbsp;bem-tools. <a href="http://delka.name/blog/2013/04/bem-otkroveniya-prinyavshih-veru/">Я&nbsp;долго считал что &laquo;BEM&nbsp;&mdash; это классная идея, но&nbsp;это чересчур, так категорично не&nbsp;надо, надо чуть по-другому, под себя...&raquo;</a>, так вот&nbsp;&mdash; это неверно! Нужно обязательно уходить от&nbsp;каскада, а&nbsp;БЭМ&nbsp;&mdash; это один из&nbsp;отличных вариантов решения.</li>
<li>Хорошо&nbsp;&mdash; структурировать код в&nbsp;блоки описывающие логику документа. Т.е. создавать div даже там, где он&nbsp;для презентационных целей не&nbsp;нужен. И&nbsp;наоборот&nbsp;&mdash; стараться не&nbsp;ставить лишний div там, где структура этого не&nbsp;требует, а&nbsp;это нужно лишь для визуальных эффектов.</li>
<li><strong><a href="http://html5boilerplate.com">HTML5 Boilerplate</a></strong>&nbsp;&mdash; замечательный стартовый шаблон от&nbsp;&laquo;отцов&raquo;. Используйте и&nbsp;присоединяйтесь к&nbsp;разработке, добавляйте свои велосипеды туда! 
Раньше у&nbsp;нас был свой самописный framework-стартовый html, теперь используем Boilerplate как основу, а&nbsp;в&nbsp;него уже добавляем старые наработки.</li>
<li>Используйте наработанные решения, чужие модули, jQuery-плагины, не&nbsp;изобретайте велосипедов, а&nbsp;если изобретаете&nbsp;&mdash; поддерживайте&nbsp;их, ведите библиотеку кода (после каждого нового проекта добавляйте туда код, обновляйте старый).</li>
<li>Для текстовых блоков, что редактируются в&nbsp;админке, должна обеспечиваться атомарность текстовых стилей. Т.е. есть у&nbsp;нас страничка с&nbsp;каким-то текстовым блоком, примерно такой структуры:
```css
.content-text h1
.content-text .entry
.content-text .entry .somenamedblock
```
То .somenamedblock должен получать текстовые стили непосредственно&nbsp;&mdash; <code>.somenamedblock {font: …; color: …;}</code>, т.к. иначе в&nbsp;визиге админки мы&nbsp;не&nbsp;сможем их&nbsp;застайлить.</li>
<li>одинаковый html-код для блоков на&nbsp;морде и&nbsp;внутряках, с&nbsp;идентичным контентом, но&nbsp;разным визуальным представлением данных. Реализуется через модификаторы блоков и элементов, но не через модификацию от родителя (каскад от body.pagename например!)</li></ul> 

<h2>17. Важные мелочи</h2>

<ul><li>Лого на&nbsp;внутряках должно вести на&nbsp;титулку. На&nbsp;титулке logo = h1, на&nbsp;внутряках H1=заголовок контента, а&nbsp;Logo=div</li>
  <li>У&nbsp;каждой страницы должен быть свой уникальный TITLE формата <code>About Us&nbsp;&mdash; %CompanyName%</code></li>
  <li>Все страницы должны быть слинкованы и&nbsp;<a href="http://home.snafu.de/tilman/xenulink.html">проверены на&nbsp;наличие битых ссылок</a>.</li>
  <li>Все ссылки должны как-то реагировать на :hover, :active и :focus&nbsp;&mdash; показыванием/убиранием подчёркивания, сменой цвета, чем угодно. У&nbsp;всех ссылок, кроме пунктов меню, должна быть реакция на :visited</li>
  <li>Проверять что все интерактивные элементы страницы что должны работать&nbsp;&mdash; работают.</li>
  <li>&laquo;Контент в&nbsp;начале страницы&raquo;&nbsp;&mdash; содержимое страницы должно идти в&nbsp;начале кода, до&nbsp;всяких сайдбаров и&nbsp;прочего.</li>
  <li>Все созданные странички изначально должны быть порезаны на шаблоны, чтоб программеру было легче их интегрировать.</li>
  <li><a href="http://habrahabr.ru/blogs/typography/23812/">Копирайт должен быть написан правильно</a>.</li>
  <li>Должны быть favicon.ico (желательно с&nbsp;включенными внутрь неё 32&times;32, 48&times;48 и&nbsp;64&times;64&nbsp;вариациями) и&nbsp;apple-touch-icon</li>
  <li>В&nbsp;вёрстке не&nbsp;должны оставаться закомментированные &laquo;на&nbsp;всякий случай&raquo; куски кода, лишние неиспользуемые файлы, старые версии файлов и&nbsp;т.п. Все бекапы можно вытянуть из&nbsp;системы контроля версий (например Git или SVN), а&nbsp;на&nbsp;живом проекте &laquo;мусор&raquo; потом мешает разобраться как что работает.</li>
  <li>Размеры для блоков, чьи размеры зависят от&nbsp;содержащегося в&nbsp;них текста, нужно задавать в&nbsp;em, а&nbsp;не&nbsp;px.</li>
  <li>Если url ссылки неизвестен, то&nbsp;он&nbsp;должен быть равен её&nbsp;анкору, написанному латиницей с&nbsp;заменой пробелов/спецсимволов на&nbsp;тире.</li>
  <li>Skype-плагин не&nbsp;должен ломать вёрстку</li>
  <li>Ресайз textarea не&nbsp;должен ломать вёрстку</li>
  <li>При проверке frontend в&nbsp;целом&nbsp;&mdash; 404-страница должна отдаваться с&nbsp;кодом 404&nbsp;а не&nbsp;200.</li>
  <li>Нужно подстраховываться фиксируя в&nbsp;css размеры картинок, выводящихся программно.</li>
  <li>Проверка орфографии Word&rsquo;ом или <a href="http://www.artlebedev.ru/tools/orfograf/">Орфографом</a>, желательно&nbsp;&mdash; <a href="http://www.artlebedev.ru/tools/typograf/">оттипографить</a> контент.</li>
  <li>Ссылки на&nbsp;чужие сайты должны быть с&nbsp;<code>target="blank"</code>, желательно выделять их&nbsp;иконкой &laquo;внешняя ссылка&raquo;.</li>
  <li>Разумеется картинки должны быть в&nbsp;отдельной папке, css&nbsp;&mdash; в&nbsp;отдельной и&nbsp;js&nbsp;&mdash; в&nbsp;отдельной. Графика, не являющаяся частью дизайна (всякие илююстрации, фото в новостях и т.д.) — нужно положить в отдельную папку, например userfiles.</li>
  <li>Изображения должны масштабироваться в зависимости от размера окна <code>(max-width:100%; height:auto;)</code></li>
</ul>
