#end
```cpp
iterator end() noexcept;
const_iterator end() const noexcept;
```

##概要

<b>末尾の次を指すイテレータを取得する。</b>



##戻り値

非constな文脈ではiterator型で最後尾要素の次を指すイテレータを返し、
constな文脈ではconst_iterator型で 最後尾要素の次を指すイテレータを返す。



##例外

投げない


##計算量

定数時間


##備考



##例

```cpp
#include <iostream>
#include <array>

int main()
{
  std::array<int, 3> ar = {1, 2, 3};
  const std::array<int, 3>& car = ar;

  decltype(ar)::iterator i = ar.begin();
  decltype(ar)::iterator last = ar.end();

  decltype(ar)::const_iterator ci = car.begin();
  decltype(ar)::const_iterator clast = car.end();

  for (; i != last; ++i) {
    std::cout << *i << std::endl;
  }

  for (; ci != clast; ++ci) {
    std::cout << *ci << std::endl;
  }
}
```
* end[color ff0000]
* end[color ff0000]

###出力

```cpp
1
2
3
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
- [Visual C++](/implementation#visual_cpp.md) ??<h4>備考</h4>
(処理系やライブラリのバグや不完全な実装などをここに書く。なければ備考欄を削除)



##実装例

```cpp
```

##参照
```