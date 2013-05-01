#operator!=
```cpp
namespace std {

  template <class T, class Container>
  bool operator!=(const stack<T, Container>& x, const stack<T, Container>& y);

}
```

##概要

<b>stack の非等値比較を行う。</b>



##戻り値

`x.c != y.c`

##例外



##計算量



##備考



##例

```cpp
#include <iostream>
#include <stack>

int main ()
{
  std::stack<int>  x;
  x.push(3);
  x.push(1);
  x.push(4);

  std::stack<int>  y;
  y.push(3);
  y.push(1);
  y.push(4);

  std::cout << std::boolalpha << (x != y) << std::endl;

  // x に要素を追加
  x.push(1);

  std::cout << std::boolalpha << (x != y) << std::endl;

}
```
* !=[color ff0000]
* !=[color ff0000]

###出力

```cpp
false
true
```

##参照

