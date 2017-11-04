* 代码越少，开发效率越高。

* Python 使用缩进来组织代码块，请务必遵守约定俗成的习惯，坚持使用 4 个空格的缩进。

* 在文本编辑器中，需要设置把 Tab 自动转换为 4 个空格，确保不混用 Tab 和空格。

* Python 还允许用 r''表示''内部的字符串默认不转义。

* 空值是 Python 里一个特殊的值，用 None 表示。None不能理解为 0，因 为 0 是有意义的，而 None 是一个特殊的空值。

* Python 的整数没有大小限制，Python 的浮点数也没有大小限制。

* 对于单个字符的编码，Python 提供了 ord()函数获取字符的整数表示， chr()函数把编码转换为对应的字符


    >>> ord('A')
    65
    >>> ord('中')
    20013
    >>> chr(66)
    'B'
    
* 当 Python 解释器读取源代码时，为了让它按UTF-8 编码读取，我们通常 在文件开头写上这:


    # -*- coding: utf-8 -*-

* 在字符串内部，%s 表示用字符串替换，%d 整数，%f 浮点数，%x 十六进制整数，有几个%?占位符，后面就跟几 个变量或者值，顺序要对应好。如果只有一个%?，括号可以省略。如果你不太确定应该用什么，%s 永远起作用，它会把任何数据类型转换 为字符串。

* 对于不变对象来说，调用对象自身的任意方法，也不会改变该对 象自身的内容。相反，这些方法会创建新的对象并返回，这样，就保证 了不可变对象本身永远是不可变的。

    
    >>> a = 'abc'
    >>> a.replace('a', 'A')
    'Abc'
    >>> a
    'abc'
    
* 函数的默认参数尽量使用不可变对象，以免出现BUG。Python 函数在定义的时候，默认参数 L的值就被计算出来了，即[]，因 为默认参数 L也是一个变量，它指向对象[]，每次调用该函数，如果改 变了 L 的内容，则下次调用时，默认参数的内容就变了，不再是函数定 义时的[]了。
    
    
    def add_end(L=[]):
        L.append('END')
        return L
        
    >>> add_end()
    Out[3]: ['END']
    >>> add_end()
    Out[4]: ['END', 'END']

* 此外，由于对象不变，多任务环境下同时读取对象不需要加锁，同时读 一点问题都没有。我们在编写程序时，如果可以设计一个不变对象，那 就尽量设计成不变对象。

* pass 语句什么都不做，那有什么用？实际上 pass 可以用来作为占位符， 比如现在还没想好怎么写函数的代码，就可以先放一个 pass，让代码能 运行起来。

* Python 的函数返回多值其实就是返回一个 tuple。

* 把函数的参数改为可变参数：


    def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n**2
    return sum
    
    >>> calc(1,2)
    Out[3]: 5
    >>> calc()
    Out[4]: 0
    >>> nums = [1, 2, 3]
    >>> calc(*nums) # *nums 表示把 nums这个 list 的所有元素作为可变参数传进去。
    Out[6]: 14

* ** extra 表示把 extra这个 dict 的所有 key-value 用关键字参数传入到函 数的**kw 参数，kw将获得一个 dict，注意 kw 获得的 dict 是 extra 的一份 拷贝，对 kw 的改动不会影响到函数外的 extra。

* 如果要限制关键字参数的名字，就可以用命名关键字参数，例如，只接 收 city 和 job 作为关键字参数。这种方式定义的函数如下,和关键字参数**kw 不同，命名关键字参数需要一个特殊分隔符*，*后面 的参数被视为命名关键字参数。


    def person(name, age, *, city, job): 
        print(name, age, city, job)
        
* 对于任意函数，都可以通过类似 func(*args, **kw)的形式调用它， 无论它的参数是如何定义的。

* 遗憾的是，大多数编程语言没有针对尾递归做优化，Python 解释器也没 有做优化，所以，即使把上面的 fact(n)函数改成尾递归方式，也会导 致栈溢出。

* 切片操作
    
    
    >>> a = [1,2,3,4,5,6,7,8,9]
    >>> a[::-1]
    Out[14]: [9, 8, 7, 6, 5, 4, 3, 2, 1]
    # a[x:y:z]，x起始位置，y终止位置，z步进

* 可迭代对象，列表，元组，字典，字符串等等，方法是通过 collections 模块 的 Iterable 类型判断：


    >>> from collections import Iterable
    >>> isinstance('abc', Iterable) # str 是否可迭代
    
* 在 Python 中，这种一边循环一边计算的机制，称 为生成器：generator。要创建一个 generator，有很多种方法。第一种方法很简单，只要把一个 列表生成式的[]改成()，就创建了一个 generator：


    >>> g = (x * x for x in range(10))
    >>> g
    <generator object <genexpr> at 0x1022ef630>
使用next(g)不太实用，正确的方法是使用 for 循环，因为 generator 也是可迭代对象。

定义 generator 的另一种方法。如果一个函数定义中包含 yield 关 键字，那么这个函数就不再是一个普通函数，而是一个 generator：

    def fib(max):
        n, a, b = 0, 0, 1 
        while n < max: 
            yield b
            a, b = b, a + b 
            n = n + 1
        return 'done'

