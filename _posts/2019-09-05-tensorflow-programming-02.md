---
layout: post
title:  "2019/09/05 Tensorflow programming-Ch02"
subtitle: "2019/09/05 Tensorflow programming-Ch02"
categories: deeplearning
tags: tensorflow
comments: true
---

- 여러가지 자료를 활용한 Tensorflow Tutorials 
  - Ch1 Multi layer perceptron

------

## Ch1 Multi layer perceptron


```python
import tensorflow as tf
import numpy as np
```

### Ex.1


```python
x_data = [1,2,3]
y_data = [1,2,3]

# Placeholder
X = tf.placeholder(tf.float32, name="X")
Y = tf.placeholder(tf.float32, name="Y")

# Variable
W = tf.Variable(tf.random_uniform([1], -1.0, 1.0))
b = tf.Variable(tf.random_uniform([1], -1.0, 1.0))

# Hypothesis
hypothesis = W * X + b

# Cost (RMS) & optimizer
cost = tf.reduce_mean(tf.square(hypothesis - Y))
optimizer = tf.train.GradientDescentOptimizer(learning_rate=0.1)
train_op = optimizer.minimize(cost)
```


```python
# Training Phase
#with tf.Session() as sess:
sess = tf.Session()
sess.run(tf.global_variables_initializer())

for step in range(100):
    _, cost_val = sess.run([train_op, cost], feed_dict={X: x_data, Y: y_data})

    print(step, cost_val, sess.run(W), sess.run(b))
```

    0 0.48942924 [0.67671835] [0.66008174]
    1 0.06985671 [0.71441513] [0.657378]
    2 0.06180435 [0.71800977] [0.64013636]
    3 0.05881207 [0.7251461] [0.62490517]
    
    ...
    
    94 0.00070168846 [0.9699738] [0.06825662]
    95 0.0006683576 [0.9706956] [0.06661578]
    96 0.00063660915 [0.9714] [0.06501435]
    97 0.0006063708 [0.97208756] [0.06345148]
    98 0.00057756744 [0.9727586] [0.06192616]
    99 0.0005501336 [0.9734134] [0.06043748]



```python
# Test
print("X: 5, Y: ", sess.run(hypothesis, feed_dict={X: 5}))
print("X: 2.5, Y: ", sess.run(hypothesis, feed_dict={X: 2.5}))
    
sess.close()
```

    X: 5, Y:  [4.9275045]
    X: 2.5, Y:  [2.4939709]


### Ex.2 Softmax regression


```python
# Data preparation

x_data = np.array([
    [0,0], [1,0], [1,1], [0,0], [0,0], [0,1]
])
y_data = np.array([
    [1,0,0],
    [0,1,0],
    [0,0,1],
    [1,0,0],
    [1,0,0],
    [0,0,1],
])
```


```python
# Placeholder 
X = tf.placeholder(tf.float32, [None, 2])
Y = tf.placeholder(tf.float32, [None, 3])

# Variable
W = tf.Variable(tf.random_uniform([2,3], -1., 1.))
b = tf.Variable(tf.zeros([3]))

# Loss
L = tf.add(tf.matmul(X,W), b)
L = tf.nn.relu(L)

# Cost
model = tf.nn.softmax(L)
cost = tf.reduce_mean(-tf.reduce_sum(Y*tf.log(model), axis=1))

# Optimizer
optimizer = tf.train.GradientDescentOptimizer(learning_rate=0.01)
train_op = optimizer.minimize(cost)
```


```python
# Training phase
sess = tf.Session()
sess.run(tf.global_variables_initializer())

for step in range(100):
    sess.run(train_op, feed_dict={X: x_data, Y: y_data})
    
    if (step + 1) % 10 == 0:
        print(step+1, sess.run(cost, feed_dict={X: x_data, Y: y_data}))       
```

    10 1.1477284
    20 1.1427294
    30 1.1379366
    40 1.1332898
    50 1.1288582
    60 1.1245589
    70 1.1204705
    80 1.1165211
    90 1.1127042
    100 1.1090314



```python
prediction = tf.argmax(model, axis=1)
target = tf.argmax(Y, axis=1)
print('예측 값: ', sess.run(prediction, feed_dict={X: x_data}))
print('실제 값: ', sess.run(target, feed_dict={Y: y_data}))
```

    예측 값:  [0 2 2 0 0 0]
    실제 값:  [0 1 2 0 0 2]



```python
is_correct = tf.equal(prediction, target)
accuracy = tf.reduce_mean(tf.cast(is_correct, tf.float32))
print('정확도: %.2f' % sess.run(accuracy * 100, feed_dict={X: x_data, Y: y_data}))
```

    정확도: 66.67



```python
sess.close()
```

### Ex.3 Deep Neural Network


```python
# Data preparation

x_data = np.array([
    [0,0], [1,0], [1,1], [0,0], [0,0], [0,1]
])
y_data = np.array([
    [1,0,0],
    [0,1,0],
    [0,0,1],
    [1,0,0],
    [1,0,0],
    [0,0,1],
])
```


```python
# Placeholder 
X = tf.placeholder(tf.float32, [None, 2])
Y = tf.placeholder(tf.float32, [None, 3])

# Variable
W1 = tf.Variable(tf.random_uniform([2,10], -1., 1.))
b1 = tf.Variable(tf.zeros([10]))

W2 = tf.Variable(tf.random_uniform([10,3], -1., 1.))
b2 = tf.Variable(tf.zeros([3]))

# Loss
L1 = tf.add(tf.matmul(X,W1), b1)
L1 = tf.nn.relu(L1)

# Cost
logits = tf.add(tf.matmul(L1,W2), b2)
cost = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits_v2(labels=Y, logits=logits))

# Optimizer
optimizer = tf.train.GradientDescentOptimizer(learning_rate=0.01)
train_op = optimizer.minimize(cost)
```


```python
# Training phase
sess = tf.Session()
sess.run(tf.global_variables_initializer())

for step in range(100):
    sess.run(train_op, feed_dict={X: x_data, Y: y_data})
    
    if (step + 1) % 10 == 0:
        print(step+1, sess.run(cost, feed_dict={X: x_data, Y: y_data}))    
```

    10 1.2115687
    20 1.1780648
    30 1.1487331
    40 1.1211877
    50 1.0950718
    60 1.0701938
    70 1.0464278
    80 1.0248119
    90 1.0060588
    100 0.987839



```python
prediction = tf.argmax(logits, axis=1)
target = tf.argmax(Y, axis=1)
print('예측 값: ', sess.run(prediction, feed_dict={X: x_data}))
print('실제 값: ', sess.run(target, feed_dict={Y: y_data}))
```

    예측 값:  [0 2 2 0 0 2]
    실제 값:  [0 1 2 0 0 2]



```python
is_correct = tf.equal(prediction, target)
accuracy = tf.reduce_mean(tf.cast(is_correct, tf.float32))
print('정확도: %.2f' % sess.run(accuracy * 100, feed_dict={X: x_data, Y: y_data}))
```

    정확도: 83.33

```python
sess.close()
```
