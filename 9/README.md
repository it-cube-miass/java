Массив – это упорядоченная совокупность, или пронумерованный список значений, ссылка на который выполняется по общему имени. Это могут быть как примитивные значения, так и объекты или даже другие массивы, однако все значения массива должны принадлежать одному типу. Тип массива идентичен типу содержащихся в нем значений.

Массивы относятся к ссылочным типам данных, собственно как и все остальные типы, кроме примитивных. Напомню еще раз, что в Java все является объектом, исключение составляют лишь примитивные типы.

Массивы могут быть одномерными и многомерными.

Процесс создания массива можно разделить на три этапа:
- Объявление (declaration)
- Создание (instantation)
- Инициализация  (initialization)

## Объявление массива 
На этом этапе определяется только переменная типа ссылка (reference) на массив, содержащая тип массива. Для этого записывается имя типа элементов массива, квадратными скобками указывается, что объявляется ссылка на массив, а не простая переменная, и перечисляются имена переменных ссылочного типа, например:
```java
int[] numbers; // numbers ссылка на массив int-ов
String[] strings; // strings ссылка на массив строк
byte[][] twoBytes; // twoBytes ссылка на двумерный массив байтов
char[] letters, digits; //letters и digits ссылки на массивы символов
```
По существу объявление массивов, точно такая же операция как и объявление любых других типов данных, правда имеющая немного свой синтаксис, так как это все таки массивы.

Java поддерживает еще один синтаксис объявления переменных типа массив, обеспечивающий совместимость с С и С++. Согласно этому синтаксису, одна или несколько пар квадратных скобок следуют за именем переменной, а не за именем типа:
```java
byte arrayOfBytes[]; // То же, что и byte[] arrayOfBytes
byte arrayOfArrayOfBytes[][]; // То же, что и byte[][] arrayOfArrayOfBytes
byte[] arrayOfArrayOfBytes[]; // То же, что и byte[][] arrayOfArrayOfBytes
```
Однако зачастую такой синтаксис сбивает с толку, поэтому его следует избегать. В следующем примере, легко спутать что имелось в виду:
```java
float rates[], maxRate; // может хотели объявить два массива?
```
Вообщем, так не делаем!. В соглашения по оформлению Java кода, рекомендуется синтаксис, который был приведен первым, то есть квадратные скобки следуют сразу за типом объявляемого массива.

Следует понимать, что операция объявления массива еще не создает массив, а только объявляет переменную являющуюся ссылкой на него, которую без инициализации нельзя использовать в программе, так как компилятор выдаст ошибку, что переменная массива не инициализирована.

Пока объявленная переменная массива не определена, она может содержать (если вы присвоите) значение null. И только после определения она будет содержать ссылку на конкретный объект.

Указать длину массива при объявлении переменной массива невозможно, поскольку размер является строго функцией объекта массива, а не ссылки на него.

Важно понимать разницу между ссылкой на массив (имя переменной массива) и самим массивом, то есть объектом, на который указывает эта ссылка.

## Создание массива
На этом этапе указывается количество элементов массива, называемое его размером, выделяется место для массива в оперативной памяти, переменной-ссылке присваивается оператором = адрес массива. Все эти действия производятся оператором new за которым следует тип элементов массива. Например:
```java
letters = new char[10]; // создали массив char-ов размеров в 10 элементов
```
Но стоит еще раз заметить, что до этого переменная letters, должна быть объявлена как массив. Чтобы было более понятно, это можно представить вот так:
```java
char[] letters; // объявили letters как ссылку на массив символов char
letters = new char[10]; // создали массив char-ов размеров в 10 элементов
```
При создании массива с таким синтаксисом все элементы массива автоматически инициализируются значениями по умолчанию. Это false для значений boolean, '\u0000'  для значений char, 0 для целых значений, 0.0 для значений с плавающей точкой и null для объектов или массивов.

В Java размер массива фиксирован. Созданный массив нельзя увеличить или уменьшить. Желаемый размер создаваемого массива задается неотрицательным целым числом. Но в любое время переменной типа массив может быть сопоставлен новый массив другого размера. То есть может быть присвоена ссылка на другой массив того же типа что и объявленная переменная.

Индексы массивов всегда начинаются с 0.

Первые две операции: объявление и создание массива можно объединить в один оператор. Например:
```java
char[] letters = new char[10];
```
Этот оператор эквивалентен двум приведенным выше.

После данной операции переменная letters будет уже содержать ссылку на массив и если попробовать вывести ее значение то мы получим значение, что то вроде ```[C@659e0bfd```. А все элементы массива, как уже говорилось будут содержать значения по умолчанию для объявленного типа.

Создать массив можно только при помощи оператора new, но ссылку на уже существующий массив можно присвоить другой ссылке того же типа. Например:
```java
int[] a = new int[4];
int[] b = a;
```
Но надо иметь в виду, что переменные a и b указывают на один и тот же массив. По началу это может сбивать с толку, но если помнить что мы имеем дело с ссылочными типами данных, то все становится на свои места. Если этот момент не понятен, то чуть позже мы все это разберем на примерах.

Следует, так же, еще раз упомянуть, что ссылке (переменной массива) можно присвоить "пустое" значение null, не указывающее ни на какой адрес оперативной памяти:
```java
a = null;
```
После этого массив, на который указывала данная ссылка, теряется, если на него не было других ссылок.

