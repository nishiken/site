#epsilon
```cpp
// C++03
static const T epsilon() throw();

// C++11
static constexpr T epsilon() noexcept;
```

##概要
機械イプシロンを取得する。  
これは浮動小数点数の比較のために誤差幅を評価するのに使用できる。  

対応するマクロを次の表に挙げる。

| 型            | 対応するマクロ                                      |
|---------------|-----------------------------------------------------|
| `float`       | [`FLT_EPSILON`](/reference/cfloat/flt_epsilon.md)   |
| `double`      | [`DBL_EPSILON`](/reference/cfloat/dbl_epsilon.md)   |
| `long double` | [`LDBL_EPSILON`](/reference/cfloat/ldbl_epsilon.md) |


##例
```cpp
#include <iostream>
#include <cmath>
#include <limits>

int main()
{
  constexpr double e = std::numeric_limits<double>::epsilon();

  std::cout << e << std::endl;

  double a = 0.6 - 0.4;
  double b = 0.2;
  if (std::abs(a - b) < e) {
    std::cout << "equal" << std::endl;
  }
  else {
    std::cout << "not equal" << std::endl;
  }
}
```
* epsilon[color ff0000]

###出力
```
2.22045e-016
equal
```

##参照
* [C++ FAQ - Why doesn't my floating-point comparison work?](http://www.parashift.com/c++-faq-lite/floating-point-arith.html)


