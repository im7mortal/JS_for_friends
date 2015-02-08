Введение
=========



Многие вещи становятся понятны если воспринимать js как ешё одну абстракцию.

Много написано про асинхронность js, какая это больщая проблема. Но нигде не проясняется, что это и почему это пока не почитаешь исходников w3c.
Почему работает замыкание. Смысл объектов.
Чтобы понимать эти вещи нужно для начала просто принять как должное.
Что мы работаем в песочнице с черным ящиком и мы слепы(пока:-)
Трудно понять зачем нужны все эти паттерны и соглашения, которыми грузят многие руководства с самого начала.


Для кого эта книга
---------------------

Для моих друзей!!! Они закончили технические вузы. В их курсах были программы по информатике,
но они закончились на этапе перебора двумерного массива.

Также он подойдет для любому кто понимает простейшие операции в программировании и хочет понять js.

Глава 1
=========

Сущность js.
------------


###JS интепретируемый язык.

JS это еще одна абстракция.Почему еще одна? Потому что вызов одной команды на js подразумевает кучу шаблонного кода на языке с,
который в свою очередь является абстракцией над языком ассеблер, который вообще никто не знает.

=>

- работает медленнее низкоуровневых языков

+ легче других языков (на самом деле + гигантский)

###JS не типизированный язык.

В низкоуровневых языках нужно обязательно при объявлении(создании) переменной указывать её тип.
```
string var = 'hello'; //  тип переменной var  строка(string)
```
И в дальнейшем переменная, тип которой был указан как строка, не сможет содержать данные любого другого типа(например чисел).

В JS переменная обьявлется единственным словом var, и в дальнейшем может содержать данные любого типа.

Важной особенность является, то что при арифметических операциях и операциях сравнения, переменные могут менять тип динамически.
Это может приводить к ошибкам при невнимательности.

=>

- работает медленнее( так как машина вынуждена делать дополнительные проверки для определения типа)

- может вызвать ошибки при неопытности.

+ легкость и быстрота написания кода

###JS ассинхронный язык.

Ассинхронный - выполняет не сколько действий одновременно. Не буду даваться в подробности реализации, в программирование
зачастую это означает, что на если есть две операции которые выполняются парралельно. То на самом деле они выполняются не
одновременно, вернее они выполняются в одном потоке(одно ядро процессора), но постоянно прерывают друг друга.

операция1---->...........------>.................----->конец

операция2.....---------->.......---------------->......------------------->конец

В других языках мы сами указываем, когда нам нужно вышеприведенное поведение.
Но в JS оно по умолчанию. Это очень важно так как, если бы все операции шли последовательно,
то команды пользователя обрабатывались бы с существенной задержкой(когда до них дойдет очередь).

## Про песочницу и чёрный ящик
Представьте что  вы в гостях у иностранца и просите на его языке принести вам чай.
Вести себя как дома вы не можете.
Так и JS работает в среде браузера. Ты как бы приходите в гости в операционную систему пользователя,
но не можете выйти за пределы браузера(из за соображений безопасности). Это состояние называется песочницей.
Вы можете играться, запустить опасный код но за пределы песочницы он не выйдет и вреда не насет.

Для того чтобы как то влиять на ситуацию вы говорите с иностранцем на его языке(скрипт JS) и в зависимости
от того как он тебя понял, он выполняет некоторые действия. В браузере этим иностранцем будет глобальный объект window(чёрный ящик).
Мы будем постоянно к нему обращаться, просить что-нибудь делать.

JS работает внутри браузера(песочница) работает с api браузера (черный ящик).

##Где можно применить JS/ Песочницы

На сервере node.js и io.js.
На клиенте - любой браузер.

##Кроссбраузерность
Мы не будем рассматривать эксцентричное поведение некоторых браузеров.

##Новшества
Мы будем рассматривать экспериментальные элементы языка, которые уже доступны в прогрессивных браузерах.
Я буду акцентировать на этом внимание.



Песочниц для js большое множество.
Их можно разделить на 2 вида.
Серверные(мимими) node.js и io.js(совсем недавно)
Клиентские(любой браузер). Ужасный ужас. Раньше был. Сейчас кроссбраузерная война закончилась, но
недопонятки между ними ещё встречаются.
Настоящая проблема это совместимость со старыми версиями браузеров.
В то время как из за взрыва популярности js
Многие плюшки которые будут рассказаны далее, не поддерживаются в более старых версиях браузеров.
Это ужасный ужас сейчас.


## Требования
Я подразумеваю, что ты уже знаешь циклы и условия, и прочие элементарные операции одинаковые во всех языках.
Мы будем изучать только особенности языка.

##Подготовка песочницы

Для упражнений нам понадобится песочница(браузер). Я надеюсь твой подойдет.

