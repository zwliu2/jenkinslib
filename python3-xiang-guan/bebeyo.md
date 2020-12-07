# python内置小知识

## 模块中\_\_all\_\_的使用

```text
__all__ 用于限制模块中对象的导入  如果abcd.py文件中加入了__all__=('test',)
但是你需要在one.py中调用abcd模块中的test2就会提示 name 'test2' is not defined
```

## Typing 类型注解

{% tabs %}
{% tab title="以前" %}
```python
friuts = [] # type:list[int]
```
{% endtab %}

{% tab title="现在" %}
```
from typing import  List
friuts:List[int] = []
```
{% endtab %}
{% endtabs %}

### typing alias类型别名

自定义变量别名   
更具体可查看[官网](https://docs.python.org/zh-cn/3/library/typing.html)

```python
Url = str
def retry(url: Url, retry_count: int) -> None: ...
```

### TypeVar

TypeVar，我们可以借助它来自定义兼容特定类型的变量，比如有的变量声明为 int、float、None 都是符合要求的，实际就是代表任意的数字或者空内容都可以，其他的类型则不可以，比如列表 list、字典 dict 等等，像这样的情况，我们可以使用 TypeVar 来表示。 例如一个人的身高，便可以使用 int 或 float 或 None 来表示，但不能用 dict 来表示，所以可以这么声明：

{% tabs %}
{% tab title="code" %}
```python
from typing import TypeVar
height = 1
Height = TypeVar('Height', int, float, None)
def get_height() -> Height:
    print(type(height))
    return height
```
{% endtab %}

{% tab title="result" %}
```
<class 'int'>
1
```
{% endtab %}
{% endtabs %}

### Union

#### 联合类型的联合类型等价于展开后的类型

Union，联合类型，`Union[X, Y]` 代表要么是 X 类型，要么是 Y 类型

{% tabs %}
{% tab title="code" %}
```python
from typing import Union, TypeVar, NewType, Optional

if Union[Union[int, str], float] == Union[int, str, float]:
    print('yes')
```
{% endtab %}

{% tab title="result" %}
```
yes
```
{% endtab %}
{% endtabs %}

#### 忽略内部顺序

{% tabs %}
{% tab title="code" %}
```python
from typing import Union
if Union[int,str,float] == Union[int,float,str]:
    print('yes')
```
{% endtab %}

{% tab title="result" %}
```
yes
```
{% endtab %}
{% endtabs %}

参数申明时比较常用

```python
from typing import Union, Callable
def process(fn: Union[str, Callable]):
    if isinstance(fn, str):
        pass
    elif isinstance(fn, Callable):
        fn()
```

#### 实战

可以参考  [https://cuiqingcai.com/7071.html](https://cuiqingcai.com/7071.html)  感谢作者

