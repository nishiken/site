#operator>
```cpp
namespace std {

  template <class Iterator1, class Iterator2>
  bool operator>(const move_iterator<Iterator1>& x,
                 const move_iterator<Iterator2>& y);

}
```

##概要

<b>2つのmove_iteratorオブジェクトにおいて、左辺が右辺より大きいかを判定する。</b>



##戻り値

`return y < x;`

##例

```cpp
#include <iostream>
#include <vector>
#include <memory>
#include <algorithm>
#include <iterator>

int main()
{
  std::vector<std::unique_ptr<int>> v;
  for (int i = 0; i < 5; ++i)
    v.emplace_back(new int(i));

  auto it1 = std::make_move_iterator(v.begin());
  auto it2 = std::make_move_iterator(v.begin() + 1);

  if (it2 > it1) {
    std::cout << "greater" << std::endl;
  }
  else {
    std::cout << "not greater" << std::endl;
  }
}
```
* it2 > it1[color ff0000]

###出力

```cpp
greater
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

