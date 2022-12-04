```c++
#include <iostream>
#include <vector>
#include <ctime>

class AAA {
public:
	virtual ~AAA() {}
	virtual int f() = 0;
};

class BBB : public AAA {
public:
	virtual int f() {
		return 1;
	}
};

class CCC : public AAA {
public:
	virtual int f() {
		return 2;
	}
};


class DDD {
public:
	int f() {
		return 1;
	}
};

class EEE {
public:
	int f() {
		return 2;
	}
};

class FFF {
public:
	union {
		DDD* ddd;
		EEE* eee;
	};
	int type;

	FFF(DDD* ddd) : ddd(ddd) {
		type = 0;
	}

	FFF(EEE* eee) : eee(eee) {
		type = 1;
	}

	int f() {
		if (type) {
			return eee->f();
		}
		else {
			return ddd->f();
		}
	}
};

int main(void)
{
	std::cout << sizeof(BBB) << " " << sizeof(CCC) << "\n";
	std::cout << sizeof(FFF) << "\n";
	
	{

		int a, b;
		int sum = 0;
		std::vector<FFF> test;
		test.reserve(10240000);

		a = clock();
		for (int i = 0; i < 10240000; ++i) {
			test.push_back(i % 2 == 0 ? FFF(new DDD) : FFF(new EEE));
		}
		b = clock();
		std::cout << b - a << "ms\n";

		a = clock();
		for(int t=0; t < 100; ++t)
		for (int i = 0; i < 10240000; ++i) {
			sum += test[i].f();
		}
		b = clock();
		std::cout << b - a << "ms\n";
		std::cout << "sum " << sum << "\n";
	}	{
		int a, b;
		int sum = 0;
		std::vector<AAA*> test;
		test.reserve(10240000);

		a = clock();
		for (int i = 0; i < 10240000; ++i) {
			test.push_back(i % 2 == 0 ? (AAA*) new BBB : (AAA*) new CCC);
		}
		b = clock();
		std::cout << b - a << "ms\n";

		a = clock();
		for (int t = 0; t < 100; ++t)
		for (int i = 0; i < 10240000; ++i) {
			sum += test[i]->f();
		}
		b = clock();
		std::cout << b - a << "ms\n";
		std::cout << "sum " << sum << "\n";
	}
	{
		int a, b;
		int sum = 0;
		std::vector<FFF> test;
		test.reserve(10240000);

		a = clock();
		for (int i = 0; i < 10240000; ++i) {
			test.push_back(i % 2 == 0 ? FFF(new DDD) : FFF(new EEE));
		}
		b = clock();
		std::cout << b - a << "ms\n";

		a = clock();
		for (int i = 0; i < 10240000; ++i) {
			sum += test[i].f();
		}
		b = clock();
		std::cout << b - a << "ms\n";
		std::cout << "sum " << sum << "\n";
	}
	return 0;
}

```
