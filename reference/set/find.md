#find
```cpp
iterator find(const key_type& x);

const_iterator find(const key_type& x) const;
```

##概要

　コンテナ内で値が <i>x</i> である要素を検索し、見つかった場合はそれへのイテレータを返し、見つからなかった場合は [set::end](/reference/set/end.md) （コンテナの最後の要素の次）を指すイテレータを返す。


##引数

　・x

　　検索する値。
　　key_type はset コンテナの中で Key のエイリアスとして定義される。ここで Key は 1 番目のテンプレートパラメータであり、コンテナに格納される要素の型である。


##戻り値

　指定した値が見つかった場合はその要素へのイテレータ、そうでない場合は [set::end](/reference/set/end.md) へのイテレータ。iterator はメンバ型であり、set の中で bidirectional iterator 型として定義される。


##計算量

　[size](/reference/set/size.md) について対数時間。


##例

```cpp
#include <iostream>
#include <set>
using namespace std;

int main()
{
  set<int> c;

  c.insert(10);

  cout << (c.find(10) == c.end()) << endl;
  cout << (c.find(42) == c.end()) << endl;
  return 0;
}
```

###出力

```cpp
1
0
```

##参照

| | |
|-------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| [set::count](/reference/set/count.md) | 指定したキーにマッチする要素の数を返す |
| [set::lower_bound](/reference/set/lower_bound.md) | 与えられた値より小さくない要素へのイテレータを返す |
| [set::upper_bound](/reference/set/upper_bound.md) | 特定の値よりも大きい最初の要素へのイテレータを返す |

