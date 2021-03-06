#emplace_hint
```cpp
template <class... Args>
iterator emplace_hint(const_iterator position, Args&&... args);
```

##概要
挿入位置のヒントを使用してコンテナ内へ要素を直接構築する


##要件
このコンテナの要素型 `value_type` は、コンテナに対して引数 `args` から直接構築可能（EmplaceConstructible）でなければならない。

ここで、コンテナに対して引数 `args` から直接構築可能とは、`m` をアロケータ型 `allocator_type` の lvalue、`p` を要素型 `value_type` へのポインタとすると、以下の式が適格（well-formed）であるということである。

`std::`[`allocator_traits`](/reference/memory/allocator_traits)`<allocator_type>::construct(m, p, args);`


引数 `position` は、コンテナの有効な読み取り専用イテレータでなければならないが、間接参照可能（dereferenceable）である必要はない。（つまり、最終要素の次を指すイテレータでも良い）


##効果
`std::`[`forward`](/reference/utility/forward.md)`<Args>(args)...` から構築された `value_type` のオブジェクトを `t` とすると、`t` をコンテナに挿入する。

なお、オブジェクト `t` は、構築後にコンテナにコピー、あるいはムーブされるわけではなく、コンテナ内に直接構築される。

引数 `position` は、要素の挿入位置を探し始める場所のヒントとして使用されるが、実装によって無視されるかもしれない。


##戻り値
追加された要素を指すイテレータ。


##例外
ハッシュ関数以外から例外が投げられた場合には、挿入はされない。


##計算量
平均的なケースでは定数（O(`1`)）だが、最悪のケースではコンテナの要素数に比例（O([`size`](./size.md)`()`)）。


##備考
- この関数が呼ばれた後も、当該コンテナ内の要素を指す参照は無効にはならない。なお、標準に明確な記載は無いが、当該コンテナ内の要素を指すポインタも無効にはならない。
- この関数が呼ばれた後も、呼び出しの前後でこのコンテナのバケット数（[`bucket_count`](./bucket_count.md)`()` の戻り値）が変わらなかった場合には当該コンテナを指すイテレータは無効にはならない。<br/>それ以外の場合は、当該コンテナを指すイテレータは無効になる可能性がある。<br/>コンテナのバケット数が変わらない場合とは、要素追加後の要素数が、要素追加前のバケット数（[`bucket_count`](./bucket_count.md)`()` の戻り値）×負荷率の最大値（[`max_load_factor`](./max_load_factor.md)`()` の戻り値）よりも小さかった場合である。<br/>なお、後者の条件は「よりも小さい」となっているが、最大負荷率の定義からすると「以下」の方が適切と思われる。[`reserve`](./reserve.md) も参照。

このメンバ関数は、コンテナの種類によってシグネチャが異なるため、注意が必要である。

`emplace` も含めた一覧を以下に示す。

| | |
|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| シーケンスコンテナ | `template <class... Args>`<br/> `iterator emplace(const_iterator, Args&&...)` |
| 連想コンテナ、非順序連想コンテナ<br/>（同一キーの重複を許さない場合） | `template <class... Args>`<br/> `pair<iterator, bool> emplace(Args&&...)` |
| 連想コンテナ、非順序連想コンテナ<br/>（同一キーの重複を許す場合） | `template <class... Args>`<br/> `iterator emplace(Args&&...)` |
| 連想コンテナ、非順序連想コンテナ | `template <class... Args>`<br/> `iterator emplace_hint(const_iterator, Args&&...)` |


