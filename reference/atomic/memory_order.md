#memory_order
```cpp
namespace std {
  typedef enum memory_order {
    memory_order_relaxed, memory_order_consume, memory_order_acquire,
    memory_order_release, memory_order_acq_rel, memory_order_seq_cst
  } memory_order;
}
```

##概要
コンパイラに許可されている最適化の一つに、「プログラムの意味を変えない限りにおいて、メモリアクセスの順番を変えたり、省略したりしてもよい」というものがある。また、マルチコアCPUにおいては、あるCPUコアによるメモリアクセスの順序が他のコアからも同じように見えるとは限らない。このような挙動はマルチスレッドプログラミングにおいて問題になることがある。
この問題への対処として、C++11では各スレッドの実行に順序付けをするための"happens before"(先行発生)という関係を定義し、それによってあるスレッドでの操作が他スレッドから可視になるか否かを定めている。
atomic変数においては、"release"操作によって書き込まれた値を"acquire"操作によって別のスレッドが読み出した場合に、そのrelease操作とacquire操作の間に順序付けが行われる。以下に例を挙げる。

```cpp
#include <iostream>
#include <atomic>
#include <thread>
int data;
std::atomic<bool> ready(false);

void f()
{
  while (!ready.load(std::memory_order_acquire)) {
  }

  std::cout << data << std::endl;   // (2)
}

int main()
{
  std::thread t(f);

  data = 3;   // (1)
  ready.store(true, std::memory_order_release);

  t.join();
}
```
* memory_order_acquire[color ff0000]
* memory_order_release[color ff0000]

[`atomic<bool>`](./atomic.md)型の変数`ready`への読み書きに注目すると、`main()`では変数`ready`に `true` を"release"操作として書き込み、`f()`では"acquire"操作としての読み込みを `true` が返されるまで繰り返している。よって、`f()`の`while`ループを抜けた時点で、`main()`の`ready.store()`と`f()`の`ready.load()`の間に順序付け(happens before関係)が成立している。
ここでさらに変数`data`への読み書き(1), (2)に注目すると、(1)は`ready.store()`より前、(2)は`ready.load()`より後にあるので、以下のようなスレッド間の順序付け(happens before関係)が成立することになる。
   (1) → `ready.store()` → `ready.load()` → (2)
よって、(1)における書き込みが(2)の時点で可視であることが保証される。
このようにしてC++のマルチスレッドプログラムにおける実行順序および可視性を理解することができる。

以下の列挙値はatomic変数への操作に指定可能な順序付けの種類を表す。

| 列挙値 | 説明 |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `memory_order_relaxed` | スレッド間の順序付けの効果は一切持たない。 |
| `memory_order_consume` | acquire操作と似ているが、それより弱い順序付けでの読み込みを行うことを指示する。acquire操作は後続の全ての操作に対して順序付けを行うのに対し、consume操作は読み込まれた値に依存(ただし条件分岐による依存は除く)する操作のみに順序付けを保証する点が異なる。[store()](./atomic/store.md)など、書き込みのみを行う操作に対しては指定できない。 |
| `memory_order_acquire` | aquire操作としての読み込みを行うことを指示する。[store()](./atomic/store.md)など、書き込みのみを行う操作に対しては指定できない。 |
| `memory_order_release` | release操作としての書き込みを行うことを指示する。[load()](./atomic/load.md)など、読み込みのみを行う操作に対しては指定できない。 |
| `memory_order_acq_rel` | 読み込みと書き込みを同時に行う操作(Read-Modify-Write操作)に対してのみ指定することができ、acquireとreleaseを合わせた効果を持つ。 |
| `memory_order_seq_cst` | aquire(読み込み操作の場合)、release(書き込み操作の場合)、acq_rel(Read-Modify-Write操作の場合)としての効果を持つ。さらに、同じseq_cstが指定されている他のatomic操作との間での順序一貫性も保証する。これは最も強い保証であり、標準のatomic操作におけるデフォルトのメモリオーダーとして使用される。「seq_cst」は「sequential consistency(順序一貫性)」を意味する。 |


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
- [そろそろvolatileについて一言いっておくか - yamasaのネタ帳](http://d.hatena.ne.jp/bsdhouse/20090720/1248085754)
- [次期C++に導入されるメモリバリアについて解説してみる - yamasaのネタ帳](http://d.hatena.ne.jp/bsdhouse/20090816/1250446250)
- [C++0xのメモリバリアをより深く解説してみる - yamasaのネタ帳](http://d.hatena.ne.jp/bsdhouse/20090929/1254237835)
- [C/C++11 mappings to processors](http://www.cl.cam.ac.uk/~pes20/cpp/cpp0xmappings.html)
- [N1525: Memory-Order Rationale](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n1525.htm)

