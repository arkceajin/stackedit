* `const Bytes& a2 = func_a();` weird
* `Bytes a1 = func_a();` better
* `const Bytes& a2 = a;` right
* `Bytes a1 = a;` right

```
#include <chrono>
#include <ctime>
#include <cstddef>
#include <vector>
#include <iostream>

typedef uint8_t Byte;
typedef std::vector<Byte> Bytes;

#define benchmark(f)\
    {auto begin = std::chrono::steady_clock::now();  \
    for (int i = 0; i < 10000000; ++i) \
        f;  \
    auto now = std::chrono::steady_clock::now();    \
    auto elapsed = std::chrono::duration_cast<std::chrono::milliseconds>(now - begin);    \
    std::cout << "Cost of code is " << elapsed .count() << " milliseconds" << std::endl;}

Bytes func_a()
{
    Bytes a(10000);
    return a;
}

int main(void)
{
    Bytes a(10000);
    benchmark({
                  const Bytes& a2 = func_a();
              })
    benchmark({
                  Bytes a1 = func_a();
              })
    benchmark({
                  const Bytes& a2 = a;
              })
    benchmark({
                  Bytes a1 = a;
              })
    return 0;
}
```
