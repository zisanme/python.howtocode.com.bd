## ডাটা হাইডিং

অবজেক্ট ওরিয়েন্টেড প্রোগ্রামিং -এ এনক্যাপসুলেশন (Encapsulation) একটি গুরুত্বপূর্ণ কনসেপ্ট যার অর্থ কিছু ভ্যারিয়েবল এবং ফাংশনকে একত্রিত করে একটি সিঙ্গেল ইউনিট হিসেবে প্রকাশ করা। এই কনসেপ্টে একটি ক্লাসের ভ্যারিয়েবল গুলোকে অন্য ক্লাস এর কাছ থেকে আড়ালে রাখা হয় এবং শুধুমাত্র ওই ক্লাসের নির্দিষ্ট মেথডের মাধ্যমে অ্যাক্সেস করার পারমিশন থাকে। এজন্য এই কনসেপ্টকে **ডাটা হাইডিং** -ও বলা হয়ে থাকে। অন্যভাবে বলা হয়, একটি ক্লাসের ইমপ্লিমেন্টেশন ডিটেইল গুলো আড়ালে রাখা।    

> সাধারণ অবজেক্ট ওরিয়েন্টেড প্রোগ্রামিং এর চারটি গুরুত্বপূর্ণ কনসেপ্ট হচ্ছে - **encapsulation, inheritance, polymorphism, and abstraction.**   


অন্যান্য প্রোগ্রামিং ল্যাঙ্গুয়েজে একটি ক্লাসের অ্যাট্রিবিউট ও মেথড গুলোকে নির্দিষ্ট কিওয়ার্ড (অ্যাক্সেস মডিফায়ার) ব্যবহার করে প্রাইভেট বা প্রটেক্টেড হিসেবে ডিফাইন করে এই উদ্দেশ্য পূরণ করা হয়ে থাকে। এর মাধ্যমে ওই ক্লাসের ওই নির্দিষ্ট মেথড বা অ্যাট্রিবিউট গুলোকে বাইরের ক্লাস থেকে অ্যাক্সেস করা থেকে বিরত রাখা হয়।    

**কিন্তু,** পাইথনে এই বিষয়টাকে একটু আলাদাভাবে দেখা হয়। বলা হয়ে থাকে - *"we are all consenting adults here"*  অর্থাৎ - একটি ক্লাসের কোন এলিমেন্টকে শক্তভাবে বাইরের অ্যাক্সেস থেকে বিরত রাখার ব্যবস্থা করা উচিৎ নয়। আর তাই, পাইথনে সত্যিকারের কোন পদ্ধতি নেই যার মাধ্যমে একটি ক্লাসের অ্যাট্রিবিউট বা মেথডকে প্রাইভেট হিসেবে ডিফাইন করা যেতে পারে।  বরং, এধরনের এলিমেন্ট গুলোকে বাইরে থেকে অ্যাক্সেস করতে নিরুৎসাহিত করা হয় এবং এগুলো যে আসলে ক্লাসের ইমপ্লিমেন্টেশন ডিটেইল তা প্রকাশ করার মাধ্যমে এগুলোর সরাসরি অ্যাক্সেস/ব্যবহার বন্ধ রাখতে বলা হয়।  

**উইকলি প্রাইভেট**   
অ্যাট্রিবিউট এবং মেথডের নামের শুরুতে একটি আন্ডারস্কোর ব্যবহার করে এরকম প্রাইভেট এলিমেন্ট গুলোকে ডিফাইন করা হয়ে থাকে। আবার বলতে হচ্ছে - এভাবে প্রাইভেট এলিমেন্ট হিসেবে ডিফাইন করে এটাই প্রকাশ করা হয় যে, বাইরের কোড থেকে এগুলো অ্যাক্সেস করার দরকার নেই বা উচিৎ নয়। কিন্তু তার মানে এই না যে এগুলোকে অ্যাক্সেস করা যাবে না।   

