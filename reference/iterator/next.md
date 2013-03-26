#next
```cpp
namespace std {
  template <class ForwardIterator>
  ForwardIterator next(ForwardIterator x,
                       typename std::iterator_traits<ForwardIterator>::difference_type n = 1);
}
```

##概要

<b>n回進めたイテレータを返す。</b>
<b>[advance](/reference/iterator/advance)()と違い、引数として渡されたイテレータへの参照を書き換えるのではなく、n回進んだイテレータのコピーを返す。</b>


##効果

`[advance](/reference/iterator/advance)(x, n);``return x;`

##戻り値

引数として渡されたイテレータをn回進めたイテレータのコピー


##例

```cpp
#include <iostream>
#include <iterator>
#include <vector>

int main()
{
  std::vector<int> v = {3, 1, 4, 5, 2};

  {
    decltype(v)::iterator it = std::next(v.begin()); // イテレータを1回進める
    std::cout << *it << std::endl;
  }
  {
    decltype(v)::iterator it = std::next(v.begin(), 2); // イテレータを2回進める
    std::cout << *it << std::endl;
  }
}
```
* next[color ff0000]
* next[color ff0000]

###出力

```cpp
1
4
```

##バージョン


###言語


- C++11



###処理系

- [Clang](/implementation#clang): ??
- [GCC](/implementation#gcc): 
- [GCC, C++0x mode](/implementation#gcc): 4.7.0
- [ICC](/implementation#icc): ??
- [Visual C++](/implementation#visual_cpp) ??



##参照

[boost::next() - Boost Utility Library](http://www.boost.org/doc/libs/release/libs/utility/utility.htm#functions_next_prior)

