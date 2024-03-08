### Введение в std::array
Представленный в C++11, std::array — это фиксированный массив, который не распадается в указатель при передаче в функцию. std::array определяется в
заголовочном файле array, внутри пространства имен std. Объявление переменной
std::array следующее:
```cpp
#include <array>

std::array<int, 4> myarray; // объявляем массив типа int длиной 4
```
Подобно обычным фиксированным массивам, длина std::array должна быть
установлена во время компиляции. std::array можно инициализировать с
использованием списка инициализаторов или uniform-инициализации:
```cpp
std::array<int, 4> myarray = { 8, 6, 4, 1 }; // список инициализаторов
std::array<int, 4> myarray2 { 8, 6, 4, 1 }; // uniform-инициализация
```
В отличие от стандартных фиксированных массивов, в std::array вы не можете
пропустить (не указывать) длину массива:
```cpp
std::array<int, > myarray = { 8, 6, 4, 1 }; // нельзя, должна быть указана длина массива
```
Также можно присваивать значения массиву с помощью списка инициализаторов:
```cpp
std::array<int, 4> myarray;
myarray = { 0, 1, 2, 3 }; // ок
myarray = { 8, 6 }; // ок, элементам 2 и 3 присвоен нуль!
myarray = { 0, 1, 3, 5, 7, 9 }; // нельзя, слишком много элементов в списке
инициализаторов!
```
std::array поддерживает вторую форму доступа к элементам массива — 
функция `at()`, которая осуществляет проверку диапазона:
```cpp
std::array<int, 4> myarray { 8, 6, 4, 1 };
myarray.at(1) = 7; // элемент массива под номером 1 - корректный, присваиваем ему значение 7
myarray.at(8) = 15; // элемент массива под номером 8 - некорректный, получим ошибку
```
#### Размер и сортировка
С помощью функции `size()` можно узнать длину массива:
```cpp
#include <iostream>
#include <array>

int main()
{
	std::array<double, 4> myarray{ 8.0, 6.4, 4.3, 1.9 };
	std::cout << "length: " << myarray.size();
	return 0;
}
```
Результат:
`length: 4`

Поскольку std::array не распадается в указатель при передаче в функцию, то
функция size() будет работать, даже если её вызвать из другой функции:
```cpp
#include <iostream>
#include <array>

void printLength(const std::array<double, 4> &myarray)
{
	std::cout << "length: " << myarray.size();
}

int main()
{
	std::array<double, 4> myarray { 8.0, 6.4, 4.3, 1.9 };
	printLength(myarray);
	return 0;
}
```
Результат тот же:
`length: 4`

*`Правило: Всегда передавайте std::array в функции по обычной или по константной
ссылке.`*
Поскольку длина массива всегда известна, то циклы foreach также можно
использовать с std::array:
1. std::array<int, 4> myarray { 8, 6, 4, 1 };
2.
3. for (auto &element : myarray)
4.
std::cout << element << ' ';
Вы можете отсортировать std::array, используя функцию std::sort(), которая
находится в заголовочном файле algorithm:
```cpp
#include <iostream>
#include <array>
#include <algorithm> // для std::sort
int main()
{
	std::array<int, 5> myarray { 8, 4, 2, 7, 1 };
	std::sort(myarray.begin(), myarray.end()); // сортировка массива по возрастанию
	std::sort(myarray.rbegin(), myarray.rend()); // сортировка массива по убыванию

	for (const auto &element : myarray)
		std::cout << element << ' ';
	return 0;
}
```
Результат:
`1 2 4 7 8`
