#swap
```cpp
void swap(forward_list& x);
```

##概要
他の`forward_list`オブジェクトと値を入れ替える。


##効果
`*this`の内容を`x`と交換する。


##戻り値
なし


##計算量
定数時間


##例
```cpp
#include <iostream>
#include <forward_list>
#include <algorithm>

int main()
{
  std::forward_list<int> ls1 = {1, 2, 3};
  std::forward_list<int> ls2 = {4, 5, 6};

  ls1.swap(ls2);

  std::for_each(ls1.begin(), ls1.end(), [](int x) {
    std::cout << x << std::endl;
  });

  std::cout << std::endl;

  std::for_each(ls2.begin(), ls2.end(), [](int x) {
    std::cout << x << std::endl;
  });
}
```
* swap[color ff0000]

###出力
```
4
5
6

1
2
3
```

##バージョン
###言語
- C++11

###処理系
- [Clang](/implementation#clang.md): ??
- [GCC](/implementation#gcc.md): 
- [GCC, C++0x mode](/implementation#gcc.md): 4.7.0
- [ICC](/implementation#icc.md): ??
- [Visual C++](/implementation#visual_cpp.md) ??


##参照


