---
layout: post
title: Map and FlatMap
date: '2016-03-30T07:17:00.003-05:00'
author: Anthony Garo
tags:
- scala
- Code
---

Hey guys I'm back. I've been real lazy about moving my blog over here but it's finally done

Today I'm going to talk about map and flatmap.
For some reason, it took me a while to understand these functions so I wanted to share them with you.

The following code examples are in scala and can easily be executed from the scala REPL.

For those of you new to scala or a REPL(read, evaluate, print, loop), here's how you set it up:

download [Scala](http://www.scala-lang.org/download/) and install it.
Once installed, just simply go to your terminal and type `scala`

you will be welcomed by the following:

```bash
~ > scala
Welcome to Scala 2.11.8 (Java HotSpot(TM) 64-Bit Server VM, Java 1.8.0_60).
Type in expressions for evaluation. Or try :help.

scala>
```

For those of you who don't know Functional Programming or are starting to use it now, you're in for a treat :-)

Map and FlatMap usually come bundled with Monads.
Monads are specific to functional programming. A Monad is not a type but more of a construct.
Many different objects in scala are Monads out of the box because they follow the Monad laws.
Lists, Options, and Futures are great examples of Monads in Scala. To put it simply, a Monad is a container with some stuff in it.
The Monad gives you the ability to perform operations on the stuff while it's in the container. Once you're done  operating on your stuff, you can unwrap the Monad and get your result. Whether it succeeded or not.


Let's get right into it.

###Map
Goes through every item in your container and performs the specified operation on it.

####List

```scala
scala> val list = List(1,2,3,4,5,6,7,8,9,10)
list: List[Int] = List(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
 
scala> list.map(num => num * 2)
res0: List[Int] = List(2, 4, 6, 8, 10, 12, 14, 16, 18, 20)
```

For those of you new to lambda expressions let me clarify some stuff:
`list.map(num => num * 2)`
We're iterating over every value in our list. `num` is a reference to the current value the map function will be looking at.
At the end, the map function produces a NEW list with the new values. FYI `val` signifies an IMMUTABLE value in scala so our original list does not change. If you want to retain this value, you need to assign a new `val` to it.

```scala
scala> val list = List(1,2,3,4,5,6,7,8,9,10)
list: List[Int] = List(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
 
scala> list.map(num => num * 2)
res0: List[Int] = List(2, 4, 6, 8, 10, 12, 14, 16, 18, 20)
 
scala> list
res1: List[Int] = List(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
 
scala> val list2 = list.map(num => num * 2)
list2: List[Int] = List(2, 4, 6, 8, 10, 12, 14, 16, 18, 20)
 
scala> list2
res2: List[Int] = List(2, 4, 6, 8, 10, 12, 14, 16, 18, 20)
```


```scala
scala> list.map(num => println(s"current number = $num"))
current number = 1
current number = 2
current number = 3
current number = 4
current number = 5
current number = 6
current number = 7
current number = 8
current number = 9
current number = 10
res11: List[Unit] = List((), (), (), (), (), (), (), (), (), ()) 
//println statements return void(nothing) so you get back a list of nothing...notice Unit :-)
//Unit is basically saying this returns nothing and is a valid return type. 
//You typically would not use void like in other languages
```

####Option Example
I'm not going to go into it too much but an Option in scala is exactly that. You either have something or you don't.
This solves the issue of NullPointerExceptions in Java. At the end of operating on an Option, you either have `Some` or `None`
Let's take a look at some code:

```scala
scala> val option = Option(10)
option: Option[Int] = Some(10) //notice the Some
 
scala> option.map(num => num * 2)
res3: Option[Int] = Some(20) //notice the Some again
```

As you've noticed, we used the EXACT same map function over the Option.
You can picture an Option of just simply a list of 1 item. Only difference it's either there or not.

Let's see what happens when it is not there or we perform a bad operation on it.

```scala
scala> val none: Option[Int] = None
none: Option[Int] = None
 
scala> none.map(num => num * 2)
res0: Option[Int] = None
```

Some things to note about the code above.

`val none: Option[Int]` here we are specifying that the variable none will be of type Option[Int] 

We then set it to None to signify there is nothing there. As you can see when we tried to multiply nothing * 2, the compiler did not freak out but simply returned None to us to show there is nothing there
This is just for simply giving an example but if this were a database retrieval, json/xml being converted into an object, then it could get ugly if an Option were not used here.

###FlatMap
Let's look at flatMap now. FlatMap is a combination of map and another function called flatten. It works just like map but it calls the flatten function for you. It's better if I showed you.


####List
```scala
scala> val list = List(1,2,3)
list: List[Int] = List(1, 2, 3)
 
scala> list.map(num => List(num-1,num,num+1))
res0: List[List[Int]] = List(List(0, 1, 2), List(1, 2, 3), List(2, 3, 4))
 
scala> list.map(num => List(num-1,num,num+1)).flatten
res1: List[Int] = List(0, 1, 2, 1, 2, 3, 2, 3, 4)
 
scala> list.flatMap(num => List(num-1,num,num+1))
res2: List[Int] = List(0, 1, 2, 1, 2, 3, 2, 3, 4)
```

The example above starts off with `val list = List(1,2,3)`

Then it goes on to map over it and produce a list for every number in the original list. Each mini list contains the number and it's left and right neighbors.

