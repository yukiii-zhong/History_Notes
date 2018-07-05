# Python Learning Notes

### Print in a line

```python
print('Hello', end = "")
print('World', end = "?")
print('!')
```

```
Hello World?!
```

Usage

```python
for letter in hand.keys():
    for j in range(hand[letter]):
        print(letter, end =" ")
```



### Global Variable

在def function中使用`global`



### 运算符号（Exponent，Mod）

```python
1. Exponent 
eggs = 10**2        #eggs=10^2
print eggs          #print 10

2. Modulo (Mod)
spam = 9%4       #9 mod 4
print spam		#print 1

-10%4 =  2
10%-4 =  -2
-10%-4 =  -2


3. 整除
print (9//4)     #2 

4.divmod
width, reminder = divmod(9,2)
print(width)		#4
print(reminder)		#1

5. log
import math
math.log(n,[base])
math.log10(n)
```



## float —> int

`int()`

```python
n = 7
middle = int(n/2)
```



## Module(import) & Files

### Module

```python
import circule
print(circule.pi)
print(circule.area(3))
```

## Cha1. Strings, Tuples, Ranges, Lists, Set

### 1.0 Common Operations

`seq1+seq2` —>concatenation of sequences (not range)

`n*seq` —>sequence that repeats seq n times (not range)

`e in seq` —>True/ False

`e not in seq`

`for e in seq`

`seq[i]`

`len(seq)`

`seq[start:end]`

Notes: only Lists are mutable

### 1.1 Tuples & Lists

#### Tuples 

```python
t1 = (2, "one", 3)
t2 = (4, 5)
t3 = t1 + t2 
print(t3)
print(t3[0])
print(t3[0:1])
print(t3[0:-1])
```

```
(2,"one",3, 4, 5)
2
(2,) #Indicate it's a tuple
(2,"one",3, 4)
```

##### Immutale

```python
t3 = (2,"one",3, 4, 5)
t3[0] = 4
```

```
ERROR
```

#### Lists

##### Mutable: Add&Remove

1. `List.append()`

```python
L1 = [1, 3, ['one'],4,5]
L1.append(6)
print(L1)
```

```
[1, 3, ['one'],4,5,6]
```

2. `List.extend([NewList])`

```python
L1 = [1,2,3]
L2 = [4,5,6]
L1.extend(L2)
print(L1)
```

```
[1, 2, 3, 4, 5, 6]
```

3. `List.remove()`

   `del(L[1])`

   `L.pop()`

```python
L = [2,1,3,6,3,7,0]
L.remove(6)			#[2, 1, 3, 3, 7, 0]
print(L)
del(L[1])			#[2, 3, 3, 7, 0]
print(L)
L.pop()				#[2, 3, 3, 7]
print(L)
```

```
[2, 1, 3, 3, 7, 0]
[2, 3, 3, 7, 0]
[2, 3, 3, 7]
```



##### Convert Lists to Strings and Back

1. String —> List

   `list(string)`

   `string.split()`

```python
s = "I <3 CS"
L1 = list(s)         
L2 = s.split('<')
print(L1)
print(L2)


name = "Nick A"
print ("lastname: " + str(name.split(" ")[-1]))
```

```
['I', ' ', '<', '3', ' ', 'C', 'S'] 
['I ', '3 CS']						

A
```

2. List —>String

   `' '.join(L)`

   ```python
   L=['a','b','c']
   L2 = ''.join(L)
   L3 = '_'.join(L)
   print(L2)
   print(L3)
   ```

   ```
   abc
   a_b_c
   ```



##### Copy a list

```python
L1 = [0,1,2,3,4]
L2 = L1[:]      # Copy the entire L1
L3 = L1[1:3]	# L3 = [1, 2]
L4 = L1[:3]		# L3 = [0, 1, 2]
L5 = L1[1:]		# L5 = [1,2,3,4]
```



##### sort(), sorted(), reverse()

```python
L=[9,6,0,3]
L2 = sorted(L)# return a sorted list
print(L2)
print(L)
```

```
[0,3,9,6]
[9,6,0,3]
```

```python
L.sort()
print(L)
L.reverse()
print(L)
```

```
[0,3,6,9]
[9,6,3,0]
```

##### index()

```python
>>> aList = [1,2,3]
>>> aList.index(3)
2
```





### 1.2 Function As objects

#### Apply function to each node of list

```python
def applyToEach(L, f):
	"""assumes L is a list, 
    f a function mutates L 
    by replacing each element,e, of L by f(e)"""
    for i in range(len(L)):
        L[i] = f(L[i])

L = [1, -3.2, -5]
applyToEach(L,abs)
print(L)
```

```
[1, 3.2, 5]
```

#### List of Functions