##例
```cpp
#include <iostream>
#include <unordered_set>
#include <string>
#include <utility>    // for std::pair
#include <algorithm>  // for std::copy
#include <iterator>   // for std::ostream_iterator

// サンプル用クラス
struct is : std::pair<int, std::string> {
  is(int i, const char* s) : std::pair<int, std::string>(i, s) {}
};

// サンプル用クラスの比較演算子（first のみを比較）
bool operator==(const is& t, const is& u)
{
  return t.first == u.first;
}

bool operator!=(const is& t, const is& u)
{
  return t.first != u.first;
}

// サンプル用クラスのために std::hash を特殊化
namespace std {
  template <>
  struct hash<is> : private hash<int> {
    size_t operator()(const is& v) const { return hash<int>::operator()(v.first); }
  };
}

// サンプル用クラスのための挿入演算子
std::ostream& operator<<(std::ostream& os, const is& p)
{
  return os << '(' << p.first << ',' << p.second << ')';
}

int main()
{
  std::unordered_multiset<is> um{ {1, "1st"}, {1, "2nd"}, {2, "3rd"}, };

  // 初期状態の出力
  std::copy(um.cbegin(), um.cend(), std::ostream_iterator<is>(std::cout, ", "));
  std::cout << std::endl;

  // 追加するデータと等価な範囲を取得
  auto p = um.equal_range(is(1, "4th"));
  std::copy(p.first, p.second, std::ostream_iterator<is>(std::cout, ", "));
  std::cout << std::endl;

  // データの追加
  auto it = um.emplace_hint(std::next(p.first), 1, "4th");
  std::cout << *it << '\n';

  // 追加結果の出力
  std::copy(um.cbegin(), um.cend(), std::ostream_iterator<is>(std::cout, ", "));
  std::cout << std::endl;
}
```
* iostream[link /reference/iostream]
* unordered_set[link /reference/unordered_set.md]
* string[link /reference/string.md]
* utility[link /reference/utility.md]
* algorithm[link /reference/algorithm.md]
* iterator[link /reference/iterator.md]
* pair[link /reference/utility/pair.md]
* hash[link /reference/functional/hash.md]
* ostream[link /site/cpprefjp/reference/ostream]
* unordered_multiset[link /reference/unordered_set/unordered_multiset/unordered_multiset.md]
* copy[link /reference/algorithm/copy.md]
* cbegin[link /reference/unordered_set/unordered_multiset/cbegin.md]
* cend[link /reference/unordered_set/unordered_multiset/cend.md]
* ostream_iterator[link /reference/iterator/ostream_iterator.md]
* equal_range[link /reference/unordered_set/unordered_multiset/equal_range.md]
* next[link /reference/iterator/next.md]

###出力
libstdc++ の出力例（4.7.2 現在）
- 追加した要素 (1,4th) はヒントを無視して (1,2nd) と (1,1st) よりも前に追加されている。

```
(2,3rd), (1,2nd), (1,1st),
(1,2nd), (1,1st),
(1,4th)
(2,3rd), (1,4th), (1,2nd), (1,1st),
```

libc++ の出力例（2012/12/19 現在）


- 追加した要素 (1,4th) がヒントで指定した通り (1,1st) と (1,2nd) の間に追加されている。
```
(2,3rd), (1,1st), (1,2nd),
(1,1st), (1,2nd),
(1,4th)
(2,3rd), (1,1st), (1,4th), (1,2nd),
```

注：[`unordered_multiset`](/reference/unordered_set/unordered_multiset.md) は非順序連想コンテナであるため、出力順序は無意味であることに注意


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
|-------------------------------------------|------------------------------|
| [`emplace`](./emplace.md)                 | コンテナ内への要素の直接構築 |
| [`insert`](./insert.md)                   | 要素の追加                   |
| [`bucket_count`](./bucket_count.md)       | バケット数の取得 |
| [`load_factor`](./load_factor.md)         | 現在の負荷率（バケットあたりの要素数の平均）を取得 |
| [`max_load_factor`](./max_load_factor.md) | 負荷率の最大値を取得、設定 |
| [`rehash`](./rehash.md)                   | 最小バケット数指定によるバケット数の調整 |
| [`reserve`](./reserve.md)                 | 最小要素数指定によるバケット数の調整 |