```python
class Queue:
    def __init__(self, contents):
        self._hiddenlist = list(contents)

    def push(self, value):
        self._hiddenlist.insert(0, value)

    def pop(self):
        return self._hiddenlist.pop(-1)

    def _show_list(self):
        return self._hiddenlist
        

queue = Queue([1, 2, 3])
print(queue._hiddenlist)

queue.push(0)
print(queue._hiddenlist)

queue.pop()
print(queue._hiddenlist)

print(queue._show_list())        
```        

আউটপুট, 

```python
[1, 2, 3]
[0, 1, 2, 3]
[0, 1, 2]
[0, 1, 2]
```
 
উপরের উদাহরণে, কিছু উইকলি প্রাইভেট এলিমেন্ট ডিফাইন করা থাকলেও সেগুলো ক্লাসের বাইরে থেকে অ্যাক্সেস করা গেছে।   

**কিন্তু হ্যাঁ**, এভাবে ডিফাইন করা ভ্যারিয়েবল	নিয়ে তৈরি একটি পাইথন ফাইলকে মডিউল হিসেবে ইম্পোরট করলে ওই প্রাইভেট ভ্যারিয়েবল গুলো ইম্পোরট হয় না। এতে করে এগুলোর সরাসরি অ্যাক্সেস বাধাগ্রস্ত রাখা হয়। অর্থাৎ, `from module_name import *` কোড ব্যবহার করলেও `module_name` এর মধ্যে থাকা আন্ডারস্কোর ওয়ালা ভ্যারিয়েবল গুলো ইম্পোরট হবে না।   

উদাহরণ, 

```python
# myfile.py
_my_private_variable = 10
```

```python
# data-hiding-test.py
from myfile import *


print(_my_private_variable)
```

`data-hiding-test.py` ফাইলকে রান করলে আউটপুট আসবে, 

```python
Traceback (most recent call last):
  File "/Users/nuhil/Documents/Python/data-hiding-test.py", line 4, in <module>
    print(_my_private_variable)
NameError: name '_my_private_variable' is not defined
```   

**স্ট্রংলি প্রাইভেট**   
এ ধরনের অ্যাট্রিবিউট ও মেথডের নামের শুরুতে ডাবল আন্ডারস্কোর ব্যবহার করা হয়। পাইথন এরকম নামের অ্যাট্রিবিউট বা মেথড পেলে এগুলোর নামকে আরেক্টু পরিবর্তন করে ফেলে। এতে করে ক্লাসের বাইরে থেকে সেই ডিফাইন করা নামে এদেরকে আর অ্যাক্সেস করা যায় না। 

> মূলত অ্যাক্সেস রোধ করার জন্য এরকম করা হয় না বরং একটি ক্লাসের সাবক্লাসে যদি একই নামের এলিমেন্ট থাকে তাহলে যেন সেগুলোর সাথে কনফ্লিক্ট না করে। 

উদাহরণ,   

```python
class Spam:
    __egg = 7

    def print_egg(self):
        print(self.__egg)

s = Spam()
s.print_egg()
print(s.__egg)
```    

আউটপুট, 

```python
7
Traceback (most recent call last):
  File "/Users/nuhil/Documents/Python/myfile.py", line 10, in <module>
    print(s.__egg)
AttributeError: 'Spam' object has no attribute '__egg'
```

যদিও নিচের মত করে ঠিকি ওই প্রাইভেট এলিমেন্টকে অ্যাক্সেস করা যায়,   

```python
class Spam:
    __egg = 7

    def print_egg(self):
        print(self.__egg)

s = Spam()
s.print_egg()
print(s._Spam__egg)
```

আউটপুট, 

```python
7
7
```

অর্থাৎ, পাইথন আসলে আড়ালে, ডাবল আন্ডারস্কোর ওয়ালা এলিমেন্টের নামের সাথে তার ক্লাসের নামটি জুড়ে দেয় আর তাই `s._Spam__egg` ব্যবহার করে `Spam` ক্লাসের `__egg` কে অ্যাক্সেস করা হয়েছে। 


>  সংকলন - [নুহিল মেহেদী](https://nuhil.net)


  
  