```python
def applyFuncs(L,x):
    #L: a list of functions
    for f in L:
        print(f(x))

L = [abs, int]
applyFuncs(L,-3.4)
```

```
3.4
-3
```

#### HOP:map

`map(function, iterable, ...)`

```python
def square(x):
    return x**2

L1 = [2,-4,-7]
newL1 = list(map(square,L1))
print(newL1)
```

```
[4, 16, 49]
```

Use `map` with `lambda`

```python
L1 = [1,2,4]
L2 = [23,5,8]
newT = tuple(map(lambda x,y : x+y, L1,L2))
print(newT)
```

```
(24, 7, 12)
```

### 1.3 Dictionary

Key-value pair

1. **Keys** must be immutable(hashable)

   Type:int, float, string, **tuple**, **bool**

2. **Values** can of any type

3. **No Order** to keys or values

4. Dictionary is **Mutable**

Example:

`grades = {'Ana':'B', 'John':'A+', 'Denise':'A', 'Katy':'A'}`

`grades['John']`—>'A+'

#### Operations (add, test,delete) (get Keys, values)

```python
grades = {'Ana':'B', 'John':'A+', 'Denise':'A', 'Katy':'A'}

#add
grades['Sylvan'] ='A'

#test if KEY in the dictionary
'John' in grades  #return True
'Danel' in grades  #return False

#DEl
del(Grades['Ana'])

#Get Keys
grades.keys()     #return a list: ['Denise','Katy','John','Ana']

#Get Values
grades.values()    #return a list: ['A', 'A', 'A+', 'B']  
```

### 1.4 Set

https://blog.csdn.net/business122/article/details/7541486



#### 1. 可以将Iterable 转换为Set, 但其中的重复内容会删除

```python
a = [1,1,2,2,3,4]
b = set(a)		# b: {1,2,3,4}

t = set('Hello') # t: {'H','e','l','o'}
```



#### 2. 集合的标准操作

```python
a = t|s		# t 和 s的并集  

b = t&s		# t 和 s的交集 

c = t-s		# 求差集（项在t中，但不在s中） 

d = t^s		# 对称差集（项在t或s中，但不会同时出现在二者中）  
```



#### 3. 增减，基本操作

```python
t.add('x')		# 添加‘x’

s.update([10,36,21]) # 在s中添加多项

t.remove('H')	# 删除‘H’

```



## Cha2. Exceptions, Assertions

### Exceptions

#### Handle Exceptions

```python
try: 
    a = int(input("Tell me one number: ")) 
    b = int(input("Tell me another number: ")) 
    print("a/b = ", a/b) 
    print("a+b = ", a+b) 
except ValueError: 
    print("Could not convert to a number.”) 
except ZeroDivisionError: 
	print("Can't divide by zero”) 
except: 
    print("Something went very wrong.”)
```

#### 'else', 'finally' in exceptions

1. `else`: If try statement works, do the `else` statement
2. `finally`: No matter try or except works, do the finally statement 

```python
data = []
file_name = input("Provide a name of a file of data ")

try:
    fh = open(file_name, 'r')
except IOError:
    print('cannot open', file_name)
else:                       #else-->if try works
    for new in fh:
        if new !='\n':
            addIt = new[:-1].split(',')
            data.append(addIt)
finally:
    fh.close()              #finally -->do no matter try or except works
```

### Assertions

`assert` execution halts whenever an expected condition is not met

if `assert` statement is not met, raise an **AssertionError**

```python
def avg(gradesList):
    '''gradesList is a List containing seversal grades'''
    assert not len(gradesList)==0, 'no grades data'
    return sum(gradesList)/len(gradesList)   # Execute return if 通过了assert statement
```



## Cha3: Classes & Inheritance

### 3.1 `__init__` `__str__`method

```python
class Coordinate(object):
    def __init__(self,x,y):
        self.x = x
        self.y = y

    def distance(self, other):
        x_diff_sq = (self.x - other.x)**2
        y_diff_sq = (self.y - other.y)**2
        return  (x_diff_sq + y_diff_sq)**0.5

    def __str__(self):
        return "<"+str(self.x)+", "+ str(self.y)+">"
   
    def __eq__(self, other):
        if self.x == other.x and self.y ==other.y:
            return True
        else:
            return False

	#Represent 
    def __repr__(self):
        return  "Coordinate(" +str(self.getX()) +","+str(self.getY())+")"
    
#Instance
c = Coordinate(3, 4)
origin = Coordinate(0,0)

#Call method
print(Coordinate.distance(c,origin))
print(c.distance(origin))

#__str___
print(c)
print()

#type
print(isinstance(c,Coordinate))
print(type(c))
print(Coordinate)
print(type(Coordinate))
    
```

