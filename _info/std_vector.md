### Векторы
Представленный в C++03, std::vector (или просто "вектор") — это тот же
динамический массив, но который может сам управлять выделенной себе памятью.
Это означает, что вы можете создавать массивы, длина которых задается во время
выполнения, без использования операторов new и delete (явного указания
выделения и освобождения памяти). std::vector находится в заголовочном файле
vector. Объявление std::vector следующее:
```cpp
#include <vector>
// Нет необходимости указывать длину при инициализации
std::vector<int> array;
std::vector<int> array2 = { 10, 8, 6, 4, 2, 1 }; // используется список инициализаторов для инициализации массива
std::vector<int> array3 { 10, 8, 6, 4, 2, 1 }; // используется uniform-инициализация для инициализации массива (начиная с C++11)
```
#### Длина векторов
В отличие от стандартных динамических массивов, которые не знают свою длину,
std::vector свою длину запоминает. Чтобы её узнать, нужно использовать функцию
`size()`:
```cpp
#include <vector>
#include <iostream>

int main()
{
	std::vector<int> array { 12, 10, 8, 6, 4, 2, 1 };
	std::cout << "The length is: " << array.size() << '\n';
	return 0;.
}
```
Результат:
`The length is: 7`
Изменить длину стандартного динамически выделенного массива довольно
проблематично и сложно. Изменить длину std::vector так же просто, как вызвать
функцию resize():
```cpp
#include <vector>
#include <iostream>

int main()
{
		std::vector<int> array { 0, 1, 2 };
		array.resize(7); // изменяем длину array на 7
		std::cout << "The length is: " << array.size() << '\n';

	for (auto const &element: array)
		std::cout << element << ' ';

	return 0;
}
```
Результат:
`The length is: 7`
`0 1 2 0 0 0 0`

Длину вектора также можно изменить и в обратную сторону (обрезать):
```cpp
#include <vector>
#include <iostream>

int main()
{
		std::vector<int> array { 0, 1, 4, 7, 9, 11 };
		array.resize(4); // изменяем длину array на 4
		std::cout << "The length is: " << array.size() << '\n';

	for (auto const &element: array)
		std::cout << element << ' ';
	return 0;
 }
 ```
Результат:
`The length is: 4`
`0 1 4 7`


Длина в std::vector — это количество фактически используемых элементов.
Ёмкость (или "вместимость") в std::vector — это количество выделенных
элементов.
используя функцию **capacity()**:
```cpp
#include <iostream>
#include <vector>

int main()
{
	std::vector<int> array { 0, 1, 2, 3};
	array.resize(6); // устанавливаем длину, равную 6
	std::cout << "The length is: " << array.size() << '\n';
	std::cout << "The capacity is: " << array.capacity() << '\n';
	return 0;
}
```
Результат на моем компьютере:
`The length is: 6`
`The capacity is: 6`

#### std::vector в качестве стека

**функция push_back()** — добавляет элемент в стек;
**функция back()** — возвращает значение верхнего элемента стека;
**функция pop_back()** — вытягивает элемент из стека.
Например:
```cpp
#include <iostream>
#include <vector>

void printStack(const std::vector<int> &stack)
{
	for (const auto &element : stack)
	std::cout << element << ' ';
	std::cout << "(cap " << stack.capacity() << " length " << stack.size() << ")\n";
}

int main()
{
	std::vector<int> stack;
	
	stack.reserve(7); // устанавливаем ёмкость (как минимум), равную 7
	
	printStack(stack);
	
	stack.push_back(7); // функция push_back() добавляет элемент в стек
	printStack(stack);
	
	stack.push_back(4);
	printStack(stack);
	
	stack.push_back(1);
	printStack(stack);
	
	std::cout << "top: " << stack.back() << '\n'; // функция back() возвращает последний элемент
	
	stack.pop_back(); // функция pop_back() вытягивает элемент из стека
	printStack(stack);
	
	stack.pop_back();
	printStack(stack);
	
	stack.pop_back();
	printStack(stack);
	
	return 0;
}
```
Результат выполнения программы:
`(cap 0 length 0)`
`7 (cap 1 length 1)`
`7 4 (cap 2 length 2)`
`7 4 1 (cap 3 length 3)`
`top: 1`
`7 4 (cap 3 length 2)`
`7 (cap 3 length 1)`
`(cap 3 length 0)`
Поскольку изменение размера вектора является затратной операцией, то мы
можем сообщить вектору выделить заранее заданный объем ёмкости, используя
функцию reserve()
