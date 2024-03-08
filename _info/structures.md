## Структуры

### Объявление и определение структур
Поскольку структуры определяются программистом, то вначале мы должны
сообщить компилятору, как она вообще будет выглядеть. Для этого используется
ключевое слово struct:
```cpp
struct Employee
{
	short id;
	int age;
	double salary;
 };
```
### Доступ к членам структур
Когда мы объявляем переменную структуры, например, Employee john , то
john ссылается на всю структуру. Для того, чтобы получить доступ к отдельным её
членам, используется оператор выбора члена (.). Например, в коде, приведенном
ниже, мы используем оператор выбора членов для инициализации каждого члена
структуры:
```cpp
Employee john; // создаем отдельную структуру Employee для John-а
john.id = 8; // присваиваем значение члену id структуры john
john.age = 27; // присваиваем значение члену age структуры john
john.salary = 32.17; // присваиваем значение члену salary структуры john

Employee james; // создаем отдельную структуру Employee для James-а
james.id = 9; // присваиваем значение члену id структуры james
james.age = 30; // присваиваем значение члену age структуры james
james.salary = 28.35; // присваиваем значение члену salary структуры james
```
### Инициализация структур
```cpp
struct Employee
{
	short id;
	int age;
	double salary;
};
Employee john = { 5, 27, 45000.0 }; // john.id = 5, john.age = 27, john.salary = 45000.0
Employee james = { 6, 29}; // james.id = 6, james.age = 29, james.salary = 0.0 (инициализация по умолчанию)```
```
В C++11 также можно использовать uniform-инициализацию:

```cpp
Employee john { 5, 27, 45000.0 }; // john.id = 5, john.age = 27, john.salary = 45000.0
Employee james { 6, 29 }; // james.id = 6, james.age = 29, james.salary = 0.0 (инициализация по умолчанию)
```
### C++11/14: Инициализация нестатических членов структур
В C++11 добавили возможность присваивать нестатическим (обычным) членам
структуры значения по умолчанию. Например:
```cpp
#include <iostream>

struct Triangle
{
	double length = 2.0;
	double width = 2.0;
};

int main()
{
	Triangle z; // длина = 2.0, ширина = 2.0
	z.length = 3.0; // вы также можете присваивать членам структуры и другие значения

	return 0;
}
```
### Присваивание значений членам структур
```cpp
struct Employee
{
	short id;
	int age;
	double salary;
};
Employee john;
john = { 5, 27, 45000.0 }; // только C++11
```

### Структуры и функции
```cpp
#include <iostream>

struct Employee
{
	short id;
	int age;
	double salary;
};

void printInformation(Employee employee)
{
	std::cout << "ID: " << employee.id << "\n";
	std::cout << "Age: " << employee.age << "\n";
	std::cout << "Salary: " << employee.salary << "\n";
}

int main()
{
	Employee john = { 21, 27, 28.45 };
	Employee james = { 22, 29, 19.29 };

	// Выводим информацию о John-е

	printInformation(john);
	std::cout << "\n";
	// Выводим информацию о James-е
	printInformation(james);
	return 0;
}
```

### Вложенные структуры
```cpp
struct Employee
{
	short id;
	int age;
	double salary;
};
struct Company
{
	Employee CEO; // Employee - это структура внутри структуры Company
	int numberOfEmployees;
};

Company myCompany;
```
