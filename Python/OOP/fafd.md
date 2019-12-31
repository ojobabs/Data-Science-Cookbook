
> Written with [StackEdit](https://stackedit.io/).

# What is Object Oriented Programming and Why?

> Section 1 - Lesson 2 of Udemy course: _Python Beyond the Basics - Object-Oriented Programming_ 

## Object-Oriented Programming (OOP)

So what is object oriented programming.

- Well it was invented in the 1960s for a language called Simula 67 and then it was later picked up and used a little more widely in a language called Smalltalk.
- The simplest way to talk about object oriented programming is as a paradigm or as a way of organizing our code.
- As you've probably realized all programs are comprised of code that's designed to process data.
- We store the data temporarily in variables and then we call functions to process the variables.
    - The object oriented paradigm organizes the data into specially designed entities called **objects** and, the functionality for processing the data, into the specialized functions that we call **methods**.
    - The design of these objects and methods is specified in a kind of a blueprint which we call a **class**.

- This paradigm is one of the most important advances in software design.

- It promotes collaboration and the extension and maintenance of our code.

- And because it's ability to help us manage complexity is so profound it is the primary paradigm used for software design.

- It's hard to overstate just how important it is to programmers every day. And it's simple enough to begin implementing, that it can make your coding work easier every day too.

## Procedural vs. Object paradigm

Now as a way of explaining the difference between object oriented code and non object oriented code. Let's look at a really simple example.

#### Procedural paradigm

The below code is what we call **procedural code**. That's the word they use when they mean non object oriented. As you can see, we're taking an integer and passing it to a function called increment. Then catching the result in the same variable name. In the end we print the integer and you can see it's been incremented twice.

```python
this = 0
this = increment(this)
this = increment(this)
print(this)
```
```
2
```

#### Object paradigm

Compare this code to the below code. `this` is not an integer in the object paradigm. `this` is `MyCustomInt()` object. It's an object that I designed myself in a class called `MyCustomInt()`. `MyCustomInt()` includes a method called `increment` and I'm calling `increment` on the object.

```python
this = MyCustomInt()
this.increment()
this.increment()
print(this)
```
```
2
```

> `this` is `MyCustomInt` object


Now the result is the same. And you can imagine that within `MyCustomInt` object there is an integer there but, again it's not an integer. It's been designed specifically to my specification and I've included a special method to work with it.

It that doesn't illustrate exactly why we need objects but it does show the difference in the procedural paradigm.

We might design a function that works with an integer and it would be doing the same work as the object.

The differences in the object paradigm we actually have a custom type of object that has its own special method for doing this incrementing. The functionality and the data are connected.

And that's really the best way to begin thinking about objects data plus functionality.

> One definition of _object_: a unit of _data_ that has associated _functionality_.

## Procedural vs. Object paradigm: Library Code (for reference - we'll discuss details later)

Now just to satisfy your curiosity Here's the code behind both of those examples and the previous slide.

The procedural code should be self-explanatory.

But I won't go into what's going on on the OOP code because that's going to be the topic of some upcoming lessons.

#### Procedural paradigm

```python
def increment(arg):
    arg = arg + 1
    return arg
```

The whole code:

```python
def increment(arg):
    arg = arg + 1
    return arg

this = 0
this = increment(this)
print(this)
this = increment(this)
print(this)
```

```
1
2
```


#### Object paradigm

```python
class MyCustomInt(object):
    def __init__(self):
        self.val = 0
    def increment(self):
        self.val = self.val + 1
    def __repr__(self):
        return str(self.val)
```

the whole code:

```python
class MyCustomInt(object):
    def __init__(self):
        self.val = 0
    def increment(self):
        self.val = self.val + 1
    def __repr__(self):
        return str(self.val)

this = MyCustomInt()
this.increment()
print(this)
this.increment()
print(this)
```
```
1
2
```

## OOP: Why?

- OOP organizes code so it is:
    - Easier to use
    - Easier to understand
    - Easier to maintain and extend
    - Easier to collaborate
- Complexity must always be managed
- OOP is a universal paradigm (many languages)
- Learning OOP is a necessary next step into the larger world of software engineering

Now it's going to take several lessons really for it to become clear to you exactly why we need object oriented programming.

> The short answer is that it just makes our lives easier.

And when we have very complex programs objects make it so much easier to handle the complexity.

Also to work with other developers on the same code and to communicate exactly what the library does to people who might use it.

for this reason Object Oriented Programming is a universal paradigm used in many languages and it's safe to say that learning object oriented programming is a necessary next step into the larger world of software engineering.

## OOP: Three Pillars

- Encapsulation
- Inheritance
- Plymorphism

Now a full description of objects wouldn't be complete without talking about the three pillars.

We're going to discuss each of these in upcoming lessons.

For now I'll just let you know what they are.

I also might mention that I had this as a question in an interview many years ago.

> What are the three pillars of object oriented programming?

I wouldn't be surprised if they're still using this question.

The answer is encapsulation inheritance and polymorphism does may not mean very much right now but we'll be discussing them much more extensively going forward.

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY0MjA4NTYzNl19
-->