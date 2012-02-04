## О переводе ##

Это форк репозитория книги "The Little MongoDB Book" для перевода ее на русский язык.

Каталог `en` содержит оригинальный текст, каталог `ru` -- перевод. Буду рад помощи в работе.

## О книге ##

Маленькая Книга про MongoDB -- это бесплатная книга, представляющая MongoDB.

Эта книга была написана вскоре после создания [Интерактивного курса MongoDB](http://mongly.com). Книга и сайт дополняют друг друга.

Книгу написал [Karl Seguin](http://openmymind.net), при поддержке [Perry Neal](http://twitter.com/perryneal).

Если вам нравится эта книга, возможно, вы так же оцените [Маленькую книгу про Redis](http://openmymind.net/2012/1/23/The-Little-Redis-Book/).

## Лицензия ##

Этак книга распространяется свободно под [Attribution-NonCommercial 3.0 Unported license](<http://creativecommons.org/licenses/by-nc/3.0/legalcode>).

## Форматы ##
Книга написана на [markdown](http://daringfireball.net/projects/markdown/) и конвертируется в PDF с помощью [PanDoc](http://johnmacfarlane.net/pandoc/). Несколько LaTex-команд добавлены в разметку для правильного создания PDF (в основном, для титульного листа и чтобы главы начинались с новой страницы).

Шаблон LaTex использует [Lena Herrmann's JavaScript highlighter](http://lenaherrmann.net/2010/05/20/javascript-syntax-highlighting-in-the-latex-listings-package).

Форматы Kindle и ePub собираются с [PanDoc](http://johnmacfarlane.net/pandoc/). Для сборки выполните `make en/mongodb.mobi`.

## Сборка PDF ##
Мы используем слегка измененный шаблон <https://github.com/claes/pandoc-templates> для сборки PDF:

	#!/bin/sh
	paper=a4paper
	hmargin=3cm
	vmargin=3cm
	fontsize=11pt

	mainfont=Verdana
	sansfont=Tahoma
	monofont="Courier New"
	columns=onecolumn
	geometry=portrait
	nohyphenation=true


	markdown2pdf --xetex --template=template/xetex.template \
	-V paper=$paper -V hmargin=$hmargin -V vmargin=$vmargin \
	-V mainfont="$mainfont" -V sansfont="$sansfont" -V monofont="$monofont" \
	-V geometry=$geometry -V columns=$columns -V fontsize=$fontsize \
	-V nohyphenation=$nohyphenation --listings en/mongodb.markdown -o mongodb.pdf 

## Титульное изображение ##
Титульное изображение в формате PSD прилагается. Используемый шрифт -- [Comfortaa](http://www.dafont.com/comfortaa.font).
