#recursive_timed_mutex
```cpp
namespace std {
  class recursive_timed_mutex;
}
```

##概要
`recursive_timed_mutex`は、スレッド間で使用する共有リソースを排他制御するためのクラスであり、再帰的なロックと、ロック取得のタイムアウト機能をサポートする。[`lock()`](./recursive_timed_mutex/lock.md)メンバ関数によってリソースのロックを取得し、[`unlock()`](./recursive_timed_mutex/unlock.md)メンバ関数でリソースのロックを手放す。このクラスのデストラクタは自動的に[`unlock()`](./recursive_timed_mutex/unlock.md)メンバ関数を呼び出すことはないため、通常このクラスのメンバ関数は直接は呼び出さず、[`lock_guard`](/reference/mutex/lock_guard.md)のようなクラスと併用する。


###メンバ関数

| | |
|---------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
| [`(constructor)`](./recursive_timed_mutex/revursive_timed_mutex.md) | コンストラクタ |
| [`(destructor)`](./recursive_timed_mutex/-recursive_timed_mutex.md) | デストラクタ |
| `operator=(const recursive_timed_mutex&) = delete` | 代入演算子 |
| [`lock`](./recursive_timed_mutex/lock.md) | ロックを取得する |
| [`try_lock`](./recursive_timed_mutex/try_lock.md) | ロックの取得を試みる |
| [`try_lock_for`](./recursive_timed_mutex/try_lock_for.md) | タイムアウトする相対時間を指定してロックの取得を試みる |
| [`try_lock_until`](./recursive_timed_mutex/try_lock_until.md) | タイムアウトする絶対時間を指定してロックの取得を試みる |
| [`unlock`](./recursive_timed_mutex/unlock.md) | ロックを手放す |
| [`native_handle`](./recursive_timed_mutex/native_handle.md) | ミューテックスのハンドルを取得する |


###メンバ型

| | |
|---------------------------------|--------------------------------|
| `native_handle_type` | 実装依存のハンドル型 |


###例
```cpp
#include <iostream>
#include <mutex>
#include <thread>
#include <chrono>
#include <system_error>

class counter {
  int count_ = 0;
  std::recursive_timed_mutex mtx_;
public:
  int add(int value)
  {
    // ロックを取得する(3秒でタイムアウト)
    if (!mtx_.try_lock_for(std::chrono::seconds(3))) {
      // ロック取得がタイムアウト
      std::error_code ec(static_cast<int>(std::errc::device_or_resource_busy), std::generic_category());
      throw std::system_error(ec);
    }

    int result = count_ += value;

    mtx_.unlock();

    return result;
  }

  int increment()
  {
    // ロックを取得する(3秒でタイムアウト)
    if (!mtx_.try_lock_for(std::chrono::seconds(3))) {
      // ロック取得がタイムアウト
      std::error_code ec(static_cast<int>(std::errc::device_or_resource_busy), std::generic_category());
      throw std::system_error(ec);
    }

    int result = add(1); // add()関数内でも同じミューテックスからロックを取得する

    mtx_.unlock();

    return result;
  }
};

std::mutex print_mtx_;
void print_value(int value)
{
  std::lock_guard<std::mutex> lock(print_mtx_);
  std::cout << "count == " << value << std::endl;
}

counter c;
void change_count()
{
  int value = c.increment();
  print_value(value);
}

int main()
{
  std::thread t1(change_count);
  std::thread t2(change_count);

  t1.join();
  t2.join();
}
```

###出力例
```
count == 1
count == 2
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

###参照

