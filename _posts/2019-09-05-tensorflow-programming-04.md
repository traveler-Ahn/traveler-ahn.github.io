---
layout: post
title:  "2019/09/05 Tensorflow programming-Ch04"
subtitle: "2019/09/05 Tensorflow programming-Ch04"
categories: deeplearning
tags: tensorflow
comments: true
---

- 여러가지 자료를 활용한 Tensorflow Tutorials 
  - Ch3 MNIST (
    1. Softmax Regression
    2. Deep Neural Network
    3. Convolutional Neural Network

------

## Ch3 MNIST softmax regression

```python
import tensorflow as tf

from tensorflow.examples.tutorials.mnist import input_data
mnist = input_data.read_data_sets("./mnist/data", one_hot=True)
```



```python
X = tf.placeholder(tf.float32, [None, 784])
Y = tf.placeholder(tf.float32, [None, 10])

W = tf.Variable(tf.random_normal([784,10], stddev=0.01))
b = tf.Variable(tf.zeros(shape=[10]))

logits = tf.add(tf.matmul(X, W), b)
y_pred = tf.nn.softmax(logits)

# loss, optimizer
loss= tf.reduce_mean(-tf.reduce_sum(Y * tf.log(y_pred), reduction_indices=[1]))
#loss = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits_v2(logits=logits, labels=Y))
# tf.nn.softmax_cross_entropy_with_logits_v2 API를 이용한 구현
optimizer = tf.train.GradientDescentOptimizer(0.5).minimize(loss)
```

```python
sess = tf.Session()
sess.run(tf.global_variables_initializer())

batch_size = 100

for i in range(1000):
    batch_xs, batch_ys = mnist.train.next_batch(batch_size)
    sess.run(optimizer, feed_dict={X: batch_xs, Y: batch_ys})
```

```python
is_correct = tf.equal(tf.argmax(y_pred, 1), tf.argmax(Y, 1))
accuracy = tf.reduce_mean(tf.cast(is_correct, tf.float32))
print('정확도: ', sess.run(accuracy, feed_dict={X: mnist.test.images, Y: mnist.test.labels}))

sess.close()
```

```
정확도:  0.9205
```



---

## Ch3 MNIST_DNN

```python
import tensorflow as tf

from tensorflow.examples.tutorials.mnist import input_data
mnist = input_data.read_data_sets("./mnist/data", one_hot=True)
```



```python
global_step = tf.Variable(0, trainable=False, name='global_step')

X = tf.placeholder(tf.float32, [None, 784])
Y = tf.placeholder(tf.float32, [None, 10])
```

```python
with tf.name_scope('layer1'):
    W1 = tf.Variable(tf.random_normal([784,256], stddev=0.01), name='W1')
    L1 = tf.nn.relu(tf.matmul(X,W1))
    
    tf.summary.histogram('weight_1', W1)
    
with tf.name_scope('layer2'):
    W2 = tf.Variable(tf.random_normal([256,256], stddev=0.01), name='W2')
    L2 = tf.nn.relu(tf.matmul(L1,W2))
    
    tf.summary.histogram('weight_2', W2)
    
with tf.name_scope('layer3'):
    W3 = tf.Variable(tf.random_normal([256,10], stddev=0.01), name='W3')
    model = tf.matmul(L2,W3)
    
    tf.summary.histogram('weight_3', W3)
    
with tf.name_scope('optimizer'):
    cost = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits_v2(labels=Y, logits=model))
    optimizer = tf.train.AdamOptimizer(learning_rate=0.001).minimize(cost, global_step=global_step)
    
    tf.summary.scalar('cost', cost)
```

```python
config = tf.ConfigProto()
config.gpu_options.allow_growth=True
sess = tf.Session(config=config)
saver = tf.train.Saver(tf.global_variables())

ckpt = tf.train.get_checkpoint_state('./model')
if ckpt and tf.train.checkpoint_exists(ckpt.model_checkpoint_path):
    saver.restore(sess, ckpt.model_checkpoint_path)
else:
    sess.run(tf.global_variables_initializer())
    
merged = tf.summary.merge_all()
writer = tf.summary.FileWriter('./logs', sess.graph)
```



```python
batch_size = 100
total_batch = int(mnist.train.num_examples / batch_size)
```

```python
for epoch in range(10):
    total_cost = 0
    
    for i in range(total_batch):
        batch_xs, batch_ys = mnist.train.next_batch(batch_size)
        
        _, cost_val = sess.run([optimizer, cost], feed_dict={X: batch_xs, Y: batch_ys})
        total_cost += cost_val
        summary = sess.run(merged, feed_dict={X: batch_xs, Y: batch_ys})
        writer.add_summary(summary, global_step=sess.run(global_step))
        
    print('Epoch: %04d' %(epoch+1),
          'Avg. cost: %.3f' % float(total_cost/total_batch))
    
saver.save(sess, './model/mnist_dnn.ckpt', global_step=global_step)
print("Done")
```

```
Epoch: 0001 Avg. cost: 0.397
...
Epoch: 0010 Avg. cost: 0.017
Done
```



```python
is_correct = tf.equal(tf.argmax(model, 1), tf.argmax(Y, 1))
accuracy = tf.reduce_mean(tf.cast(is_correct, tf.float32))
print('정확도: ', sess.run(accuracy, feed_dict={X: mnist.test.images, Y: mnist.test.labels}))

sess.close()
```

```
정확도:  0.9767
```

### 2. Dropout

```python
global_step = tf.Variable(0, trainable=False, name='global_step')

X = tf.placeholder(tf.float32, [None, 784])
Y = tf.placeholder(tf.float32, [None, 10])
keep_prob = tf.placeholder(tf.float32)
```

```python
with tf.name_scope('layer1'):
    W1 = tf.Variable(tf.random_normal([784,256], stddev=0.01), name='W1')
    L1 = tf.nn.relu(tf.matmul(X,W1))
    L1 = tf.nn.dropout(L1, keep_prob)
    
with tf.name_scope('layer2'):
    W2 = tf.Variable(tf.random_normal([256,256], stddev=0.01), name='W2')
    L2 = tf.nn.relu(tf.matmul(L1,W2))
    L2 = tf.nn.dropout(L2, keep_prob)
    
with tf.name_scope('layer3'):
    W3 = tf.Variable(tf.random_normal([256,10], stddev=0.01), name='W3')
    model = tf.matmul(L2,W3)
    
with tf.name_scope('optimizer'):
    cost = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits_v2(labels=Y, logits=model))
    optimizer = tf.train.AdamOptimizer(learning_rate=0.001).minimize(cost, global_step=global_step)
```



```python
config = tf.ConfigProto()
config.gpu_options.allow_growth=True
sess = tf.Session(config=config)
saver = tf.train.Saver(tf.global_variables())

ckpt = tf.train.get_checkpoint_state('./model_dropout')
if ckpt and tf.train.checkpoint_exists(ckpt.model_checkpoint_path):
    saver.restore(sess, ckpt.model_checkpoint_path)
else:
    sess.run(tf.global_variables_initializer())
```

```python
batch_size = 100
total_batch = int(mnist.train.num_examples / batch_size)
```

```python
for epoch in range(10):
    total_cost = 0
    
    for i in range(total_batch):
        batch_xs, batch_ys = mnist.train.next_batch(batch_size)
        
        _, cost_val = sess.run([optimizer, cost], feed_dict={X: batch_xs, Y: batch_ys, keep_prob: 0.8})
        total_cost += cost_val
        
    print('Epoch: %04d' %(epoch+1),
          'Avg. cost: %.3f' % float(total_cost/total_batch))
    
saver.save(sess, './model_dropout/mnist_dnn.ckpt', global_step=global_step)
print("Done")
```

```
Epoch: 0001 Avg. cost: 0.425
...
Epoch: 0010 Avg. cost: 0.037
Done
```



```python
is_correct = tf.equal(tf.argmax(model, 1), tf.argmax(Y, 1))
accuracy = tf.reduce_mean(tf.cast(is_correct, tf.float32))
print('정확도: ', sess.run(accuracy, feed_dict={X: mnist.test.images, Y: mnist.test.labels, keep_prob: 1.}))

sess.close()
```

```
정확도:  0.9795
```



---

## Ch3 MNIST CNN

### 1. Low level API 사용


```python
import tensorflow as tf

from tensorflow.examples.tutorials.mnist import input_data
mnist = input_data.read_data_sets("./mnist/data/", one_hot=True)
```



```python
X = tf.placeholder(tf.float32, [None, 28, 28, 1])
Y = tf.placeholder(tf.float32, [None, 10])
keep_prob = tf.placeholder(tf.float32)
```


```python
W1 = tf.Variable(tf.random_normal([3,3,1,32], stddev=0.01))
L1 = tf.nn.conv2d(X, W1, strides=[1,1,1,1], padding='SAME')
L1 = tf.nn.relu(L1)
L1 = tf.nn.max_pool(L1, ksize=[1,2,2,1], strides=[1,2,2,1], padding='SAME')

W2 = tf.Variable(tf.random_normal([3,3,32,64], stddev=0.01))
L2 = tf.nn.conv2d(L1, W2, strides=[1,1,1,1], padding='SAME')
L2 = tf.nn.relu(L2)
L2 = tf.nn.max_pool(L2, ksize=[1,2,2,1], strides=[1,2,2,1], padding='SAME')

W3 = tf.Variable(tf.random_normal([7*7*64, 256], stddev=0.01))
L3 = tf.reshape(L2, [-1, 7*7*64])
L3 = tf.matmul(L3, W3)
L3 = tf.nn.relu(L3)
L3 = tf.nn.dropout(L3, keep_prob)

W4 = tf.Variable(tf.random_normal([256, 10], stddev=0.01))
model = tf.matmul(L3, W4)

cost = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits_v2(logits=model, labels=Y))
optimizer = tf.train.AdamOptimizer(0.001).minimize(cost)
```



```python
config = tf.ConfigProto()
config.gpu_options.allow_growth=True
sess = tf.Session(config=config)
sess.run(tf.global_variables_initializer())
```


```python
batch_size = 100
total_batch = int(mnist.train.num_examples / batch_size)
```


```python
for epoch in range(10):
    total_cost = 0
    
    for i in range(total_batch):
        batch_xs, batch_ys = mnist.train.next_batch(batch_size)
        batch_xs = batch_xs.reshape(-1, 28, 28, 1)
        
        _, cost_val = sess.run([optimizer, cost], feed_dict={X: batch_xs, 
                                                             Y: batch_ys,
                                                             keep_prob: 0.7})
        
        total_cost += cost_val
    print('Epoch: %04d' %(epoch+1),
          'Avg. cost: %.3f' % float(total_cost/total_batch))
    
print("Done")
```

    Epoch: 0001 Avg. cost: 0.352
    Epoch: 0002 Avg. cost: 0.110
    
    ...
    
    Epoch: 0009 Avg. cost: 0.028
    Epoch: 0010 Avg. cost: 0.027
    Done



```python
is_correct = tf.equal(tf.argmax(model, 1), tf.argmax(Y, 1))
accuracy = tf.reduce_mean(tf.cast(is_correct, tf.float32))
print('정확도: ', sess.run(accuracy, feed_dict={X: mnist.test.images.reshape(-1, 28, 28, 1), Y: mnist.test.labels, keep_prob: 1.}))

sess.close()
```

    정확도:  0.9901


### 2. High level API 사용
- tf.keras.layer 사용해서 추가 필요
- Tensorflow에서 Keras layer 사용하는 방법


```python
X = tf.placeholder(tf.float32, [None, 28, 28, 1])
Y = tf.placeholder(tf.float32, [None, 10])
is_training = tf.placeholder(tf.bool)
```


```python
L1 = tf.layers.conv2d(X, 32, [3,3])
L1 = tf.layers.max_pooling2d(L1, [2,2], [2,2])
L1 = tf.layers.dropout(L1, 0.7, is_training)

L2 = tf.layers.conv2d(L1, 64, [3,3])
L2 = tf.layers.max_pooling2d(L2, [2,2], [2,2])
L2 = tf.layers.dropout(L2, 0.7, is_training)

L3 = tf.contrib.layers.flatten(L2)
L3 = tf.layers.dense(L3, 256, activation=tf.nn.relu)
L3 = tf.layers.dropout(L3, 0.5, is_training)

model = tf.layers.dense(L3, 10, activation=None)
```



```python
cost = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits_v2(logits=model, labels=Y))
optimizer = tf.train.AdamOptimizer(0.001).minimize(cost)
```


```python
config = tf.ConfigProto()
config.gpu_options.allow_growth=True
sess = tf.Session(config=config)
sess.run(tf.global_variables_initializer())
```


```python
batch_size = 100
total_batch = int(mnist.train.num_examples / batch_size)
```


```python
for epoch in range(10):
    total_cost = 0
    
    for i in range(total_batch):
        batch_xs, batch_ys = mnist.train.next_batch(batch_size)
        batch_xs = batch_xs.reshape(-1, 28, 28, 1)
        
        _, cost_val = sess.run([optimizer, cost], feed_dict={X: batch_xs, 
                                                             Y: batch_ys,
                                                             is_training:True})
        
        total_cost += cost_val
    print('Epoch: %04d' %(epoch+1),
          'Avg. cost: %.3f' % float(total_cost/total_batch))
    
print("Done")
```

    Epoch: 0001 Avg. cost: 0.006
    
    ...
    
    Epoch: 0010 Avg. cost: 0.005
    Done



```python
is_correct = tf.equal(tf.argmax(model, 1), tf.argmax(Y, 1))
accuracy = tf.reduce_mean(tf.cast(is_correct, tf.float32))
print('정확도: ', sess.run(accuracy, feed_dict={X: mnist.test.images.reshape(-1, 28, 28, 1), 
                                              Y: mnist.test.labels, 
                                              is_training: False}))

sess.close()
```

    정확도:  0.9893

