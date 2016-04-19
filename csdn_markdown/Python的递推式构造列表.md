Python的递推式构造列表（List comprehension） 
===========================================
python语言的一种重要原则（zen）就是简洁、自然，递推式构造列表(List)、字典(dict)就是一个很好的例子。

我们的代码在初始化一个List或者dict时经常是这样写的：

	new_list = []
	for i in old_list:
		if filter(i):
			new_list.append(expressions(i))

但其实python提过了一个非常简洁的写法，只要一行：

	new_list = [expression(i) for i in old_list if filter(i)]

一个更简单的方式是

	[ expression for item in list if conditional ]

更进一步的像下面

	[ expression for item in list ]

我们要创建一个列表，是从零到十的平方，普通的写法像下面这样：

	squares = []
	for x in range(11):
		squares.append(x**2)

递推式构造列表写法只要一行

	squares = [x**2 for x in range(11)]

是不是简洁多了？另外递推式构造列表支持嵌套的写法，比如下面这个找出30以内所有能构成直角三角形的数组，原来我们要这样写：

	num = []
	for x in range(1,30):
		for y in range(x,30):
			for z in range(y,30):
				if x**2 + y**2 == z**2:
					num.append((x,y,z))

递推式构造列表写法还是只要一行，简单吧

	[(x,y,z) for x in range(1,30) for y in range(x,30) for z in range(y,30) if x**2 + y**2 == z**2]

但递推式构造列表里只能使用if，没有else，但是我们通过函数来实现，比如

	def expr(i):
		if i%2==0:
			return "e"
		else:
			return "o"

	lst = [expr(i) for i in range(20)]

另外我们可以递推式构造字典，比如下面的例子：

	import string

	dct = {c:ord(c) for c in string.ascii_lowercase}