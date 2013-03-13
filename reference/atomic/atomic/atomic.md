```cpp
atomic() noexcept = default;
constexpr atomic(T desired) noexcept;

atomic(const atomic&) = delete;
```

##atomicオブジェクトの構築

- <b>atomic() noexceptデフォルトコンストラクタ。atomicオブジェクトを未初期化状態にする(C言語との互換性のため)</b>
- <b>constexpr atomic(T desired)desiredでオブジェクトを初期化する。この初期化はアトミック操作ではない。</b>


##例外

投げない


##例

```cpp
#include <iostream>
#include <atomic>

int main()
{
  // デフォルト構築(不定値)
  std::atomic<int> a;

  // 値を指定して初期化
  std::atomic<int> b(3);

  std::cout << b.load() << std::endl;
}
```

###出力

```cpp
3
```

##バージョン


###言語


- C++11



###処理系

- [Clang](https://sites.google.com/site/cpprefjp/implementation#clang): ??
- [GCC](https://sites.google.com/site/cpprefjp/implementation#gcc): 
- [GCC, C++0x mode](https://sites.google.com/site/cpprefjp/implementation#gcc): 4.7.0
- [ICC](https://sites.google.com/site/cpprefjp/implementation#icc): ??
- [Visual C++](https://sites.google.com/site/cpprefjp/implementation#visual_cpp) ??



##参照

