#cbegin(size_type)
```cpp
const_local_iterator cbegin(size_type n) const;
```

##概要
インデックス（添え字）で指定したバケット内の先頭の要素を指す読み取り専用イテレータを取得する。

`unordered_set` は非順序連想コンテナであるため「先頭」に特に意味はないが、`cbegin(size_type)` で得られたイテレータを [`cend(size_type)`](./cend-size_type.md) まで `operator++()` でイテレートすることで当該バケットの要素を漏れなくダブりなく走査することができる。


##要件
パラメータ `n` は `[0, `[`bucket_count`](./bucket_count.md)`())` の範囲でなければならない。


##戻り値
インデックス（添え字） `n` で指定したバケット内の先頭の要素を指すイテレータ


##計算量
定数


##例
```cpp
#include <iostream>
#include <string>
#include <unordered_set>
#include <algorithm>
#include <iterator>

int main()
{
  std::unordered_set<std::string> us{ "A", "B", "C", "D", "E", };

  decltype(us)::size_type c = us.bucket_count();
  std::cout << "bucket_count() = " << c << std::endl;

  for (decltype(us)::size_type b = 0; b < c; ++b) {
    decltype(us)::size_type s = us.bucket_size(b);
    std::cout << "bucket = " << b << ", bucket_size = " << s << ", keys = { ";
    std::copy(us.cbegin(b), us.cend(b), std::ostream_iterator<std::string>(std::cout, ", "));
    std::cout << "}" << std::endl;
  }
}
```
* iostream[link /reference/iostream.md]
* string[link /reference/string.md]
* unordered_set[link /reference/unordered_set.md]
* algorithm[link /reference/algorithm.md]
* iterator[link /reference/iterator.md]
* bucket_count[link ./bucket_count.md]
* bucket_size[link ./bucket_size.md]
* copy[link /reference/algorithm/copy.md]
* cend[link ./cend-size_type.md]
* ostream_iterator[link /reference/iterator/ostream_iterator.md]

###出力
```
bucket_count() = 5
bucket = 0, bucket_size = 1, keys = { E, }
bucket = 1, bucket_size = 1, keys = { D, }
bucket = 2, bucket_size = 0, keys = { }
bucket = 3, bucket_size = 1, keys = { A, }
bucket = 4, bucket_size = 2, keys = { C, B, }
```

##バージョン
###言語
- C++11

###処理系
- [Clang](/implementation#clang.md): -
- [Clang, C++0x mode](/implementation#clang.md): 3.1
- [GCC](/implementation#gcc.md): -
- [GCC, C++0x mode](/implementation#gcc.md): 4.7.0
- [ICC](/implementation#icc.md): ?
- [Visual C++](/implementation#visual_cpp.md): ?

##参照

| | |
|--------------------------------------------|--------------------------------|
| [`begin`](./begin.md)                      | 先頭要素を指すイテレータの取得 |
| [`end`](./end.md)                          | 最終要素の次を指すイテレータの取得 |
| [`cbegin`](./cbegin.md)                    | 先頭要素を指す読み取り専用イテレータの取得 |
| [`cend`](./cend.md)                        | 最終要素の次を指す読み取り専用イテレータの取得 |
| [`begin(size_type)`](./begin-size_type.md) | インデックス（添え字）で指定したバケット内の先頭要素を指すイテレータを取得 |
| [`end(size_type)`](./end-size_type.md)     | インデックス（添え字）で指定したバケット内の最終要素の次を指すイテレータを取得 |
| [`cend(size_type)`](./cend-size_type.md)   | インデックス（添え字）で指定したバケット内の最終要素の次を指す読み取り専用イテレータを取得 |

