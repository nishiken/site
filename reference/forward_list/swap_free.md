#swap(非メンバ関数)
```cpp
namespace std {
  template <class T, class Allocator>
  void swap(forward_list<T, Allocator>& x, forward_list<T, Allocator>& y);
}
```

##概要
2つの`forward_list`オブジェクトを入れ替える



##効果
`x.`[`swap`](./swap.md)`(y)`


##戻り値
なし


##例
```cpp
#include <iostream>
#include <forward_list>
#include <string>
#include <algorithm> // std::for_each

template <class T>
void print(const std::string& name, const std::forward_list<T>& ls)
{
  std::cout << name << " : {";
  std::for_each(ls.begin(), ls.end(), [](const T& x) { std::cout << x << " "; });
  std::cout << "}" << std::endl;
}

int main ()
{
  std::forward_list<int> ls1 = {4, 5, 6};
  std::forward_list<int> ls2 = {1, 2, 3};

  std::swap(ls1, ls2);

  print("ls1", ls1);
  print("ls2", ls2);
}
```
* swap[color ff0000]

###出力
```
ls1 : {1 2 3 }
ls2 : {4 5 6 }
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


