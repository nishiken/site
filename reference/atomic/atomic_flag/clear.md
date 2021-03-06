#clear
```cpp
void clear(memory_order order = memory_order_seq_cst) volatile noexcept;
void clear(memory_order order = memory_order_seq_cst) noexcept;
```
* memory_order[link /reference/atomic/memory_order.md]
* memory_order_seq_cst[link /reference/atomic/memory_order.md]

##概要
フラグをクリアする


##要件
`order`が以下のメモリオーダーではないこと：
- [`memory_order_acquire`](/reference/atomic/memory_order.md)
- [`memory_order_acq_rel`](/reference/atomic/memory_order.md)


##効果
`order`で指定されたメモリオーダーにしたがって、アトミックに`false`値を書き込む。


##戻り値
なし


##例外
投げない


##例
```cpp
#include <iostream>
#include <atomic>

int main()
{
  std::atomic_flag x = ATOMIC_FLAG_INIT;

  std::cout << std::boolalpha;
  {
    // 値をtrueに設定する(変更前の値はfalse)
    bool result = x.test_and_set();
    std::cout << result << std::endl;
  }

  // 値をfalseにする
  x.clear();

  {
    // 値をtrueに設定する(変更前の値はfalse)
    bool result = x.test_and_set();
    std::cout << result << std::endl;
  }
}
```
* clear[color ff0000]

###出力
```
false
false
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


