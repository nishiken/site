#get_id
```cpp
namespace std {
namespace this_thread {
  thread::id get_id() noexcept;
}}
```
* thread::id[link /reference/thread/thread/id.md]


##概要
現スレッドのスレッド識別子を取得する。


##戻り値
現在のスレッド、すなわちこの関数を呼び出したスレッドのスレッド識別子。戻り値はデフォルトコンストラクトされた[`thread::id`](/reference/thread/thread/id.md)オブジェクトとは必ず異なる。


##例外
送出しない。


##例
```cpp
#include <iostream>
#include <thread>

int main()
{
  std::cout << "thread_id=" << std::this_thread::get_id() << std::endl;
  return 0;
}
```

###出力例
```
thread_id=538af0
```

##バージョン
###言語
- C++11

###処理系
- [Clang](/implementation#clang.md):
- [GCC](/implementation#gcc.md):
- [GCC, C++0x mode](/implementation#gcc.md): 4.6.3, 4.7.0
- [ICC](/implementation#icc.md):
- [Visual C++](/implementation#visual_cpp.md):


##参照
