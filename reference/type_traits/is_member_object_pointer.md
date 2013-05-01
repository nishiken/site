#is_member_object_pointer
```cpp
namespace std {

  template <class T>

  struct is_member_object_pointer;

}
```

##概要

<b>型Tがデータメンバへのポインタ型かを調べる</b>


##効果

`is_member_object_pointer`は、型`T`がデータメンバへのポインタであるならば[`true_type`](/reference/type_traits/integral_constant-true_type-false_type.md)から派生し、そうでなければ[`false_type`](/reference/type_traits/integral_constant-true_type-false_type.md)から派生する。


##備考

メンバ関数へのポインタはデータメンバへのポインタではない。`static`なデータメンバへのポインタはデータメンバへのポインタではない。


##例

```cpp
#include <type_traits>
```

struct s

{

  int member_object;                     // decltype(&s::member_object) は int s::*

  void member_function(){}               // decltype(&s::member_function) は void (s::*)()

  static int static_member_object;       // decltype(&s::static_member_object) は int*

  static void static_member_function(){} // decltype(&s::static_member_function) は void (*)()

};


static_assert(std::is_member_object_pointer<int s::*>::value == true, "value == true, int s::* is member object pointer");

static_assert(std::is_same<std::is_member_object_pointer<int s::*>::value_type, bool>::value, "value_type == bool");

static_assert(std::is_same<std::is_member_object_pointer<int s::*>::type, std::true_type>::value, "type == true_type");

static_assert(std::is_member_object_pointer<int s::*>() == true, "is_member_object_pointer<int s::*>() == true");


static_assert(std::is_member_object_pointer<int>::value == false, "value == false, int is not member object pointer");

static_assert(std::is_same<std::is_member_object_pointer<int>::value_type, bool>::value, "value_type == bool");

static_assert(std::is_same<std::is_member_object_pointer<int>::type, std::false_type>::value, "type == false_type");

static_assert(std::is_member_object_pointer<int>() == false, "is_member_object_pointer<int>() == false");


static_assert(std::is_member_object_pointer<int s::* const>::value == true, "int s::* const is member object pointer");

static_assert(std::is_member_object_pointer<const int s::*>::value == true, "const int s::* is member object pointer");

static_assert(std::is_member_object_pointer<int* s::*>::value == true, "int* s::* is member object pointer");


static_assert(std::is_member_object_pointer<void (s::*)()>::value == false, "void (s::*)() is not member object pointer");
static_assert(std::is_member_object_pointer<int*>::value == false, "int* is not member object pointer");

static_assert(std::is_member_object_pointer<void (*)()>::value == false, "void (*)() is not member object pointer");


int main(){}




###出力

```cpp
```

##バージョン
```
###言語


- C++11


###処理系


- GCC, C++0x mode: 4.3.4, 4.5.3, 4.6.1

- Visual C++ 10.0<h4>備考</h4>
上の例でコンパイラによってはエラーになる。GCC 4.3.4, 4.5.3, Visual C++ 10.0 は [integral_constant](/reference/type_traits/integral_constant-true_type-false_type.md) が operator bool を持っていないためエラーになる。
