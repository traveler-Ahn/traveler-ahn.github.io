---
layout: post
title:  "2019/09/05 Tensorflow programming-Ch01"
subtitle: "2019/09/05 Tensorflow programming-Ch01"
categories: deeplearning
tags: tensorflow
comments: true

---

- 여러가지 자료를 활용한 Tensorflow Tutorials 
  - Ch0 기본적인 Tensor 연산

---

## Ch0 기본적인 Tensor 연산

### 1) constant


```python
import tensorflow as tf
```


```python
hello = tf.constant('Hello, Tensorflow!')
print(hello)
```

    Tensor("Const:0", shape=(), dtype=string)



```python
a = tf.constant(10)
b = tf.constant(32)
c = tf.add(a, b)
print(c)
```

    Tensor("Add:0", shape=(), dtype=int32)



```python
sess = tf.Session()
sess
```




    <tensorflow.python.client.session.Session at 0x7f65997535f8>




```python
print(sess.run(hello))
print(sess.run(c))
```

    b'Hello, Tensorflow!'
    42



```python
sess.close()
```

### 2) placeholder, 3) Variable


```python
# placeholder
X = tf.placeholder(tf.float32, [None, 3])
print(X)
```

    Tensor("Placeholder:0", shape=(?, 3), dtype=float32)



```python
x_data = [[1,2,3], [4,5,6]]

# Variable
W = tf.Variable(tf.random_normal([3,2]))
b = tf.Variable(tf.random_normal([2,1]))

expr = tf.matmul(X, W) + b
```


```python
sess = tf.Session()
sess.run(tf.global_variables_initializer())
```


```python
print(x_data)
print(sess.run(W))
print(sess.run(b))
print("==============")
print(sess.run(expr, feed_dict={X: x_data}))
```

    [[1, 2, 3], [4, 5, 6]]
    [[ 0.75671136 -0.5083588 ]
     [-1.7855581  -0.08332505]
     [ 0.8447792   0.68591684]]
    [[-0.04964273]
     [-1.0905735 ]]
    ==============
    [[-0.3297102  1.3330989]
     [-1.9228437  0.574867 ]]



```python
sess.close()
```

### 4) placeholder와 Variable의 종합적인 사용


```python
import tensorflow as tf
```


```python
x_train = [1, 2, 3, 4]
y_train = [2, 4, 6, 8]
```


```python
W = tf.Variable(tf.random_normal(shape=[1]))
b = tf.Variable(tf.random_normal(shape=[1]))

x = tf.placeholder(tf.float32)
y = tf.placeholder(tf.float32)

linear_model = W*x + b

# 손실함수
loss = tf.reduce_mean(tf.square(linear_model - y))

# Optimizer
optimizer = tf.train.GradientDescentOptimizer(0.01).minimize(loss)
```


```python
sess = tf.Session()
sess.run(tf.global_variables_initializer())

total_cost = 0

for i in range(1000):
    _, cost =sess.run([optimizer, loss], feed_dict={x: x_train, y: y_train})
    total_cost += cost
    
    if i % 100 == 0:
        print("{} 번째 Cost : {}".format(i, total_cost/1000))
        total_cost = 0
```

    0 번째 Cost : 0.06275773620605468
    100 번째 Cost : 0.23862323957681655
    200 번째 Cost : 0.05455601394176483
    300 번째 Cost : 0.029950608119368553
    400 번째 Cost : 0.016442522786557674
    500 번째 Cost : 0.00902674874663353
    600 번째 Cost : 0.0049555815868079665
    700 번째 Cost : 0.002720555143430829
    800 번째 Cost : 0.001493550975807011
    900 번째 Cost : 0.0008199408235959708



```python
x_test = [3.5, 5, 5.5, 6]

print(sess.run(linear_model, feed_dict={x: x_test}))
```

    [ 6.9732504  9.901583  10.877694  11.853805 ]

