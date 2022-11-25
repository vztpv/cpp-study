```c++
#include <iostream>
#include <vector>

class AAA {
public:
  AAA() = delete;
  AAA(int) { } // parameter name is omitted.
};

int main(void)
{
  std::vector<AAA> x; // no error
  //std::vector<AAA> y(10); // error - need default constructor.

  x.reserve(10); // no error 
  for (size_t i = 0; i < 10; ++i) {
    x.push_back(AAA(3)); // no error
  }

  return 0;
}
```
# cf) new - 1. memory allocation 2. call constructor
