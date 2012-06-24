# Гайдлайны для вёрстки



## Общие требования
- Кодировка всех файлов, если не указано обратное&nbsp;&mdash; UTF-8, без [BOM](http://en.wikipedia.org/wiki/Byte_order_mark).
- Использование транслита с русского в именах файлов, CSS-селекторах и т.п. недопустимо. Правильно, например: `.l-header`, неправильно: `.l-shapka`.
- Комментариев кириллицей лучше избегать, особенно в CSS и JavaScript.
- Отступы делаются табуляцией (никаких holy wars, просто соглашение).
- CSS и JavaScript размещаются в большом количестве файлов, в них свободно используются комментарии. Подразумевается, что в реальном проекте эти файлы будут объединены, минимизированы и сжаты в gzip.
- Кавычки в CSS и JavaScript всегда одиночные (`'`), для атрибутов в HTML&nbsp;&mdash; всегда двойные (`"`).
- Все файлы называются в нижнем регистре, если не указано обратное


## Общие принципы и приоритеты
- Чем меньше графики, тем лучше
- Решение средствами CSS лучше решения с графикой
- Cложное решение с CSS-хаками хуже решения с простым и понятным JavaScript



## HTML

### Структура
- Файлы могут быть статичными, но если верстаемых страниц больше одной, скорее всего имеет смысл вынести общие элементы в отдельные файлы и собирать страницу с помощью любой серверной технологии (SSI, PHP, ASP.NET и т.д.).
- Использование тегов в соответствии с семантикой
- Использование тегов по их назначению вместо `<div>` и `<span>` там, где это возможно.

### Оформление
- Использование отступов, иллюстрирующих вложенность (допустимо «сбрасывать» отступы влево внутри больших блоков).
- Закрывающие теги больших блочных элементов должны заканчиваться комментарием с указанием CSS-селектора для блока, чтобы было понятно какой тег закрывается. Это будет полезно на том этапе, когда HTML-код разбивается на несколько файлов-шаблонов.

Пример:

```html
<div class="b-news">
	<div class="b-news__latest">
		...
	</div><!-- /.b-news__latest -->
</div><!-- /.b-news-->
```

### Содержимое
- HTML-код должен проходить валидацию по выбранному `DOCTYPE` (в последнее время чаще всего это HTML5)
- Тексты на макете должны быть на том языке, на котором будет сайт, 
- Cледует использовать реальные тексты и данные, если такой возможности нет, то [тексты, похожие на настоящие](http://vesna.yandex.ru/).
- В тексте должна быть расставлена [правильная типографика](http://artvolk.sumy.ua/uploads/texts/artvolk-office_typography.pdf) для языка сайта.

### Особые случаи
- Применение inline-стилей (атрибут `style=""`) запрещено. Исключение&nbsp;&mdash; `style="display: none"`, если это необходимо.
- Пустые ссылки (включая те, на которых будут только JavaScript-обработчики) должны выглядеть так: `<a href="#">Кликни меня</a>`, а не так `<a href="javascript:;">Кликни меня</a>`.

### HTML5
- Пока доля браузеров (старые IE), [которые не поддерживают новые HTML5 теги](http://caniuse.com/#feat=html5semantic) и [новые возможности форм](http://caniuse.com/#feat=forms) без дополнительных JavasScript-библиотек ещё велика, эти возможности не используем, если не оговорено обратное.



## Изображения
- Не должно быть неиспользуемых изображений.
- Файлы должны быть оптимизированы по размеру для веба, должны быть правильно выбраны форматы файлов в зависимости от характера изображения.
- Там, где это возможно, лучше использовать PNG8 вместо GIF.
- Для больших файлов в формате PNG24 можно использовать вынесение непрозрачных частей картинки в отдельный файл другого формата и сборку финальной картинки с помощью нескольких фоновых изображений.
- Если позволяет задача, предпочтительнее делать CSS-спрайты сразу на этапе вёрстки. 
- Спрайты обязательны для роловеров (например, если иконка меняется при наведении на кнопку).
- Файлы нужно разделять на папки по предназначению, временные файлы изображений (например, временные баннеры) нужно класть в отдельную папку, например `/images/temp/`), чтобы их можно было легко удалить при интеграции.
- Если в вёрстке есть изображения которые, возможно, придётся изменить позднее, стоит включать в проект `psd`-файлы этих элементов в папке `/graph/`. Примером подобных изображений может быть сложный графический элемент с текстом (его и может понадобиться изменить), используемый в вёрстке целиком как фоновая картинка. Графические кнопки всегда нужно верстать так, чтобы надписи на них были текстом, а сами кнопки адаптировались под количество текста на них (см. ниже ссылки на способы).

### Правила именования
- Имена файлов с фоновыми картинками должны начинаться с префикса `bg-`, иконок с `icon-`, кнопок с `button-`.
- В качестве разделителя слов в названиях файлов необходимо использовать дефис.
- Правила сокращения некоторых слов в именах файлов:
	- left = `l`
	- right = `r` (например, `user-pic-r.png`)
	- top = `t`
	- bottom = `b` 
	- ascending = `asc`
	- descending = `desc`
	- horizontal = `h`
	- vertical = `v`
- Допустимы объединения сокращений: `bg-table-lb.png` (фоновая картинка (`bg-`) таблицы, левая (`l`) нижняя (`b`) часть).
- Слова active, inactive, selected, up, down, field не сокращаются.



## JavaScript (для случая использования jQuery)

### Общие рекомендации
- Код инициализации элементов на текущей странице по событию `DOMReady` должен быть вынесен в отдельные файлы (по одному на страницу). Файл можно подключать как внешний ресурс или подставлять прямо в шаблон средствами серверных скриптов.
- Если не оговорено, необходимо использовать [`jQuery.noConflict()`](http://api.jquery.com/jQuery.noConflict/)

### Скрипты для проекта
- Собственные плагины общего назначения, не специфичные для данного проекта (т.е. те, которые скорее всего будут использоваться не в одном проекте), должны придерживаться стандартных именований файлов для jQuery-плагинов, например, `jquery.supertip.js`
- Собственные плагины, специфичные для данного проекта (т.е. те, которые нельзя будет использовать нигде больше) необходимо именовать следующим образом: `jquery.<кодовое название проекта>_<имя плагина>.js`, название самого плагина в этом случае будет `<кодовое название проекта>_<имя плагина>`, например: в файле `jquery.project_mySuperPlugin.js` будет содержаться плагин `project_mySuperPlugin`. Причина использования «некрасивых» названий: для некоторых плагинов может понадобиться поддержка вызова методов цепочкой (chaining), это ограничивает возможность использования техник эмулирующих неймспейсы.
- Для написания плагинов нужно использовать один из проверенных паттернов:
	- [jQuery boilerplate](http://jqueryboilerplate.com/)
	- [jQuery widget factory](https://github.com/scottgonzalez/widget-factory-docs/)

### Сторонние jQuery-плагины и библиотеки
- Если сторонний плагин поставляется в сжатом (minimized, packed) и исходном виде оба файла должны быть включены в проект, но подключаться должен сжатый вариант. Исключение&nbsp;&mdash; библиотеки jQuery и jQuery UI, для них нужно использовать только минимизированные версии.
- В случае использования сторонних библиотек, для которых существует конструктор версии для скачивания (например, [jQuery UI](http://jqueryui.com/download) или [jQuery Tools](http://www.jquerytools.org/download/)), необходимо документировать в отдельном текстовом файле (например, `/js/_readme.txt`) конфигурацию, использовавшуюся для генерации.
- Если сторонний плагин требует кроме JavaScript-кода подключения CSS-файлов и наличия картинок, эти элементы должны быть вынесены в соответствующие подпапки проекта (см. ниже пример структуры файлов проекта и приём переопределения путей в CSS).

### Размещение файлов
- При небольшом количестве файлов (до 10) файлы можно размещать в одной директории, если файлов больше и\или некоторые компоненты состоят из нескольких файлов лучше сделать подпапки для хранения, называя их по имени файла плагина, но без расширения.

### Особые случаи
- Для JSON-сериализации в [старых браузерах](http://caniuse.com/#search=JSON) предпочтительнее использовать [эту реализацию](http://www.json.org/js.html).



## Flash
Для вставки Flash следует использовать [swfobject](http://code.google.com/p/swfobject/) если не используется библиотека jQuery и 
[jQuery SWFObject](http://jquery.thewikies.com/swfobject/) если эта библиотека используется.



## CSS

### Организация файлов
CSS-код разбивается на несколько файлов по смыслу (т.е. субъективно). Минимальный набор файлов:

- `reset.css` (или [`normalize.css`](http://necolas.github.com/normalize.css/))&nbsp;&mdash; сброс стилей браузера по умолчанию (например, [Eric Meyer's reset](http://meyerweb.com/eric/tools/css/reset/), [HTML5 Reset](http://html5reset.org/))
- `layout.css`&nbsp;&mdash; общие стили, формирующие сетку (макет, layout) страниц. Часто в этом файле могут использоваться следующие приёмы и техники
	- [Принудительное включение вертикальной полосы прокрутки](http://css-tricks.com/snippets/css/force-vertical-scrollbar/)
	- [Sticky footer](http://www.cssstickyfooter.com/)
	- [Шрифты в em](http://cssing.org.ua/2006/10/16/font-size-em/) если важен IE6. Если не важен, то базовый размер шрифта задается в пикселях, остальные&nbsp;&mdash; в em
- `fonts.css`&nbsp;&mdash; для подключения шрифтов через `@font-face`, файлы удобно подготовить в [генераторе](http://www.fontsquirrel.com/fontface/generator)
- `print.css`&nbsp;&mdash; CSS для печати (можно и нужно [объединить CSS для экрана и для печати](http://snippets.crisp-studio.com/view/9/prostoj-sposob-pomeshheniya-v-odin-fajl-css-dlya-ekrana-i-pechati))
- `ui.css`&nbsp;&mdash; общие элементы интерфейса (кнопки, иконки, поля ввода)
- `widgets.css`&nbsp;&mdash; более крупные элементы интерфейса (пейджер, бредкрамб и т.п.) 
- ... (другие файлы по смыслу, например, по страницам (`page-index.css`, `page-cart.css` и т.п.) или по контроллерам\экшенам)

### Базовые приёмы и техники
- Творческое [использование списков](http://css.maxdesign.com.au/listamatic2/index.htm) для формирования меню и т.п. элементов.
- Творческое использование фоновых картинок для списков, иконок и т.п. 	
- [CSS-спрайты](http://webo.in/articles/habrahabr/08-all-about-css-sprites/) для уменьшения числа запросов на сервер, реализации hover-эффектов
- Предзагрузка (preload) картинок с помощью CSS.
- Выравнивание одной строки по вертикали с помощью `line-height`.
- Выравнивание блоков по центру с помощью `margin: 0px auto;`.
- [Растягиваемые графические кнопки](http://www.catswhocode.com/blog/top-10-css3-buttons-tutorials), часто [вот эти](http://members.chello.nl/o.karadeniz/sndbx/even_more_sexy_button/index.html)

### CSS3 и vendor-prefixes
- Текущую поддержку лучше проверять перед стартом каждого проекта, например, на [этом сайте](http://caniuse.com/) или [на этом](http://html5please.com/#use), учитывая целевые браузеры.

### Структура CSS
Для организации CSS используется упрощённая [методология БЭМ](http://bem.github.com/bem-method/pages/beginning/beginning.ru.html). Упрощения состоят в том, что не используются автоматические инструменты, строгость правил несколько уменьшена и немного изменены соглашения по именованию.

#### Термины и определения
*Блок*&nbsp;&mdash; логический элемент (не HTML элемент!) страницы. Примеры блоков: меню, кнопка с иконкой. 
**Важное правило**: внутри блока могут находится **только** другие блоки (например, кнопка с иконкой внутри меню) и\или элементы этого блока.

*Элемент*&nbsp;&mdash; логический компонент (не HTML элемент!) блока, который не имеет смысла в отрыве от блока. Для блока меню это может быть, например, пункт меню. Для кнопки с иконкой&nbsp;&mdash; надпись на кнопке.

*Модификатор*&nbsp;&mdash; CSS-класс с помощью которого можно изменить внешний вид блока или элемента. Например, поменять иконку у кнопки.

#### Правила именования
Схема именования блоков, элементов и модификаторов отличается от [текущей, принятой для проекта БЭМ](http://bem.github.com/bem-bl/pages/naming/naming.ru.html) и больше похожа на [старую](http://vitaly.harisov.name/article/independent-blocks.html).

- Для именования блоков, элементов и модификаторов (которые, кстати, могут быть реализованы любыми HTML-тегами) используются **только CSS-классы**. Селекторы по id, тегу и т.п. запрещены.
- Разделитель слов в именах блоков и элементов&nbsp;&mdash; символ дефиса (`-`)
- Cтандартные термины для обозначения блока-обёртки `wrap`, внутреннего блока&nbsp;&mdash; `inner`.
- Для блоков и элементов выбираются те HTML теги, которые подходят по семантике. Другими словами логический блок заголовка может быть представлен тегом `<h1>`, необязательно заворачивать его в `<div>`.

CSS-классы блоков именуются следующим образом:

```text
.[l|b]-<имя блока>
```

CSS-классы элементов именуются следующим образом: 

```text
.[l|b]-<имя блока>__<имя элемента>
```

CSS-классы модификатора блока:

```text
.m-<имя блока>_<тип модификатора>_<значение модификатора>
```

CSS-классы модификатора элемента:

```text
.m-<имя блока>__<имя элемента>_<тип модификатора>_<значение модификатора>
```
#### Примеры

Пример HTML-кода блока с элементами (панель с кнопками, объединёнными в группы):

```html
<!-- Блок -->
<div class="b-toolbar">
	<!-- Элемент group блока b-toolbar --->
	<ul class="b-toolbar__group"> 
		<li>
			<!-- Блок, который вложен в другой блок вместе со своими элементами -->
			<a href="#" class="b-button"><span class="b-button__icon"></span>Открыть</a>
		</li>
		<li>
			<a href="#" class="b-button"><span class="b-button__icon"></span>Сохранить</a>
		</li>
	</ul>
	<ul class="b-toolbar__group">
		<li>
			<a href="#" class="b-button"><span class="b-button__icon"></span>Экспорт</a>
		</li>
		<li>
			<a href="#" class="b-button"><span class="b-button__icon"></span>Импорт</a>
		</li>
	</ul>
</div><!-- /.b-toolbar -->
```

В CSS-коде отступы иллюстрируют вложенность элементов в блоки, например:	

```css
/*
	.b-toolbar
*/
.b-toolbar
	{
	...
	}
	
	.b-toolbar__group
		{
		...
		}

/*
	.b-button		
*/
.b-button
	{
	...
	}
	
	.b-button__icon
		{
		...
		}
```

В случае сложных блоков можно использовать составные имена элементов, например, так (псевдокод):

```text
.b-news
	.b-news__top
		.b-news__top-title
		.b-news__top-text
	.b-news__other
		.b-news__other-title
		.b-news__other-text
```

Блоки могут быть двух видов:

- Блоки сетки страницы (называются так: `l-<имя блока>`)
- Обычные блоки (называются так: `b-<имя блока>`)

Разделение условное, обычно `l-`блоков гораздо меньше и стили для них описаны в одном файле `layout.css`. В случае, если на сайте может быть несколько разных шаблонов для страниц, можно разделить стили на несколько файлов.

Цель существования этих блоков&nbsp;&mdash; определить сетку страницы, в которую можно поместить обычные блоки, поэтому обычно для них указываются только стили для размеров и позиционирования. Для `l-`блоков особенно важно указывать в комментариях где находится закрывающий тег того или иного блока.

Пример `l-`блоков:

```html
<html>
	<head>...</head>
	<body>
		<div class="l-page">
			
			<div class="l-header">
				<!-- У `l-`блоков тоже могут быть элементы -->
				<div class="l-header__logo">
					...
				</div><!-- /.l-header__logo --> 
				<div class="l-header__menu">
					...
				</div><!-- /.l-header__menu -->
			</div><!-- /.l-header -->
			
			<div class="l-main">
				<div class="l-main__sidebar">
					...
				</div><!-- /.l-main__sidebar -->
				<div class="l-main__content">
					...
				</div><!-- /.l-main__content -->
			</div><!-- /.l-main  -->

			<div class="l-footer">
				...
			</div><!-- /.l-footer -->
			
		</div><!-- /.l-page -->
	</body>
</html>
```

#### Модификаторы
Для изменения внешнего вида блоков или элементов можно определить классы-модификаторы. 

Обычный блок: 

```html
<a href="#" class="b-button">
	<span class="b-button__icon"></span>Войти на сайт
</a>
```

Блок с модификатором:

```html
<a href="#" class="b-button m-button_icon_login">
	<span class="b-button__icon"></span>Войти на сайт
</a>
```

У блока может быть одновременно несколько модификаторов:

```html
<a href="#" class="b-button m-button_icon_login m-button_size_small">
	<span class="b-button__icon"></span>Войти на сайт
</a>
```

## Использование LESS

CSS-препроцессоры позволяют сократить запись в случае использования БЭМ. [LESS](http://lesscss.org/) лучше использовать в одном из серверных вариантов ([lessphp](http://leafo.net/lessphp/), [dotless](http://www.dotlesscss.org/) и т.п.).

В простейшем случае можно использовать вложенность так:

```scss
/*
	.b-toolbar
*/
.b-toolbar
	{
	...
	
	&__group
		{
		...
		}
	}
```

Для блока с модификаторами можно сократить запись:

```scss
/*
	Работу фрагмента можно проверить тут: http://leafo.net/lessphp/editor.html
*/

// Блок с модификаторами
category-menu // Имя блока
{
	// Блок и его элементы
	.b-& 
		{
		
		// Стили для блока
		color: red;

		// Стили для элементов блока
		&__item
			{
			color: yellow;

			// Псевдокласы для элемента
			&:hover 
				{
				color: green;
				}

			// Элемент со сложным именем: .b-category-menu__item-title
			&-title 
				{
				font-weight:bold;
				}
			}
		}

	// Стили для модификаторов блока и элементов
	.m-&
		{

		// Модификатор блока
		&_size_small
			{
			
			// Стили для блока
			font-size: 50%;

			// Стили для элемента, которые содержатся в модифицируемом
			// блоке. Так и не придумали как не повторять в этом случае .b-category-menu
			.b-category-menu__item 
				{
				color: yellow;
				}
			}
   
		// Модификатор элемента
		&__item_size_small
			{
			font-size: 50%;
			}
		}
}
```

Результат LESS-кода выше будет таким:

```css
.b-category-menu { color:red; }
.b-category-menu__item { color:yellow; }
.b-category-menu__item:hover { color:green; }
.b-category-menu__item-title { font-weight:bold; }
.m-category-menu_size_small { font-size:50%; }
.m-category-menu_size_small .b-category-menu__item { color:yellow; }
.m-category-menu__item_size_small { font-size:50%; }
```

#### Преимущества подхода
- Нет необходимости задумываться какие селекторы использовать (один ответ на все вопросы: &laquo;по id, по классу? по имени тега?&raquo;)
- Если по мере развития сайта блок, который раньше был единственным на странице будет необходимо продублировать (был один блок меню, стало два) не придётся менять селекторы.
- Если возникнет необходимость поменять теги, которые являются блоками или элементами (например, был `<submit>`, теперь нужна ссылка), селекторы менять не придётся
- Минимизирована возможность конфликта селекторов
- Имена классов имеют отдельное «пространство имён» благодаря префиксам
- Селекторы по классу [считаются одними из самых быстрых](http://webo.in/articles/habrahabr/19-css-efficiency-tests/)
- Легкость выявления и удаления неиспользуемых стилей

#### Недостатки подхода
- Разделение страницы на блоки субъективно
- Избыточность и многословность кода (отчасти компенсируется лёгкостью выявления и удаления неиспользуемого CSS-кода в процессе развития проекта)
- Из-за того, что используется упрощённая версия БЭМ, распределение CSS-стилей блоков по файлам неоднозначно
- Не используется каскадирование в CSS

#### Структура одного CSS правила
- Свойства указываются в следующем порядке (от общего к частному):
	- `position`, `left`, `top`
	- `display`
	- `float`, `clear`
	- `width`, `height`
	- `margin`, `padding`, `border`
	- `vertical-align`
	- `text-align`
	- `background`
	- `color`
	- `font`, `text-decoration`
	- `list-style`
	- `white-space`
	- остальные свойства...
- Следующие свойства должны использоваться только в сокращённом виде: `margin`, `padding`, `border`, `background`, `list-style`, кроме случаев, если нужно переопределить только одно из значений. 
- Следующие свойства желательно указывать в сокращённом виде, если это возможно: `font`.
- Цвета должны указываться в HEX-формате заглавными буквами, например: `#F3F3F3`.
- Для указания гарнитуры шрифта следует максимально использовать наследование. Последним в списке всегда должно идти название универсального семейства (`serif`, `sans-serif` и т.п.).
- Указание адресов в большинстве случаев возможно без кавычек, например, `background-image: url(/images/header/logo.png)`

### Сторонние CSS-файлы
В случае подключения сторонних библиотек часто необходимо внести модификации в некоторые из CSS-правил. В этом случае вместо модификации исходного файла необходимо переопределять нужные правила в отдельном. К примеру, для [Fancybox](http://fancybox.net/) файлы могут быть названы так: 

- `jquery.fancybox-1.3.1.css`&nbsp;&mdash; оригинальный немодифицированный файл
- `jquery.fancybox.override.css`&nbsp;&mdash; переопределение нужных правил

Такой подход упростит обновление сторонних компонентов. Аналогично можно реализовывать темы оформления. Часто такой подход используется, чтобы перенести графику, необходимую для стороннего плагина в нужную папку.

### Поддержка IE6 (кому-то ещё нужно? :))
- В случае необходимости поддержки IE6 отдельный CSS-файл может использоваться в следующих целях:
	- Замены картинок PNG24 на упрощённые аналоги
	- Исправления ошибок рендеринга браузера
- Предпочтительно обойтись упрощённой графикой, а не использовать `png fix` для IE6.
- Отдельный CSS-файл для этого браузера необходимо подключать с помощью [условных комментариев](http://en.wikipedia.org/wiki/Conditional_comment).

### Поддержка IE7, IE8
- Для IE7 и IE8 обычно можно обойтись без отдельного файла стилей.
- Реализация следующих дизайнерских приёмов может быть реализована средствами CSS во всех браузерах, кроме указанных. Если некоторое упрощение внешнего вида допустимо, следует использовать [CSS-решение](http://www.phpied.com/css-performance-ui-with-fewer-images/):
	- Закруглённые углы.
	- Тени и glow (как для блоков так и для текста, может быть реализован в IE с помощью фильтров).
- Можно использовать условные комментарии для выставления классов для `body` (например, как в [HTML5 boilerplate](http://html5boilerplate.com/html5boilerplate-site/built/en_US/docs/html/#ie-html-tag-classes))

### Особые случаи
- Применение CSS-хаков следует свести к минимуму.
- Фильтры в IE использовать не следует из-за проблем с производительностью.
- Использовать CSS expressions не следует по той же причине.
- Использование конструкции `!important` нежелательно. В большистве случаев без неё можно обойтись.
- Использования `<div style="clear: both"></div>` или `<br clear="all" />` почти всегда можно избежать одним из способов (в порядке предпочтения):
	- указав `clear: both;` в CSS для блока, который идёт ниже;
	- использовав [приём `overflow:hidden`](http://habrahabr.ru/blogs/css/48383/) (недостаток метода: блоки с абсолютным позиционированием, например всплывающее меню будут обрезаны границами блока)
	- использовав [приём с `display: table;`](http://www.xiper.net/collect/html-and-css-tricks/karkas-verstki/fix-colonka-rezinovaya-clear-both.html).
	- использовав [Easy Clearing](http://www.positioniseverything.net/easyclearing.html)
	- использовав [любой другой приём](http://www.ejeliot.com/samples/clearing/rule-support.html)
- Применение правильной версии кода для сброса стилей по умолчанию позволяет не использовать HTML-атрибуты `cellspacing` и `cellpadding` для таблиц.
- Необходимо применять `&nbsp` и `white-space: nowrap;` там, где текст не должен переносится.
- Для областей с контентом, который редактируется пользователем (например: комментарии, посты и т.п.) необходимо использовать простые селекторы по тегам и по возможности не использовать CSS-классы. Желательно заранее знать, каким способом (WYSIWIG-редактор, Markdown, Wiki-разметка) будет генерироваться это содержимое.



## Пример структуры файлов проекта вёрстки

В примере используется jQuery-плагин [Fancybox](http://fancybox.net/) в качестве примера плагина с собственными CSS-файлами и изображениями, шаблоны собираются с помощью простого PHP-скрипта. Условное название проекта `project`.

```text
/css
	reset.css
	layout.css
	fonts.css
	ie6.css
	...
	/plugins
		/jquery.fancybox
			jquery.fancybox-1.3.4.css 
			jquery.fancybox.override.css 
	...
/graph	
	...
/flash
	some-movie.swf
	...
/fonts
	...
/images
	/header
		...
	/footer
		...
	/plugins
		/jquery.fancybox
			...			
		...						
	/ui
		/icons
			...
		/buttons
			...
	/temp
		temp-informer100x100.gif
		temp-banner768x60.png				
/js
	/project
		jquery.project_mySuperPlugin.js
		jquery.project_myOtherPlugin.js
		...
	jquery-1.7.2.min.js 
	...
	jquery.fancybox-1.3.4.js 
	jquery.fancybox-1.3.4.pack.js 
	...
/templates
	/layout
		header.php
		footer.php
	/blocks
		main_news.php
		user_profile-links.php
		...
	/pages
		page_main.php
		page_user.php
		page_about.php
		...
index.php
favicon.ico
robots.txt
```

В `robots.txt` удобно положить следующее, чтобы запретить индексирование поисковиками на случай, если вёрстка окажется на публично доступном сервере:
	
```text
# No indexing for layout project
User-Agent: *
Disallow: /
```


## Инструменты

### Банальные 

- IDE\редактор по вкусу 
- Firefox Web Developer Toolbar и Firebug (либо другие подобные плагины)
- Набор целевых браузеров
- Мелкая автоматизация, например с помощью [пакетных файлов](http://snippets.crisp-studio.com/view/102/otkrytie-url-v-neskolkix-brauzerax-iz-komandnoj-stroki)

### Продвинутые

- Плагин [Zen Coding](http://code.google.com/p/zen-coding/) в IDE\редакторе
- [Fiddler Web Debugger](http://www.fiddler2.com/fiddler2/)
- Утилиты для комбинирования и сжатия, например [gzipit](http://code.google.com/p/gzipit/)
- CSS-препроцессоры ([LESS](http://lesscss.org/), [SASS](http://sass-lang.com/) и т.п.)

## Идеи для дальнейшей проработки
- Сейчас БЭМ-классы используются и в JavaScript. Наверное, стоит использовать отдельные?
- Есть ли какой-то способ использовать namespace'ы для тех jQuery-плагинов, для которых важно поддерживать chainable?
- Бывают ли случаи, когда без `style="display: none"` нельзя обойтись?
- Как интегрировать гайдлайны с фреймворками наподобие Twitter Bootstrap или jQuery Mobile?
- Обобщить использование media-queries для реализации концепции responsible design.