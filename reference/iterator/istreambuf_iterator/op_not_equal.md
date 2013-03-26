#operator!=
```cpp
namespace std {

  template <class CharT, class Traits>
  bool operator!=(const istreambuf_iterator<CharT, Traits>& a,
                  const istreambuf_iterator<CharT, Traits>& b);

}
```

##概要

<b>2つのistreambuf_iteratorオブジェクトを非等値比較する。</b>


##戻り値

`!a.equal(b)`

##例

```cpp
#include <iostream>
#include <iterator>
#include <sstream>

int main()
{
  std::stringstream ss;
  ss << "123";

  std::istreambuf_iterator<char> it1(ss);
  std::istreambuf_iterator<char> last;

  if (it1 != last) {
    std::cout << "not equal" << std::endl;
  }
  else {
    std::cout << "equal" << std::endl;
  }
}
```
* it1 != last[color ff0000]

###出力

```cpp
not equal
```

##参照