Размер или длину массива можно получить при помощи константы **length**, которая определена для каждого массива и возвращает его длину.

Можно создавать и использовать массивы нулевой длины (пустой массив). Например:
```java
boolean[] bits = new boolean[0];
```
Инициализировать такой массив нельзя, так как у него просто нет элементов которые можно инициализировать. Сразу же возникает вопрос, а зачем они тогда вообще нужны эти пустые массивы? Но они нужны и даже очень полезны!

Пустой массив принято использовать в тех местах программы, где заранее неизвестно, будут элементы или нет. Если элементы будут, то возвращается непустой массив, если элементов нет - пустой массив. Примером может служить массив строк который передается в метод ```main()``` и содержит аргументы командной строки, а если их нет, то возвращается пустой массив.

Пустой массив лучше, чем null, потому что не требует отдельного if-а для обработки. То же верно для списков и других коллекций.

## Инициализация массива
На этом этапе элементы массива получают начальные значения. Инициализировать элементы массива значениями можно несколькими способами:
- Присвоить каждому элементу массива конкретное значение (это можно сделать например в цикле, но до этого массив уже должен быть объявлен и создан)  
- Инициализировать массив при помощи перечисления значений его элементов в фигурных скобках (это можно сделать как на этапе объявления, так и на этапе создания, но синтаксис при этом разный)

Обращается к конкретному элементу массива можно по его индексу, который начинается с нуля, как это уже говорилось.

Индексы можно задавать любыми целочисленными выражениями, кроме типа long, например ```a[i + j]``` , ```a[i % 5]``` , ```a[++i]```. Исполняющая система Java следит за тем, чтобы значения этих выражений не выходили за границы длины массива. Если же выход все же произойдет интерпретатор Java в таком случае прекратит выполнение программы и выведет на консоль сообщение о выходе индекса массива за границы его определения *ArrayIndexOutOfBoundsException*.

Рассмотрим пример первого способа инициализации:
```java
int[] ar = new int[2];
ar[0] = 1;
ar[1] = 2;
```
Второй способ инициализации можно реализовать по разному.

Инициализацию массива можно совместить с этапом создания:
```java
int[] ar = new int[]{1,2}; // объявление, создание и инициализация массива
```
Так же инициализировать массив можно на этапе его объявления следующим синтаксисом:
```java
int[] ar = {1,2}; // объявление, создание и инициализация массива
```
Внимание! Этот синтаксис инициализации массива работает только при объявлении массива и совмещает сразу все три операции объявление, создание и инициализацию. Если массив уже объявлен, то такой синтаксис использовать нельзя. Компилятор выдаст ошибку. То есть:
```java
int[] ar; // объявление массива
ar = {1,2}; // ОШИБКА!!! создание и инициализация массива
```
Такое действо не прокатит.

Так же можно инициализировать на этапе объявления и чуть чуть по другому:

В Java предусмотрен синтаксис, который поддерживает анонимные массивы (они не присваиваются переменным и, следовательно, у них нет имен). Иногда массив нужно задействовать лишь один раз (например, передать его методу), следовательно, вы не хотите тратить время на присваивание его переменной, поэтому можно сразу же использовать результат оператора new. Например:
```java
System.out.println(new char[] {'H', 'e', 'l', 'l', 'o'});
```
Синтаксис инициализации массивов с помощью фигурных скобок называется литеральным, поскольку для инициализации используется массив-литерал.

Важно понимать что массивы-литералы создаются и инициализируются во время выполнения программы, а не во время ее компиляции. Рассмотрим следующий массив-литерал:
```java
int[] perfectNumbers = {6, 28};
```
Он компилируется в такой байт-код Java:
```java
int[] perfectNumbers = new int[2];
perfectNumbers[0] = 6;
perfectNumbers[1] = 28;
```
Поэтому если вам нужно разместить в Java программе много данных, лучше не включать их непосредственно в массив, поскольку компилятору Java придется создавать много байт-кода инициализации массива, а затем интерпретатору Java нужно будет кропотливо выполнять весь этот код. В таких случаях лучше сохранять данные во внешнем файле и считывать их в программу во время ее выполнения.

Однако тот факт, что Java инициализирует массив во время выполнения программы, имеет важные последствия. Это означает, что элементы массива-литерала являются произвольными выражениями, вычисляемыми во время выполнения программы, а не постоянными выражениями, вычисляемыми компилятором. Например:
```java
Point[] points = { circle1.getCenterPoint(), circle2.getCenterPoint() };
```
Теперь немножко попрактикуемся.
```java
public class Main {
    public static void main(String[] args) {

        int[] arr = new int[5];
        System.out.println(Arrays.toString(arr));

        for (int i = 0; i < arr.length; i++) {
            arr[i] = i;
        }
        System.out.println(Arrays.toString(arr));

        arr[2] = arr[2] * 10;
        arr[3] *= 10;
        System.out.println(Arrays.toString(arr));
    }
}
```
Данная программа генерирует следующий вывод:
```txt
[0, 0, 0, 0, 0]
[0, 1, 2, 3, 4]
[0, 1, 20, 30, 4]
```