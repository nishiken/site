#pow
```cpp
namespace std {
  float pow(float x, float y);

  double pow(double x, double y);

  long double pow(long double x, long double y);

  template<class Arithmetic1, class Arithmetic2>
  Promoted pow(Arithmetic1 x, Arithmetic2 y);   // C++11

  float pow(float x, int y);                    // C++03 only
  double pow(double x, int y);                  // C++03 only
  long double pow(long double x, int y);        // C++03 only
}
```
* Promoted[italic]

##概要
`x` の `y` 乗を求める。


##戻り値
`x` を `y` 乗した値を返す。


##備考
![](https://github.com/cpprefjp/image/raw/master/reference/cmath/pow/pow.png)


##例
```cpp
#include <cmath>
#include <limits>
#include <iostream>

int main() {
  std::cout << std::fixed;
  std::cout << "pow(2.0, +∞)  = "
            << std::pow(2.0, std::numeric_limits<double>::infinity())
            << std::endl;
  std::cout << "pow(2.0, 2.0)  = " << std::pow(2.0, 2.0) << std::endl;
  std::cout << "pow(2.0, 1.0)  = " << std::pow(2.0, 1.0) << std::endl;
  std::cout << "pow(2.0, 0.5)  = " << std::pow(2.0, 0.5) << std::endl;
  std::cout << "pow(2.0, 0.0)  = " << std::pow(2.0, 0.0) << std::endl;
  std::cout << "pow(2.0, -0.5) = " << std::pow(2.0, -0.5) << std::endl;
  std::cout << "pow(2.0, -1.0) = " << std::pow(2.0, -1.0) << std::endl;
  std::cout << "pow(2.0, -2.0) = " << std::pow(2.0, -2.0) << std::endl;
  std::cout << "pow(2.0, -∞)  = "
            << std::pow(2.0, -std::numeric_limits<double>::infinity())
            << std::endl;
}
```

###出力
```
pow(2.0, +∞)  = inf
pow(2.0, 2.0)  = 4.000000
pow(2.0, 1.0)  = 2.000000
pow(2.0, 0.5)  = 1.414214
pow(2.0, 0.0)  = 1.000000
pow(2.0, -0.5) = 0.707107
pow(2.0, -1.0) = 0.500000
pow(2.0, -2.0) = 0.250000
pow(2.0, -∞)  = 0.000000
```

##バージョン
###言語
- C++03
- C++11

###処理系
- [Clang](/implementation#clang.md): 1.9, 2.9, 3.1
- [GCC](/implementation#gcc.md): 3.4.6, 4.2.4, 4.3.5, 4.4.5, 4.5.1, 4.5.2, 4.6.1, 4.7.0
- [GCC, C++0x mode](/implementation#gcc.md): 4.3.4, 4.4.5, 4.5.2, 4.6.1, 4.7.0
- [ICC](/implementation#icc.md): 10.1, 11.0, 11.1, 12.0
- [Visual C++](/implementation#visual_cpp.md) 7.1, 8.0, 9.0, 10.0

####備考
特定の環境で `constexpr` 指定されている場合がある。（独自拡張）
- GCC 4.6.1 以上


##実装例
`exp` および `log` があれば、以下のように変換することで求められる。

![](https://raw.github.com/cpprefjp/image/master/reference/cmath/pow/pow_formula.png)

ただし `x` が負数かつ `y` が整数に等しい場合などについては、別に計算する必要がある。

