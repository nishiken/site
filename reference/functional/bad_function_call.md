#bad_function_call
```cpp
namespace std {
  class bad_function_call : public exception;
}
```
* exception[link /reference/exception/exception.md]

##概要
`std::bad_function`は、空の[`std::function`](./function.md)オブジェクトに対して`operator()`を呼び出した際に送出される例外クラスである。

注意: 空の[`std::function`](./function.md)オブジェクトに対して[`std::bind()`](./bind.md)を呼び出した結果を[`std::function`](./function.md)オブジェクトに格納しても空にはならないが、実際に`operator()`を呼ぶと`std::bad_function_call`例外が送出される。

###例
```cpp
#include <iostream>
#include <functional>

int main()
{
  std::function<void()> f;

  try {
    f();
  }
  catch (std::bad_function_call& e) {
    std::cout << "bad function call" << std::endl;
  }
}
```

###出力
```
bad function call
```

##バージョン
###言語
- C++11

###処理系
- [Clang](/implementation#clang.md): ??
- [GCC](/implementation#gcc.md): 
- [GCC, C++0x mode](/implementation#gcc.md): 4.4, 4.7.2(what()が"std::bad_weak_ptr"を返すので規格違反。バグ報告済み。[#55847](http://gcc.gnu.org/bugzilla/show_bug.cgi?id=55847))
- [ICC](/implementation#icc.md): ??
- [Visual C++](/implementation#visual_cpp.md) 10.0


###参照

