#cbegin
```cpp
const_iterator cbegin() const noexcept;
```

##概要

先頭の要素を指す読み取り専用イテレータを取得する。
`unordered_multiset` は非順序連想コンテナであるため「先頭」に特に意味はないが、`cbegin()` で得られたイテレータを [`cend`](./cend.md)`()` まで `operator++()` でイテレートすることで当該コンテナの要素を漏れなくダブりなく走査することができる。


##戻り値
先頭の要素を指す読み取り専用イテレータ


##例外
投げない


##計算量
定数


##例
```cpp
#include <iostream>
#include <algorithm>
#include <iterator>
#include <unordered_set>

int main()
{
  std::unordered_multiset<int> um{ 1, 2, 3, 1, 2, 3, };

  copy(um.cbegin(), um.cend(), std::ostream_iterator<int>(std::cout, " "));
  std::cout << std::endl;
}</pre>
```
* iostream[link /reference/iostream.md]
* algorithm[link /reference/algorithm.md]
* iterator[link /reference/iterator.md]
* unordered_set[link /reference/unordered_set.md]
* unordered_multiset[link /reference/unordered_set/unordered_multiset/unordered_multiset.md]
* cend[link /reference/unordered_set/unordered_multiset/cend.md]
* ostream_iterator[link /reference/iterator/ostream_iterator.md]

###出力
```
3 3 2 2 1 1
```

注：[`unordered_multiset`](/reference/unordered_set/unordered_multiset.md) は非順序連想コンテナであるため、出力順序は無意味であることに注意


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

##参照

| | |
|----------------------------------------------|--------------------------------|
| [`begin`](./begin.md)                        | 先頭要素を指すイテレータの取得 |
| [`end`](./end.md)                            | 最終要素の次を指すイテレータの取得 |
| [`cend`](./cend.md)                          | 最終要素の次を指す読み取り専用イテレータの取得 |
| [`begin(size_type)`](./begin-size_type.md)   | インデックス（添え字）で指定したバケット内の先頭要素を指すイテレータを取得 |
| [`end(size_type)`](./end-size_type.md)       | インデックス（添え字）で指定したバケット内の最終要素の次を指すイテレータを取得 |
| [`cbegin(size_type)`](./cbegin-size_type.md) | インデックス（添え字）で指定したバケット内の先頭要素を指す読み取り専用イテレータを取得 |
| [`cend(size_type)`](./cend-size_type.md)     | インデックス（添え字）で指定したバケット内の最終要素の次を指す読み取り専用イテレータを取得 |

