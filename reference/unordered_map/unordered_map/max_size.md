#max_size
```cpp
size_type max_size() const noexcept;
```

##概要
格納可能な最大の要素数を取得する。


##戻り値
このコンテナに格納可能な最大の要素数


##例外
投げない。


##計算量
定数


##例
```cpp
#include <iostream>
#include <string>
#include <unordered_map>

int main()
{
  std::unordered_map<std::string, int> um;
  decltype(um)::size_type s = um.max_size();

  std::cout << s << std::endl;
}
```
* iostream[link /reference/iostream]
* string[link /reference/string.md]
* unordered_map[link /reference/unordered_map.md]

###出力例
```cpp
2305843009213693951
```

##バージョン
###言語
- C++11

###処理系
- [Clang](/implementation#clang.md): -
- [Clang, C++0x mode](/implementation#clang.md): 3.0, 3.1
- [GCC](/implementation#gcc.md): -
- [GCC, C++0x mode](/implementation#gcc.md): 4.4.7, 4.5.3, 4.6.3, 4.7.0
- [ICC](/implementation#icc.md): ?
- [Visual C++](/implementation#visual_cpp.md): ?

###備考
libstdc++ では、コンテナのアロケータ `allocator_type` にメンバ関数 `max_size` が無いとコンパイル時エラーが発生する。
（`allocator_type::max_size()` を `std::`[`allocator_traits`](/reference/memory/allocator_traits)`::`[`max_size`](/reference/memory/allocator_traits/max_size) 経由ではなく直接使用しているため。）


##参照
| | |
|-----------------------|----------------------------|
| [`empty`](./empty.md) | コンテナが空かどうかを判定 |
| [`size`](./size.md)   | 要素数の取得               |