If for some reason you wanted to take all these lists and convert them into one giant list again then you would call flatten as you can see.

The flatMap takes that complexity away and does it for you in one shot.

We went from `List[Int]` to `List[List[Int]]` and back to `List[Int]`

####Option
```scala
scala> val option = Option(10)
option: Option[Int] = Some(10)
 
scala> option.map(num => Option(num * 2))
res3: Option[Option[Int]] = Some(Some(20))
 
scala> option.map(num => Option(num * 2)).flatten
res4: Option[Int] = Some(20)
 
scala> option.flatMap(num => Option(num * 2))
res5: Option[Int] = Some(20)
```

As you can see with the Option, it is the exact same thing.

Going from `Option[Int]` to `Option[Option[Int]]` and back to `Option[Int]`

You're probably asking when would you ever see something like this. I'll demonstrate with a more realistic example.

Let's imagine a structure where you have a client management system. That customer may or may not have an address. The address may or may not have a zip code depending on which country you're in(some international countries don't require zip codes in addresses).

Before we begin the example, some basic info about the code we are going to use.

####The case class
the case class is the equivalent of a plain old object with fields in it. No functions or behavior/state changing things should be here. The term case class is a scala thing but the concept is natural to other languages. Some of us call them POJOs(plain old java objects) or DTOs(Data Transfer Object)

The cool thing about case classes in scala is that they automatically come with an equals method and toString method. Another cool thing is you don't have to use the keyword `new` to create a new object from a case class or create getters/setters because they're made for you

#####Defining our stuff
```scala
scala> case class Address(add1: String, add2: String, postalCode: Option[String])
defined class Address
 
scala> case class Client(name: String, add: Option[Address])
defined class Client
```

#####Creating clients
We'll create 3 clients. One with an address with a postal code and one with an address without a postal code. And a third with no address.

```scala
//Address
scala> val addWithPostal = Address("address1","address2", Some("postalCode"))
addWithPostal: Address = Address(address1,address2,Some(postalCode))
 
scala> val addWithNoPostal = Address("address1","address2",None)
addWithNoPostal: Address = Address(address1,address2,None)
 
//Clients
scala> val clientWithNoAdd = Client("client1",None)
clientWithNoAdd: Client = Client(client1,None) 
 
scala> val clientWithNoPostal = Client("client2", Some(addWithNoPostal))
clientWithNoPostal: Client = Client(client2,Some(Address(address1,address2,None)))
 
scala> val clientWithPostal = Client("client3",Some(addWithPostal))
clientWithPostal: Client = Client(client3,Some(Address(address1,address2,Some(postalCode))))
```

Ok we're all set up. Now the fun part. I want to print out the postal code for all my clients

```scala
scala> clientWithNoPostal.add //this is an option so we need to map over it to get to it's value and operate
		.map(address => address.postalCode //postalCode is also an option
			.map(postal => println(postal)))
res7: Option[Option[Unit]] = Some(None)			
```

As you can see above that resulted in `Option[Option[Unit]] = Some(None)`
We're still not there yet. Let's flatten it.

```scala
scala> clientWithNoPostal.add.map(address => address.postalCode.map(postal => println(postal))).flatten
res8: Option[Unit] = None
```

And as you know, this can all be done from flatMap

```scala
scala> clientWithNoPostal.add.flatMap(address => address.postalCode.map(postal => println(postal)))
res9: Option[Unit] = None
```

As you can see, there was no need for null checks or Exceptions being thrown. The code simply handled everything.
But most importantly, this is a real scenario of when there are heirarchies that may have optional values in a chain

Let's look at the other examples for completion

```scala
scala> clientWithPostal.add.flatMap(address => address.postalCode.map(postal => println(postal)))
postalCode
res10: Option[Unit] = Some(()) //Again notice the empty Some(()) because println returns nothing
```

If you simply wanted to get the value, you can
See below:

```scala
scala> clientWithPostal.add.map(address => address.postalCode)
res14: Option[Option[String]] = Some(Some(postalCode))
 
scala> clientWithPostal.add.flatMap(address => address.postalCode)
res13: Option[String] = Some(postalCode)
 
scala> clientWithPostal.add.flatMap(address => address.postalCode).get//will throw an exception if no value is there
res16: String = postalCode

scala> clientWithPostal.add.flatMap(address => address.postalCode).getOrElse("noPostal")//avoid exception with default value
res15: String = postalCode
```

```scala
scala> clientWithNoAdd.add.flatMap(address => address.postalCode)
res17: Option[String] = None

scala> clientWithNoAdd.add.flatMap(address => address.postalCode.map(postal => println(postal)))
res18: Option[Unit] = None

scala> clientWithNoAdd.add.flatMap(address => address.postalCode).get
java.util.NoSuchElementException: None.get
  at scala.None$.get(Option.scala:347)
  at scala.None$.get(Option.scala:345)
  ... 32 elided
//throws exception because you're trying to get an element from Nothing  
```
As you can see from the above example, we tried to get to the postal code but this user has no address to begin with.

The container knows that there is no address, so it returns the result of that and does not go any further down the chain to retrieve the postal code

In the very last line, I tried to get something from Nothing so the compiler threw an exception

##Well that's all for today! See you again next time !!!