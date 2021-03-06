#partition_point
```cpp
namespace std {
  template <class ForwardIterator, class Predicate>
  ForwardIterator partition_point(ForwardIterator first, ForwardIterator last, Predicate pred);
}
```

##概要
与えられた範囲を条件によって 2 つのグループに分け、それらの間の位置を得る。


##要件
`ForwardIterator` の value type は `Predicate` の argument type へ変換可能でなければならない。
`[first,last)` は `pred` によって partition されていなければならない。つまり、`pred` を満たす全ての要素が、`pred` を満たさない全ての要素より前に出現してなければならない。


##戻り値
[`all_of`](/reference/algorithm/all_of.md)`(first, mid, pred)` と [`none_of`](/reference/algorithm/none_of.md)`(mid, last, pred)` が `true` であるようなイテレータ `mid` を返す。


##計算量
O(log(`last - first`)) のオーダーで `pred` が適用される。


##例
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <string>

void print(const std::string& name, const std::vector<int>& v)
{
  std::cout << name << " : ";
  std::for_each(v.begin(), v.end(), [](int x) {
    std::cout << x << ",";
  });
  std::cout << std::endl;
}

bool is_even(int x) { return x % 2 == 0; }

int main()
{
  std::vector<int> v = {1, 2, 3, 4, 5};

  std::partition(v.begin(), v.end(), is_even);

  // 偶数グループと奇数グループに分かれた位置を得る
  decltype(v)::iterator it = std::partition_point(v.begin(), v.end(), is_even);

  print("v", v);
  std::cout << *it << std::endl;
}
```
* partition_point[color ff0000]


###出力
```
v : 4,2,3,1,5,
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


##実装例
```cpp
```

##参照