```
5.0
5.0
<3, 4>

True
<class '__main__.Coordinate'>
<class '__main__.Coordinate'>
<class 'type'>
```

### 3.2 Ex2: Fraction

```python
class fraction(object):

    def __init__(self, number, denom):
        self.number = number
        self.denom = denom

    def __str__(self):
        return str(self.number) + '/' + str(self.denom)

    def getNumber(self):
        return self.number

    def getDenom(self):
        return self.denom

    def __add__(self, other):
        numberNew = self.getDenom()*other.getNumber()+other.getDenom()*self.getNumber()
        denomNew = self.getDenom()*other.getDenom()
        return fraction(numberNew,denomNew)


F1 = fraction(2,5)
F2 = fraction(3,4)

print(F1+F2)           #23/20
```

### 3.3 Inheritance

```python
class Animal(objcet):

class Cat(Animal):
    ...
```

```python
class Animal(object):
    def __init__(self,age):
        self.age = age
        self.name = None
    def set_name(self,newName):
        self.name = newName
        
class Person(Animal):
    def __init__(self,name,age):
        Animal.__init__(self,age)
        Animal.set_name(self,name)
        self.friends = []
```

### 3.4 Generate  `yield`

```python
def genPrimes():
    candidate = 2
    primeSet = []
    
    while True:
        isPrime = True
        for p in primeSet:
            if candidate % p ==0:
                isPrime = False
        if isPrime == True:
            primeSet.append(candidate)
            yield candidate
            
        candidate +=1

test = genPrimes()
for i in range(3):
    print(test.__next__())
    print(next(test))
    # the 2 statements above are the same, so will generate 6 numbers
```

1. 下次运行yield statement，从yield 结束开始

2. yield 适用于不需要长期保存的数据：we don't ultimately want (or won't want for a long time)

   the value yielded would not be stored.

# Pylab

## 调用环境（Pycharm)

1. 安装Matplotlib
2. Run --> Edit Configurations --> Add Environment Variabes "Display True"

## plot

### Using EXAMPLE

#### import pylab`, 定义变量（本EX中）

```python
import pylab as plt

mySamples = []
myLinear = []
myQuadratic =[]
myCubic = []
myExponential = []

for i in range(0,30):
    mySamples.append(i)
    myLinear.append(i)
    myQuadratic.append(i**2)
    myCubic.append(i**3)
    myExponential.append(1.5**i)
```

#### Draw a figure

```python
# open a figure window called 'lin'
plt.figure('lin')
# cler the figure
plt.clf()
# give the title
plt.title('Linear')
# label the X axis, Y axis
plt.xlabel('mySamples')
plt.ylabel('myLinear')
# plot it (X axis, Y axis)
plt.plot(mySamples,myLinear)
```

#### Overlaying Plots

```python
plt.figure('lin quad')
#It's better to clear the figure before use it.
plt.clf()
#drawing in the same picture
plt.plot(mySamples,myLinear, label = 'linear')
plt.plot(mySamples,myQuadratic, label = 'quardratic')
#展示图例，you can also call `plt.legeng()`, altomatically select the best fit location
plt.legend(loc = 'upper left')
plt.title('linear vs Quadratic')
```

#### Changing data display & Changing scales

The default scale is 'linear'

```python
plt.figure('lin quad')
plt.clf()
#Style 'b-'-->blue, 线性； 'ro', red,圆圈
plt.plot(mySamples,myLinear,'b-',label = 'linear', linewidth = 2.0)
plt.plot(mySamples,myQuadratic,'ro',label ='quadratic', linewidth = 3.0)
#Change scale
plt.yscale('log')
plt.ylabel('Value(loged)')
#You have to set label for each plot, before you call the legend
plt.legend()
plt.title('Linear vs. Quadratic')

#Second figure
plt.figure('cube exp')
plt.clf()
plt.title('Cubic vs, Exponential')
#Style 'g^'-->green, 三角； 'r--', red, --
plt.plot(mySamples,myCubic,'g^', label = 'cubic',linewidth = 4.0)
plt.plot(mySamples,myExponential, 'r--', label = 'exponential',linewidth = 5.0)
plt.legend()
```

#### Using subplots

```python
plt.figure('lin quad')
plt.clf()

# set a subplot for this figure
#211 means: 2 rows, 1 column, location 1
plt.subplot(211)
plt.ylim(0,900)
plt.plot(mySamples,myLinear,'b-', label = 'linear', linewidth = 2.0)

#set a subplot for this figure
# 212 means: 2 rows, 1 column, location 2
plt.subplot(212)
plt.ylim(0,900)
plt.plot(mySamples,myQuadratic,'r',label = 'quaratic', linewidth = 3.0)

```



