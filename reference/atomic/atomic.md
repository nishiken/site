#atomic
```cpp
namespace std {
  template<class T> struct atomic;

  template<> struct atomic<integral>;
  template<class T> struct atomic<T*>;
}
```
* integral[italic]

##概要
`atomic`クラスは、型`T`をアトミック操作するためのクラスである。整数型およびポインタに対する特殊化が提供されており、それぞれに特化した演算が用意されている。その他の型に`atomic`クラスを使用する場合、型`T`はtrivially copyable (TODO)である必要がある。特殊化された整数型および`bool`型にはそれぞれ`atomic_T`という名前の`typedef`が提供される。

| | |
|--------------------------------|--------------------------------------------|
| 名前付きアトミック型 | テンプレート引数となる整数型 |
|` atomic_char` |` char` |
|` atomic_schar` |` signed char` |
|` atomic_uchar` |` unsigned char` |
|` atomic_short` |` short` |
|` atomic_ushort` |` unsigned short` |
|` atomic_int` |` int` |
|` atomic_long` |` long` |
|` atomic_ulong` |` unsigned long` |
|` atomic_llong` |` long long` |
|` atomic_ullong` |` unsigned long long` |
|` atomic_char16_t` |` char16_t` |
|` atomic_char32_t` |` char32_t` |
|` atomic_wchar_t` |` wchar_t` |
|` atomic_bool` |` bool` |
また、`<cstdint>`で定義される整数型に対する以下の`typedef`も提供される。

| | |
|------------------------------------|--------------------------------------------|
| 名前付きアトミック型 | テンプレート引数となる整数型 |
|` atomic_int_least8_t` |` int_least8_t` |
|` atomic_uint_least8_t` |` uint_least8_t` |
|` atomic_int_least16_t` |` int_least16_t` |
|` atomic_uint_least16_t` |` uint_least16_t` |
|` atomic_int_least32_t` |` int_least32_t` |
|` atomic_uint_least32_t` |` uint_least32_t` |
|` atomic_int_least64_t` |` int_least64_t` |
|` atomic_uint_least64_t` |` uint_least64_t` |
|` atomic_int_fast8_t` |` int_fast8_t` |
|` atomic_uint_fast8_t` |` uint_fast8_t` |
|` atomic_int_fast16_t` |` int_fast16_t` |
|` atomic_uint_fast16_t` |` uint_fast16_t` |
|` atomic_int_fast32_t` |` int_fast32_t` |
|` atomic_uint_fast32_t` |` uint_fast32_t` |
|` atomic_int_fast64_t` |` int_fast64_t` |
|` atomic_uint_fast64_t` |` uint_fast64_t` |
|` atomic_intptr_t` |` intptr_t` |
|` atomic_uintptr_t` |` uintptr_t` |
|` atomic_size_t` |` size_t` |
|` atomic_ptrdiff_t` |` ptrdiff_t` |
|` atomic_intmax_t` |` intmax_t` |
|` atomic_uintmax_t` |` uintmax_t` |
`void*`に対する特殊化の`typedef`として、`atomic_address`型が提供される。


###共通メンバ関数
| | |
|-------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| [`(constructor)`](./atomic/atomic.md) | コンストラクタ |
| `~atomic() = default` | デストラクタ |
| [`operator=`](./atomic/op_assign.md) | 代入演算子 |
| [`is_lock_free`](./atomic/is_lock_free.md) | オブジェクトがロックフリーに振る舞えるかを判定する |
| [`store`](./atomic/store.md) | 値を書き込む |
| [`load`](./atomic/load.md) | 値を読み込む |
| [`operator T`](./atomic/op_t.md) | 型Tへの変換演算子 |
| [`exchange`](./atomic/exchange.md) | 値を入れ替える |
| [`compare_exchange_weak`](./atomic/compare_exchange_weak.md) | 弱い比較で値を入れ替える |
| [`compare_exchange_strong`](./atomic/compare_exchange_strong.md) | 強い比較で値を入れ替える |


