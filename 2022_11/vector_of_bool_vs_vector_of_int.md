
    std::vector<bool> vs std::vector<int>
  
```C++
#include <iostream>
#include <vector>
#include <ctime>
#include <string>

int main(void)
{
	constexpr size_t MAX = 10240000;

	{
		std::vector<int> vec;
		clock_t a = 0, b = 0;

		a = clock();
		vec.reserve(MAX);
		for (size_t i = 0; i < MAX; ++i) {
			vec.push_back(i % 2 == 0);
		}
		b = clock();
		std::cout << "int, push_back " << vec.size() << " " << b - a << "ms\n";
	}

	{
		std::vector<bool> vec;
		clock_t a = 0, b = 0;

		a = clock();
		vec.reserve(MAX);
		for (size_t i = 0; i < MAX; ++i) {
			vec.push_back(i % 2 == 0);
		}
		b = clock();
		std::cout << "bool, push_back " << vec.size() << " " << b - a << "ms\n";
	}

	{
		std::vector<bool> vec(MAX, false);
		clock_t a = 0, b = 0;

		a = clock();

		for (size_t i = 0; i < MAX; ++i) {
			vec[i] = (i % 2 == 0);
		}
		b = clock();
		std::cout << "bool, [idx] " <<  vec[0] + vec.back() << " " << b - a << "ms\n";
	}


	{
		std::vector<int> vec(MAX, 0);
		clock_t a = 0, b = 0;

		a = clock();

		for (size_t i = 0; i < MAX; ++i) {
			vec[i] = (i % 2 == 0);
		}
		b = clock();
		std::cout << "int, [idx] " << vec[0] + vec.back() << " " << b - a << "ms\n";
	}

	return 0;
}
```
