#operator++
```cpp
reverse_iterator& operator++();
reverse_iterator operator++(int);
```

##概要

<b>イテレータをインクリメントする。</b>
<b>reverse_iteratorなので逆方向に進める。</b>


##効果

前置インクリメント operator++()：
--current;`return *this;`

後置インクリメント operator++(int)：
`reverse_iterator tmp = *this;``--current;`
`return tmp;`



##例

```cpp
#include <iostream>
#include <vector>
#include <iterator>

int main()
{
  std::vector<int> v = {1, 2, 3};

  std::reverse_iterator<decltype(v)::iterator> it(v.end());

  ++it;

  std::cout << *it << std::endl;
}
```
* ++it[color ff0000]

###出力

```cpp
2
```

##参照

