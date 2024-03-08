#### Введение в класс std::string_view
В отличие от объектов класса std::string, которые хранят свою собственную копию
строки, класс `std::string_view` обеспечивает представление (англ. "view") для
заданной строки, которая может быть определена где-нибудь в другом месте.
```cpp
#include <iostream>
#include <string_view>
int main()
{
	std::string_view text{ "hello" }; // представление для строки "hello", которое хранится в бинарном виде
	std::string_view str{ text }; // представление этой же строки - "hello"
	std::string_view more{ str }; // представление этой же строки - "hello"

	std::cout << text << ' ' << str << ' ' << more << '\n';

	return 0;
}
```
```cpp
#include <iostream>
#include <string_view>

int main()
{
	std::string_view str{ "Trains are fast!" };
	std::cout << str.length() << '\n'; // 16
	std::cout << str.substr(0, str.find(' ')) << '\n'; // Trains
	std::cout << (str == "Trains are fast!") << '\n'; // 1

	// Начиная с C++20
	std::cout << str.starts_with("Boats") << '\n'; // 0
	std::cout << str.ends_with("fast!") << '\n'; // 1

	std::cout << str << '\n'; // Trains are fast!

	return 0;
}
```
*`Совет: Используйте std::string_view вместо строк C-style. Для строк, которые не
планируете изменять в дальнейшем, предпочтительнее использовать класс
std::string_view вместо std::string.`*