* 凡是可作用于 next()函数的对象都是 Iterator 类型，它们表示一个惰性 计算的序列。集合数据类型如 list、dict、str等是 Iterable 但不是 Iterator，不过可 以通过 iter()函数获得一个 Iterator对象。

* for循环等价于一个Iterator。Python 的 for循环本质上就是通过不断调用 next()函数实现的，例如：


    for x in [1, 2, 3, 4, 5]: 
        pass
    # 实际上完全等价于：
    it = iter([1, 2, 3, 4, 5])

* 函数名也是变量

    
    >>> abs(-1)
    Out[2]: 1
    >>> abs = 1
    >>> abs(-1)
    TypeError: 'int' object is not callable

* map()函数接收两个参数，一个是函数，一个是 Iterable， map 将传入的函数依次作用到序列的每个元素，并把结果作为新的 Iterator 返回。

* reduce 把一个函数作用在一个序列[x1, x2, x3, ...] 上，这个函数必须接收两个参数，reduce把结果继续和序列的下一个元 素做累积计算。

* 和 map()类似，filter()也接收一个函数和一个序列。和 map()不同的时， filter()把传入的函数依次作用于每个元素，然后根据返回值是 True 还 是 False 决定保留还是丢弃该元素。由于 filter()使 用了惰性计算，所以只有在取 filter()结果的时候，才会真正筛选并每 次返回下一个筛出的元素。

* sorted()函数也是一个高阶函数，它还可以接收一个 key 函数来 实现自定义的排序，key 指定的函数将作用于 list 的每一个元素上，并根据 key 函数返回的 结果进行排序。

* 默认情况下，对字符串排序，是按照ASCII 的大小比较的，要进行反向排序，可以传入第三个参数reverse=True。

* 闭包函数，一个函数可以返回一个计算结果，也可以返回一个函数。返回一个函数时，牢记该函数并未执行，返回函数中不要引用任何可能 会变化的变量。

* 关键字 lambda表示匿名函数，冒号前面的 x 表示函数参数。


    lambda x: x * x

* 装饰器，假设我们要增强 now()函数的功能，比如，在函数调用前后自动 打印日志，但又不希望修改 now()函数的定义，这种在代码运行期间动 态增加功能的方式，称之为“装饰器”（Decorator）。


    def log(func):
        def wrapper(*args, **kw):
            print('call %s():' % func.__name__)
            return func(*args, **kw)
        return wrapper
        
    @log
    def now():
        print('2017-10-29')
        
    # 把@log 放到 now()函数的定义处，相当于执行了语句：
    now = log(now)

* 偏函数，functools.partial 的作用就是，把一个函数的某些参数 给固定住（也就是设置默认值），返回一个新的函数，调用这个新函数 会更简单。


    >>> import functools
    >>> int2 = functools.partial(int, base=2) 
    >>> int2('1000000') 
    64
    >>> int2('1010101') 
    85

* 每一个包目录下面都会有一个__init__.py 的文件，这个文件是 必须存在的，否则，Python 就把这个目录当成普通目录，而不是一个包。

* 自己创建模块时要注意命名，不能和 Python 自带的模块名称冲突。例 如，系统自带了 sys模块，自己的模块就不可命名为 sys.py，否则将无 法导入系统自带的 sys 模块。

* 当我们在命令行运行模块文件时，Python 解释器把一个特殊变量 把__name__置为__main__，而如果在其他地方导入该模块时，if 判断 将失败，因此，这种 if 测试可以让一个模块通过命令行运行时执行一 些额外的代码，最常见的就是运行测试。


    if __name__=='__main__': 
        test()

* 正常的函数和变量名是公开的（public），可以被直接引用，比如：abc， x123，PI 等；类似__xxx__这样的变量是特殊变量，可以被直接引用，但是有特殊用途；类似_xxx 和__xxx这样的函数或变量就是非公开的（private），不应该被 直接引用，比如_abc，__abc 等。

* 和普通的函数相比，在类中定义的函数只有一点不同，就是第一个参数 永远是实例变量 self，并且，调用时，不用传递该参数。除此之外，类 的方法和普通函数没有什么区别，所以，你仍然可以用默认参数、可变 参数、关键字参数和命名关键字参数。


    class Student(object):
            
        def __init__(self, name, socre):
            self.name = name
            self.score = score
            
        def print_socre(self):
            print(self.score)
            
    ################################
    >>> bart = Student() 
    >>> bart
    <__main__.Student object at 0x10a67a590> 
    >>> Student
    <class '__main__.Student'>


* 如果要让内部属性不被外部访问，可以把属性的名称前加上两个下划线 __，在 Python 中，实例的变量名如果以__开头，就变成了一个私有变量 （private），只有内部可以访问，外部不能访问。


    self.__name = name 
    self.__score = score
    
* 双下划线开头的实例变量是不是一定不能从外部访问呢？其实也不是。 不能直接访问__name是因为 Python 解释器对外把__name 变量改成了 _Student__name，所以，仍然可以通过_Student__name 来访问__name 变量。