1. Открываем браузер.
2. Жмем F12 (стандартный вызов инструментов разработчика)
3. Ищем вкладку console(консоль).Открываем.
4. Ищем строку в которую можем ввести текст.
5. Вводим строку
>console.log('hello world!!!');
6. Появится строка
>hello world!!!
7. Можно начинать!!!

##Примитивы

1. Число:						1, 0.1;
2. Строка:						'Hello World!';
3. Логическое значение: 		true или false

##Переменные

В js переменные обьвляютс (создаются) ключевым словом var.
js не типизированный язык и в созданную переменную можно помещать любое значение.

```
var i = 0;
	i = true;
	i = 'Hello world!!!';
```

##Обьекты

Главный кирпичики построения скрипта js - это обьекты. В js всё является объектом.
Пока будем придерживаться понятия, что обьект -
это что-то что имеет свойства(некие значения, возможно вложенные обьекты или примитивы)
и как-то реагирует на вызовы некоторых свойств, которые мы назовем методы.

В браузере есть главный обьект window (тот самый чёрный ящик из введения). Рассмотрим этот обьект.

Откройте консоль и наберите

>window

В консоль выведется js обьект.
Если последовательно выбирать вложенные свойства, то возникает ассоциация с файловой системой.

Например путь к рабочему столу в ОС Microsoft Windows

>c/users/userName/Desktop

Путь к константе числа Пи содержащейся в обьекте Math который принадлежит непосредственно обьекту window.
Кстати введите этот путь в консоль.

>window.Math.PI

Представим что обьекты - это папки. Входя в папку мы видим другие папки, в которые тоже можем войти.
В папках есть и другие файлы, которые можно ассоциировать со свойствами обьекта. А программы - с методами.

Так и в обьектной модели браузера. Вызывая обьект мы получаем доступ к вложенным обьектам,
а также к свойствам и методам.

## Практика. Объкты.

Если вы не поиграли с объектом window - живо играть!

1) Изучите какие ещё константы содержит объект Math

2) Выведите по очереди два свойства

>window.innerHeight // высота видимой части страницы

>window.innerWidth // ширина видимой части страницы

Измените размер окна браузера и повторите ввод.


##Сборщик мусора

Обьект занимает какую то область в памяти компьютера и если неудалять ненужные обьекты,
то легко можно "уронить" браузер.

В js память освобождается автоматически сборщиком мусора(garbage collector, GK далее)

Момент вызова GK зависит от браузера и нам не подвластен(мы же помним что мы находимся в песочнице).
GK анализирует состояние и уничтожает ненужные обьекты.

Нам важно понимать как GK понимает, что можно уничтожать, а что нет. Это к счастью не секрет.

Вернемся к нашей ассоциации с файловой системой.

Если мы не можем войти в какую то папку двигаясь из корневой папки, то смысла в ней нет,
соответсвенное её можно уничтожить.

Так и в обьектной модели браузера. Если из обьекта window последовательно двигаясь нельзя добраться  до объекта,
значить до него вообще нельзя добраться и GK уничтожает его.

##Функции

Как уже говорилось раньше в js всё является объектом. Особым случаем является обьект function.
Для создания этого обьекта есть несколько способов.

№1. Создаем используя ключевое слово function и имя функции. В данном примере имя функции func.
В () указываем переменные, которые мы ожидаем получить. В данном случае a.
```
function func (a) {
	var b = 'Hello ';
	return b + a;
}
```
Ключевое слово return это то что вернет(отдаст) функция после вызова.В данном случаае строковый прмитив 'Hello '

Вызываем. Имя функции и (то что мы хотим передать функции).
```
func('world')
```
Метод обьекта это свойство которое содержит в себе функцию.

# Практика. Функции.

Вернемся к обьекту window.Math
1) Вызовите метод

>window.Math.random() // случайное число

2)А теперь напишем функцию возвращающую случайное число от 0 до 9

```
function getRandom() {
	return window.Math.floor(window.Math.random() * 10)
}
getRandom()
```
Вы уже догадались, что делает функция window.Math.floor?

##Объект console и метод console.log.

Обьект которым вы будете больше всего пользоваться. А конкретнее методом console.log().
Данный метод выводит данные, передаваемые в него во время выполнения скрипта.

```
var a = 'Hello';
console.log(a);
console.log('world!!!');
```

Метод не заменим при отладке скрипта. У обекта console есть и другие методы,
но они не важны на данном этапе.

##Области видимости

Область видимости это обьект который содержит переменные которые недоступные вне его.

```
function () {
	var t = 'hello';
	console.log(t) // hello
}
console.log(t) //ReferenceError: t is not defined
```

В js области видимости задаются, как вы уже наверно догадались, границами функции.

```
// глобальная область видимости
function() {
	// вот здесь новая область видимости (локальная)
	function() {
		// также новая область видимости
	}
}
```
Умение управлять
В понимании областей видимости.
В сложный скрипт состоящий из нескольких скриптов полезно разделять на области видимости.