###atomic<integral>専用メンバ関数
| | |
|----------------------------------------------------------------------------------------------------------------------|-----------------------|
| [`fetch_add`](./atomic/fetch_add.md) | 加算 |
| [`fetch_sub`](./atomic/fetch_sub.md) | 減算 |
| [`fetch_and`](./atomic/fetch_and.md) | AND演算 |
| [`fetch_or`](./atomic/fetch_or.md) | OR演算 |
| [`fetch_xor`](./atomic/fetch_xor.md) | XOR演算 |
| [`operator++`](./atomic/op_increment.md) | インクリメント |
| [`operator--`](./atomic/op_decrement.md) | デクリメント |
| [`operator+=`](./atomic/op_plus_assign.md) | 加算 |
| [`operator-=`](./atomic/op_minus_assign.md) | 減算 |
| [`operator&=`](./atomic/op_and_assign.md) | AND演算 |
| <code>[operator&#x7C;=](./atomic/op_or_assign.md)</code> | OR演算 |
| [`operator^=`](./atomic/op_xor_assign.md) | XOR演算 |


###atomic<T*>専用メンバ関数
| | |
|----------------------------------------------------------------------------------------------------------------------|-----------------------|
| [`fetch_add`](./atomic/fetch_add.md) | 加算 |
| [`fetch_sub`](./atomic/fetch_sub.md) | 減算 |
| [`operator++`](./atomic/op_increment.md) | インクリメント |
| [`operator--`](./atomic/op_decrement.md) | デクリメント |
| [`operator+=`](./atomic/op_plus_assign.md) | 加算 |
| [`operator-=`](./atomic/op_minus_assign.md) | 減算 |


###例
```cpp
// スピンロックの実装
// Boost Atomic Library - Usage Example
// http://www.boost.org/doc/libs/1_53_0/doc/html/atomic/usage_examples.html#boost_atomic.usage_examples.example_spinlock

#include <iostream>
#include <atomic>
#include <thread>
#include <mutex>
 
class spinlock {
private:
  typedef enum {Locked, Unlocked} LockState;
  std::atomic<LockState> state_;

public:
  spinlock() : state_(Unlocked) {}
  
  void lock()
  {
    // 現在の状態をLockedと入れ替える
    while (state_.exchange(Locked, std::memory_order_acquire) == Locked) {
      // busy-wait...アンロックされるまで待機
    }
  }

  void unlock()
  {
    // 値をUnlockedに更新
    state_.store(Unlocked, std::memory_order_release);
  }
};

namespace {
  spinlock lock;
}

template <class T>
void print(const T& x)
{
  std::lock_guard<spinlock> lk(lock);
  std::cout << x << std::endl;
}

void f()
{
  print(1);
}

void g()
{
  print(2);
}

int main()
{
  std::thread t1(f);
  std::thread t2(g);

  t1.join();
  t2.join();
}
```
* http://www.boost.org/doc/libs/1_53_0/doc/html/atomic/usage_examples.html#boost_atomic.usage_examples.example_spinlock[link http://www.boost.org/doc/libs/1_53_0/doc/html/atomic/usage_examples.html#boost_atomic.usage_examples.example_spinlock]
* exchange[color ff0000]
* store[color ff0000]


###出力例
```
21
```


##バージョン
###言語
- C++11

###処理系
- [Clang](/implementation#clang.md): ??
- [GCC](/implementation#gcc.md): 
- [GCC, C++0x mode](/implementation#gcc.md): 4.7.0(atomic_addressは未実装)
- [ICC](/implementation#icc.md): ??
- [Visual C++](/implementation#visual_cpp.md) ??


###参照
[N2145 C++ Atomic Types and Operations](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2007/n2145.html)
[アトミックオブジェクトを含むクラスのコピーとムーブ - Faith and Brave - C++で遊ぼう](http://d.hatena.ne.jp/faith_and_brave/20130110/1357808183)

