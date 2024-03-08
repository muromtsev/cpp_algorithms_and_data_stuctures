### std::string
#### Тип данных string
Чтобы иметь возможность использовать строки в C++, сначала нужно подключить
заголовочный файл string. Как только это будет сделано, мы сможем определять
переменные типа string:
```cpp
#include <string>
// ...
std::string name;
// ...
```
Как и с обычными переменными, мы можем инициализировать переменные типа
string или присваивать им значения:
```cpp
std::string name("Sasha"); // инициализируем переменную name строковым литералом "Sasha"
name = "Masha"; // присваиваем переменной name строковый литерал "Masha"
```

Чтобы извлечь полную строку из входного потока данных (вместе с пробелами),
используйте функцию ``std::getline()``. Она принимает два параметра: первый —
std::cin, второй — переменная типа string.
Вот программа, приведенная выше, но уже с использованием std::getline():
```cpp
#include <iostream>
#include <string>

int main()
{
	std::cout << "Enter your full name: ";
	std::string myName;
	std::getline(std::cin, myName); // полностью извлекаем строку в переменную
	myName
	std::cout << "Enter your age: ";
	std::string myAge;
	std::getline(std::cin, myAge); // полностью извлекаем строку в переменную	myAge
	std::cout << "Your name is " << myName << " and your age is " << myAge;
	
	return 0;
}
```
Теперь работает как надо:

```Enter your full name: Sasha Mak```
```Enter your age: 25```
```Your name is Sasha Mak and your age is 25```

Хорошей практикой является удалять из входного потока данных символ новой
строки. Это можно сделать следующим образом:
```cpp
std::cin.ignore(32767, '\n'); // игнорируем символы перевода строки "\n" во входящем потоке длиной 32767 символов
```
*``Правило: При вводе числовых значений не забывайте удалять символ новой
строки из входного потока данных с помощью std::cin.ignore().``*

#### Длина строк
Чтобы узнать длину строки, мы можем сделать следующее:
```cpp
#include <iostream>
#include <string>

int main()
{
	std::string myName("Sasha");
	std::cout << myName << " has " << myName.length() << " characters\n";
	return 0;
}
```
Результат выполнения программы:
``Sasha has 5 characters``

