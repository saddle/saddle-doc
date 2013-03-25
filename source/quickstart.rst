Quick Start Guide
~~~~~~~~~~~~~~~~~

Let's take a quick tour through Saddle to get a sense of the feature set. There are four
major data structures to be aware of:

- Vec: a 1d vector object
- Series: a 1d indexed vector object
- Mat: a 2d matrix object
- Frame: a 2d indexed matrix object

Let's look at each one in turn through examples. If you've got the source code and an SBT
launcher, run the following (from the directory where you've got Saddle checked out):

.. code:: bash

  $ sbt console

If you've only got the Saddle jar in your classpath, the relevant import is:

.. code:: scala

  import org.saddle._

Vec
---

Let's take a look at a few examples through an example console session.

.. code:: scala

  scala> Vec(1,2,3)
  res0: org.saddle.Vec[Int] = 
  [3 x 1]
  1
  2
  3

  scala> Vec(4,5,6)
  res1: org.saddle.Vec[Int] = 
  [3 x 1]
  4
  5
  6
  
  scala> res0 + res1
  res2: org.saddle.Vec[Int] = 
  [3 x 1]
  5
  7
  9
  
  scala> res0 * res1
  res3: org.saddle.Vec[Int] = 
  [3 x 1]
   4
  10
  18
  
  
  scala> res0 dot res1
  res4: Int = 32
  
  scala> res0 outer res1
  res5: org.saddle.Mat[Int] = 
  [3 x 3]
   4  5  6 
   8 10 12 
  12 15 18 
  
  
  scala> res0 ** res1
  res6: org.saddle.Vec[Int] = 
  [3 x 1]
    1
   32
  729
  
  
  scala> res0 << 2
  res7: org.saddle.Vec[Int] = 
  [3 x 1]
   4
   8
  12
  
  
  scala> res0 & 0x1
  res8: org.saddle.Vec[Int] = 
  [3 x 1]
  1
  0
  1
  
  
  scala> res0.filter(_ > 5)
  res9: org.saddle.Vec[Int] = Empty Vec
  
  scala> res0.filter(_ > 2)
  res10: org.saddle.Vec[Int] = 
  [1 x 1]
  3
  
  
  scala> res0.sum
  res11: Int = 6
  
  scala> res0.mean
  res12: Double = 2.0
  
  scala> res0.median
  res13: Double = 2.0
  
  scala> res0.max
  res14: Option[Int] = Some(3)
  
  scala> res0.stdev
  res15: Double = 1.0


Let's look at a few ways to create Vec instances:

.. code:: bash

  scala> Vec(1,2,3) // pass a sequence directly
  res0: org.saddle.Vec[Int] = 
  [3 x 1]
  1
  2
  3
  
  
  scala> Vec(1 to 3 : _*) // pass a sequence indirectly
  res1: org.saddle.Vec[Int] = 
  [3 x 1]
  1
  2
  3
  
  
  scala> Vec(Array(1,2,3)) // wrap an array
  res2: org.saddle.Vec[Int] = 
  [3 x 1]
  1
  2
  3

  scala> Vec(Vec(1,2,3)) // don't forget to unpack!
  res3: org.saddle.Vec[org.saddle.Vec[Int]] = 
  [1 x 1]
  [3 x 1]
  1
  2
  3
  
  
  scala> Vec(Vec(1,2,3).toSeq : _*) // this is what we usually want!
  res4: org.saddle.Vec[Int] = 
  [3 x 1]
  1
  2
  3
  
Sometimes random Vec instances are useful. There are a few ways to accomplish 
this:
  
.. code::

  scala> vec.rand(1000) // a thousand random doubles from -1.0 to 1.0 (excluding 0)
  res16: org.saddle.Vec[Double] = 
  [1000 x 1]
  -0.3647
  -0.8776
  -0.1852
   0.4713
   0.5310
   ... 
  -0.1232
  -0.3302
   0.6612
   0.1838
  -0.5100
  
  
  scala> vec.randp(1000) // a thousand random positive doubles
  res17: org.saddle.Vec[Double] = 
  [1000 x 1]
  0.4377
  0.2627
  0.7381
  0.5137
  0.1575
   ... 
  0.6006
  0.6870
  0.9352
  0.8327
  0.9287
  
  
  scala> vec.randi(1000) // a thousand random ints
  res18: org.saddle.Vec[Int] = 
  [1000 x 1]
   1486232052
     79709566
   1053064649
    -33727419
   1788415839
   ... 
   -690368198
  -1546745697
   2110715984
   1291536312
   2041370436
  
  
  scala> vec.randpi(1000) % 10 // a thousand random ints from 1 to 9
  res19: org.saddle.Vec[Int] = 
  [1000 x 1]
  7
  7
  2
  7
  3
   ... 
  1
  7
  2
  6
  4