В версии es6 добавили новое ключевое слово let это синоним var.
Отличие в том что область видимости var ограничевается function(){}, а let любым блоком {}.

```
var a = true;
{
	let a = false;
	console.log(1, a);
}
console.log(2, a);
```
##Область видимости во время выполнения функции

При каждом новом вызове функции:

1. Создаётся область видимости(контекст исполнения функции, далее контекст).
Это короткоживущий обьект, который ссылается на window через обьект функции.
2. Функции доступны данные из контекста.
3. После выполнения - ссылка на контекст удаляется, он становится недостижимым из обьекта window.
4. GK уничтожает контекст.

##Анонимные функции


№2. Обьявлеем функцию ключевым словом function без имени.
При этом функция должна присваиваться переменной

Объявление.
```
var func = function (a) {
		return a;
	}
```
Правая часть присвоения ни что иное как анонимная функция.

Вызов
```
func('hello')
```

Главное достоинство анонимных функций - это возможность динамического создания областей видимости.
Например с помощью функций высшего порядка (функции возвращающие(создающие) другие функции).

```
var func = function (a) {
		return function () {
					return a;
				}
	}

var a = func('hello');

a()
```
Подробнее про функций высшего порядка в следующей главе.

##Замыкание

[Области видимости](https://github.com/im7mortal/JS_for_friends#%D0%9E%D0%B1%D0%BB%D0%B0%D1%81%D1%82%D0%B8-%D0%B2%D0%B8%D0%B4%D0%B8%D0%BC%D0%BE%D1%81%D1%82%D0%B8) и [сборщик мусора](https://github.com/im7mortal/JS_for_friends#%D0%A1%D0%B1%D0%BE%D1%80%D1%89%D0%B8%D0%BA-%D0%BC%D1%83%D1%81%D0%BE%D1%80%D0%B0) создают замыкания(не совсем так, но допустим).

Жизненный цикл обычной функции описан в ["Область видимости во время выполнения функции"](https://github.com/im7mortal/JS_for_friends#%D0%9E%D0%B1%D0%BB%D0%B0%D1%81%D1%82%D1%8C-%D0%B2%D0%B8%D0%B4%D0%B8%D0%BC%D0%BE%D1%81%D1%82%D0%B8-%D0%B2%D0%BE-%D0%B2%D1%80%D0%B5%D0%BC%D1%8F-%D0%B2%D1%8B%D0%BF%D0%BE%D0%BB%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F-%D1%84%D1%83%D0%BD%D0%BA%D1%86%D0%B8%D0%B8)

```
function func() {
	var hello = 'hello';
	console.log(hello)
}

func()
```
После выполнения функции контекст теряет связь с глобальным объектом window,
следовательно и все переменные обьявленные в этом контексте тоже теряют связь.
GK уничтожает контекст и мы уже не можем получить данные из него.

А теперь замыкание!!!
```
function closure(a) {
	return function (v) {
		return a + 5 + v
	}
}

var b = closure(7);
```

В переменную b присвоилась анонимная функция, которая ссылается на данные в контексте функции closure.
Так как на контекст closure остались ссылки из window, GK не может уничтожить контекст. Та-да-м-ммм!!!
Это и называется замыканием.
```
console.log(b(8));
console.log(b(100));
```

1. Создаётся область видимости(контекст исполнения функции, далее контекст).
2. Функции доступны данные из контекста.
3. После выполнения(функция) - ссылка на контекст удаляется, он становится недостижимым из обьекта window.
4. GK уничтожает контекст.

Вы полюбите этот гибкий механизм с практикой.

##Применение замыкания

Замыкание применяется для настройки
эт все
пример инкапсуляции
function() {
	var g = 2;
	return function (go) {
		return go/g;
	}
}

мы не можем получить g ни как!!!


Если на обьект не остается ссылок его уничтожает gk. Прикол замыкания в том что из функции можно вернуть функцию


##Начинаем строить web-приложение.
Современное веб приложение состоит как правило из трех компонент.

html это скелет приложения. На него мы будем навешивать логику и красоту.

css это та

js это логика и движение



##Введение в html
html это разметка страицы, её скелет. В отличии от js и css html код должен распологаться в отдельном файле
с расширением .html

Минимум
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>

	</body>
</html>
```
# Практика. html.
Создайте файл, например блокнота. Поменяйте вручную расширение на .html

Вставьте следующий код:

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<div>
			Hello world!!!
		<div>
	</body>
</html>
```
Это все тот же шаблон, но с элементом <div> содержащим текст "Hello world!!!".
Это самый распространенный элемент. Он обозначает блок.

##Введение в css

css это внешний вид элемента.Код css можно встраивать в html внутри тега <style>
или распологать в отдельном файле с расширением .css




##ООП


##Наследование

Один из столпов ООП.
Когда обьекты созданные по подобию какого нибудь обьекта имеют доступ ко всем его свойствам и методам.





Глава 2
=========
