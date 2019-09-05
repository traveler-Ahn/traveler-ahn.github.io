---
layout: post
title:  "2019/09/05 Tensorflow programming-Ch03"
subtitle: "2019/09/05 Tensorflow programming-Ch03"
categories: deeplearning
tags: tensorflow
comments: true
---

- 여러가지 자료를 활용한 Tensorflow Tutorials 
  - Ch2 Tensorboard

------

## Ch2 Tensorboard


```python
import tensorflow as tf
import numpy as np
```

### 1. Check point 저장하고 불러오는 방법 (at model folder)


```python
 data = np.loadtxt('data/data.csv', delimiter=',',
                  unpack=True, dtype='float32')

x_data = np.transpose(data[0:2])
y_data = np.transpose(data[2:])
```


```python
x_data.shape, y_data.shape
```


    ((6, 2), (6, 3))


```python
x_data
```


    array([[0., 0.],
           [1., 0.],
           [1., 1.],
           [0., 0.],
           [0., 0.],
           [0., 1.]], dtype=float32)


```python
y_data
```


    array([[1., 0., 0.],
           [0., 1., 0.],
           [0., 0., 1.],
           [1., 0., 0.],
           [1., 0., 0.],
           [0., 0., 1.]], dtype=float32)




```python
global_step = tf.Variable(0, trainable=False, name='global_step')

X = tf.placeholder(tf.float32)
Y = tf.placeholder(tf.float32)

W1 = tf.Variable(tf.random_uniform([2,10], -1.,1.))
L1 = tf.nn.relu(tf.matmul(X,W1))

W2 = tf.Variable(tf.random_uniform([10,20], -1.,1.))
L2 = tf.nn.relu(tf.matmul(L1,W2))

W3 = tf.Variable(tf.random_uniform([20,3], -1.,1.))
model = tf.matmul(L2,W3)

cost = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits_v2(labels=Y, logits=model))

optimizer = tf.train.AdamOptimizer(learning_rate=0.01)
train_op = optimizer.minimize(cost, global_step=global_step)
```


```python
sess = tf.Session()
saver = tf.train.Saver(tf.global_variables())

ckpt = tf.train.get_checkpoint_state('./model')
if ckpt and tf.train.checkpoint_exists(ckpt.model_checkpoint_path):
    saver.restore(sess, ckpt.model_checkpoint_path)
else:
    sess.run(tf.global_variables_initializer())
    
for step in range(2):
    sess.run(train_op, feed_dict={X: x_data, Y: y_data})
    
    print('Step: %d, ' % sess.run(global_step),
          'Cost: %.3f' % sess.run(cost, feed_dict={X: x_data, Y: y_data}))

saver.save(sess, './model/dnn.ckpt', global_step=global_step)
```

    Step: 1,  Cost: 1.276
    Step: 2,  Cost: 1.206

    './model/dnn.ckpt-2'


```python
prediction = tf.argmax(model, 1)
target = tf.argmax(Y, 1)
print('예측 값: ', sess.run(prediction, feed_dict={X: x_data}))
print('실제 값: ', sess.run(target, feed_dict={Y: y_data}))
```

    예측 값:  [0 0 1 0 0 1]
    실제 값:  [0 1 2 0 0 2]



```python
is_correct = tf.equal(prediction, target)
accuracy = tf.reduce_mean(tf.cast(is_correct, tf.float32))
print('정확도: %.2f' % sess.run(accuracy * 100, feed_dict={X: x_data, Y: y_data}))
```

    정확도: 50.00



```python
sess.close()
```

### 2. Tensorboard를 활용하기 위해 Variable의 값을 추적하는 과정


```python
data = np.loadtxt('data/data.csv', delimiter=',',
                  unpack=True, dtype='float32')

x_data = np.transpose(data[0:2])
y_data = np.transpose(data[2:])
```


```python
global_step = tf.Variable(0, trainable=False, name='global_step')

X = tf.placeholder(tf.float32)
Y = tf.placeholder(tf.float32)
```


```python
with tf.name_scope('layer1'):
    W1 = tf.Variable(tf.random_uniform([2,10], -1.,1.), name='W1')
    L1 = tf.nn.relu(tf.matmul(X,W1))
    
    tf.summary.histogram('weight_1', W1)

with tf.name_scope('layer2'):
    W2 = tf.Variable(tf.random_uniform([10,20], -1.,1.), name='W2')
    L2 = tf.nn.relu(tf.matmul(L1,W2))
    
    tf.summary.histogram('weight_2', W2)

with tf.name_scope('output'):
    W3 = tf.Variable(tf.random_uniform([20,3], -1.,1.))
    model = tf.matmul(L2,W3)
    
    tf.summary.histogram('weight_3', W3)

with tf.name_scope('optimizer'):
    cost = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits_v2(labels=Y, logits=model))

    optimizer = tf.train.AdamOptimizer(learning_rate=0.01)
    train_op = optimizer.minimize(cost, global_step=global_step)
    
    tf.summary.scalar('cost', cost)
```


```python
sess = tf.Session()
saver = tf.train.Saver(tf.global_variables())

ckpt = tf.train.get_checkpoint_state('./model')
if ckpt and not tf.train.checkpoint_exists(ckpt.model_checkpoint_path):
    #saver.restore(sess, ckpt.model_checkpoint_path)
    pass
else:
    sess.run(tf.global_variables_initializer())
    
merged = tf.summary.merge_all()
writer = tf.summary.FileWriter('./logs', sess.graph)
```


```python
for step in range(100):
    sess.run(train_op, feed_dict={X: x_data, Y: y_data})
    
    print('Step: %d, ' % sess.run(global_step),
          'Cost: %.3f' % sess.run(cost, feed_dict={X: x_data, Y: y_data}))
    
    summary = sess.run(merged, feed_dict={X: x_data, Y: y_data})
    writer.add_summary(summary, global_step=sess.run(global_step))

saver.save(sess, './model/dnn.ckpt', global_step=global_step)
```

    Step: 1,  Cost: 1.703
    Step: 2,  Cost: 1.590
    Step: 3,  Cost: 1.484
    
    ...
    
    Step: 96,  Cost: 0.550
    Step: 97,  Cost: 0.550
    Step: 98,  Cost: 0.550
    Step: 99,  Cost: 0.550
    Step: 100,  Cost: 0.550

    './model/dnn.ckpt-100'




```python
prediction = tf.argmax(model, 1)
target = tf.argmax(Y, 1)
print('예측 값: ', sess.run(prediction, feed_dict={X: x_data}))
print('실제 값: ', sess.run(target, feed_dict={Y: y_data}))
```

    예측 값:  [0 1 2 0 0 2]
    실제 값:  [0 1 2 0 0 2]



```python
is_correct = tf.equal(prediction, target)
accuracy = tf.reduce_mean(tf.cast(is_correct, tf.float32))
print('정확도: %.2f' % sess.run(accuracy * 100, feed_dict={X: x_data, Y: y_data}))
```

    정확도: 100.00



```python
sess.close()
```

 
```
# 해당 폴더 터미널에서 아래 키워드 입력 후 브라우저를 열어서 Tensorboard를 확인한다.
$ tensorboard --logdir=./logs

At browser: "localhost:6006"
```