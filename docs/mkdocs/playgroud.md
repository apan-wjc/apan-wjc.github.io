### Admonition Style

??? note "默认支持的样式"

    !!! note
        `note`是默认样式，其他样式加载失败就回退到这个样式。
    !!! abstract
    !!! info
    !!! tip
    !!! success
    !!! failure
    !!! question
    !!! warning
    !!! danger
    !!! bug
    !!! example
    !!! quote

### Admonition
Admonition 或者叫 call-out ，是一种突出内容的手段。
原生的样式比较简单：
> 突出内容  
> 引用内容

mkdocs-material 支持更好看的样式：
#### Folded
=== "渲染效果"
    ??? info "标题"

        这里可以写一些内容
=== "源代码"
    ```
    ??? info "标题"

        这里可以写一些内容
    ```
#### Unfolded
=== "渲染效果"
    !!! info "标题"

        这里可以写一些内容
=== "源代码"
    ```
    !!! info "标题"

        这里可以写一些内容
    ```
### CLI Animation
=== "渲染效果"
    <!-- termynal -->
    ```
    $ python3 -m pip install numpy
    # 正在安装numpy，稍作等待
    
    ---> 100%
    
    $ python3 -m pip list
    
    Package    Version
    ---------- -------
    numpy      1.25.2
    pip        23.2.1
    setuptools 58.0.4
    six        1.15.0
    wheel      0.37.0
    ```
=== "源代码"
    ````
    <!-- termynal -->
    $ python3 -m pip install numpy
    # 正在安装numpy，稍作等待

    ---> 100%

    $ python3 -m pip list

    Package    Version
    ---------- -------
    numpy      1.25.2
    pip        23.2.1
    setuptools 58.0.4
    six        1.15.0
    wheel      0.37.0
    ````

### Extra Options
mkdocs-material中，代码块还可以自定义标题、显示行号、高亮显示某些行：
=== "渲染效果"

    ``` python linenums="1" title="fibonacci" hl_lines="3 5 6"
    def fib(n: int):
        assert isinstance(n, int)
        if n<2:
            return 1
        else:
            return fib(n-1)+fib(n-2)
    ```

=== "源代码"

    ````markdown
    ``` python linenums="1" title="fibonacci" hl_lines="3 5 6"
    def fib(n: int):
        assert isinstance(n, int)
        if n<2:
            return 1
        else:
            return fib(n-1)+fib(n-2)
    ```
    ````
### Side by Side
=== "Python"
    ```python
    print("Hello, World!")
    ```
=== "C"
    ```C
    #include <stdio.h>
    int main() {
      printf("Hello, World!");
      return 0;
    }
    ```
The actual code for the above:  
````markdown
=== "Python"
    ```python
    print("Hello, World!")
    ```
=== "C"
    ```C
    #include <stdio.h>
    int main() {
      printf("Hello, World!");
      return 0;
    }
    ```
````
### Side by Side (not code)
=== "Unordered List"

    ``` markdown
    * Sed sagittis eleifend rutrum
    * Donec vitae suscipit est
    * Nulla tempor lobortis orci
    ```
=== "Ordered List"

    ``` markdown
    1. Sed sagittis eleifend rutrum
    2. Donec vitae suscipit est
    3. Nulla tempor lobortis orci
    ```