* 继承有什么好处？最大的好处是子类获得了父类的全部功能。


    class Animal(object): 
        def run(self):
            print('Animal is running...')
            
    class Dog(Animal): 
        pass
        
    class Cat(Animal): 
    pass
    
    >>> dog = Dog() 
    >>> dog.run()
    
    >>> cat = Cat() 
    >>> cat.run()
    
* 当子类和父类都存在相同的 run()方法时，我们说，子类的 run()覆盖了 父类的 run()，在代码运行的时候，总是会调用子类的 run()。这样，我 们就获得了继承的另一个好处：多态。

* 在继承关系中，如果一个实例的数据类型是某个子类，那它的数 据类型也可以被看做是父类。

* 多态的好处就是，当我们需要传入 Dog、Cat、Tortoise……时，我们只 需要接收 Animal 类型就可以了，因为 Dog、Cat、Tortoise……都是 Animal 类型，然后，按照 Animal 类型进行操作即可。由于 Animal类型有 run() 方法，因此，传入的任意类型，只要是 Animal 类或者子类，就会自动调 用实际类型的 run()方法，这就是多态的意思

* 对于静态语言（例如 Java）来说，如果需要传入 Animal 类型，则传入的 对象必须是 Animal类型或者它的子类，否则，将无法调用 run()方法。

* 对于 Python 这样的动态语言来说，则不一定需要传入 Animal 类型。我 们只需要保证传入的对象有一个 run()方法就可以了。这就是动态语言的“鸭子类型”，它并不要求严格的继承体系，一个对象 只要“看起来像鸭子，走起路来像鸭子”，那它就可以被看做是鸭子。

* 配合 getattr()、setattr()以及 hasattr()，我们可以直接操作一个对象的状态。


    >>> hasattr(obj, 'x') # 有属性'x'吗？ 
    True
    >>> obj.x 
    9
    >>> hasattr(obj, 'y') # 有属性'y'吗？ 
    False
    >>> setattr(obj, 'y', 19) # 设置一个属性'y' >>> hasattr(obj, 'y') # 有属性'y'吗？ 
    True
    >>> getattr(obj, 'y') # 获取属性'y' 
    19
    >>> obj.y # 获取属性'y' 
    19
    
* 可以给类本身绑定属性，如果实例没有该属性，会调用类属性，类似全局变量。


    class Student(object): 
    name = 'Student'
    
    >>> class Student(object): ...
    name = 'Student' ...
    >>> s = Student() # 创建实例 s 
    >>> print(s.name) # 打印 name 属性，因为实例并没有 name 属性，所以会继续 查找 class 的 name 属性 
    Student
    >>> print(Student.name) # 打印类的 name 属性 
    Student
    >>> s.name = 'Michael' # 给实例绑定 name 属性 
    >>> print(s.name) # 由于实例属性优先级比类属性高，因此，它会屏蔽掉类的 name 属性 
    Michael
    >>> print(Student.name) # 但是类属性并未消失，用 Student.name 仍然可以 访问
    Student
    
* 动态语言可以在类定义完后继续给实例或者类绑定属性和方法


    >>> from types import MethodType 
    >>> s.set_age = MethodType(set_age, s) # 给实例绑定一个方法，set_age为自定义函数

* 在类中使用__slots__变量来限制实例的属性，但对继承它的子类不起作用


    class Student(object):
        __slots__ = ('name', 'age') # 用 tuple 定义允许绑定的属性名称

* 使用@property，用类似装饰器的方法将类的方法变成简单的属性调用。

* 通过多重继承，一个子类就可以同时获得多个父类的所有功能。这 种设计通常称之为MixIn。

* 更改直接打印实例返回的信息，其中__str__()返回用户看到的字符串，而__repr__()返回程序开发者 看到的字符串


    def __str__(self):
        return 'Student object (name=%s)' % self.name 
    __repr__ = __str__

* 如果一个类想被用于 for ... in 循环，类似 list 或 tuple 那样，就必须实 现一个__iter__()方法，该方法返回一个迭代对象，然后，Python 的 for 循环就会不断调用该迭代对象的__next__()方法拿到循环的下一个值， 直到遇到 StopIteration 错误时退出循环。

* Python 所有的错误都是从 BaseException类派生的。

* Python 内置的 logging 模块可以非常容易地记录错误信息。


    except Exception as e: 
        logging.exception(e)

* 虽然用 IDE 调试起来比较方便，但是最后你会发现，logging 才是终极 武器。

* StringIO顾名思义就是在内存中读写 str。

* StringIO操作的只能是str，如果要操作二进制数据，就需要使用BytesIO。

* 多任务并行运行，操作系统轮流让各个任务交替执行，任务 1 执行 0.01 秒，切换 到任务 2，任务 2 执行 0.01 秒，再切换到任务 3，执行 0.01 秒……这样 反复执行下去。

* 对于操作系统来说，一个任务就是一个进程（Process）。

* 在一个进程内部，要同时干多件事，就需要同时 运行多个“子任务”，我们把进程内的这些“子任务”称为线程（Thread）。由于每个进程至少要干一件事，所以，一个进程至少有一个线程。


