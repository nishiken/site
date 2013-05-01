#search_n
```cpp
<pre style='margin:0'><code style='color:black'>namespace std {
  template<class ForwardIterator, class Size, class T>
  ForwardIterator search_n(ForwardIterator first, ForwardIterator last,
                           Size count, const T& value);

  template<class ForwardIterator, class Size, class T, class BinaryPredicate>
  ForwardIterator search_n(ForwardIterator first, ForwardIterator last,
                           Size count, const T& value, BinaryPredicate pred);
}
</pre>
```

###概要

あるシーケンスの中から、特定のサブシーケンスを探す。

###要件

Size は整数型に変換できる型である必要がある。

###戻り値

[first,last-count) 内のイテレータ i があるとき、0 以上 count 未満の整数 n について、それぞれ *(i + n) == value もしくは pred(*(i + n),value) != false であるようなサブシーケンスを探し、見つかった最初のサブシーケンスの先頭のイテレータを返す。
そのようなイテレータが見つからない場合は last を返す。

###計算量

最大で last - first 回の対応する比較もしくは述語が適用される。

###実装例

```cpp
<pre style='margin:0'><code style='color:black'>template <class ForwardIterator, class Size, class T>
ForwardIterator search_n(ForwardIterator first, ForwardIterator last, Size count, T const& value)
{
  if (first == last || count <= 0)
    return first;

  while (first != last) {
    if (*first == value) {
      ForwardIterator it = first;
      ++it;
      Size i = 1;
      for (; i < count && it != last && *it == value; ++i, ++it)
        ;
      if (i == count)
        return first;
      else if (it == last)
        return last;
      else
        first = it;
    }
    ++first;
  }
  return last;
}
template <class ForwardIterator, class Size, class T, class BinaryPredicate>
ForwardIterator search_n(ForwardIterator first, ForwardIterator last,
                         Size count, T const& value, BinaryPredicate pred)
{
  if (first == last || count <= 0)
    return first;

  while (first != last) {
    if (pred(*first, value)) {
      ForwardIterator it = first;
      ++it;
      Size i = 1;
      for (; i < count && it != last && pred(*it, value); ++i, ++it)
        ;
      if (i == count)
        return first;
      else if (it == last)
        return last;
      else
        first = it;
    }
    ++first;
  }
  return last;
}</pre>
```

###使用例

```cpp
<pre style='margin:0'>#include <algorithm>
#include <iostream>
#include <vector><code style='color:black'>
</pre>
```

<pre style='margin:0'><code style='color:black'>int main() {
  std::vector<int> v = { 1,2,3,2,1,3,3,2,3,3,1 };

  // 3 が 2 つ連続している最初のシーケンスを探す
  auto it1 = std::</code>`<color=ff0000>search_n</color>`<code style='color:black'>(v.cbegin(), v.cend(), 2, 3);
  // v[5] の位置を指すイテレータが見つかる。
  if (it1 == v.cend()) {
    std::cout << "not found" << std::endl;
  } else {
    std::cout << "found: index==" << std::distance(v.cbegin(), it1) << std::endl;
  }

  // 3 未満が 2 つ連続している最初のシーケンスを探す
  auto it2 = std::</code>`<color=ff0000>search_n</color>`<code style='color:black'>(v.cbegin(), v.cend(), 2, 3, [](int x, int y) { return x < y; });
  // v[0] の位置を指すイテレータが見つかる。
  if (it2 == v.cend()) {
    std::cout << "not found" << std::endl;
  } else {
    std::cout << "found: index==" << std::distance(v.cbegin(), it2) << std::endl;
  }
}</code></pre>


###出力

<pre>```cpp
found: index==5
found: index==0
</pre>