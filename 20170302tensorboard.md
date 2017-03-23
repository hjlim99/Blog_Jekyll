![](/assets/tensorboard.png)
1. 코드에 텐서보드용 로그 파일 저장 위치 지정
```
writer = tf.train.SummaryWriter("/tmp/test_logs", session.graph)
```

2. Tracking할 대상 지정 

# step 1: node 선택
add_hist = tf.scalar_summary("add_scalar", add)
mul_hist = tf.scalar_summary("mul_scalar", mul)

# step 2: summary 통합. 두 개의 코드 모두 동작.
merged = tf.merge_all_summaries()
# merged = tf.merge_summary([add_hist, mul_hist])


3. 학습 수행시 로그 파일 저장 ` writer.add_summary(summary, step)`


4. 실행 

```
tensorboard --logdir=/tmp/sample
# tensorboard --logdir=/tmp/sample --port=8008
```

# 주요 함수
## 1. tf.name_scope()
- name_scope 함수는 노드의 이름을 지정하고 노드의 큰 틀을 제공해줍니다. 
- 그 틀 안에서 실행되는 연산들은 텐서보드에서 노드를 클릭하면 연산의 흐름을 볼 수 있습니다.
- 블록 단위로 나누어서 표현 하고자 할때




###### 샘플코드 #1 : tensorboard에 점 하나 찍는 예제

```python
import tensorflow as tf

a = tf.constant(3.0)
b = tf.constant(5.0)
c = a * b

# tensorboard에 point라는 이름으로 표시됨
c_summary = tf.scalar_summary("point", c)
merged = tf.merge_all_summaries()

with tf.Session() as sess:
    writer = tf.train.SummaryWriter("./board/sample_1", sess.graph)

    result = sess.run([merged])
    tf.initialize_all_variables().run()

    writer.add_summary(result[0])
```

###### 샘플코드 #2 : 두 개의 직선을 출력하는 예제

```python
import tensorflow as tf

X = tf.placeholder(tf.float32)
Y = tf.placeholder(tf.float32)

add = tf.add(X, Y)
mul = tf.mul(X, Y)

# step 1: node 선택
add_hist = tf.scalar_summary("add_scalar", add)
mul_hist = tf.scalar_summary("mul_scalar", mul)

# step 2: summary 통합. 두 개의 코드 모두 동작.
merged = tf.merge_all_summaries()
# merged = tf.merge_summary([add_hist, mul_hist])

with tf.Session() as sess:
    init = tf.initialize_all_variables()
    sess.run(init)

    # step 3: writer 생성
    writer = tf.train.SummaryWriter("./board/sample_2", sess.graph)

    for step in range(100):
        # step 4: 노드 추가
        summary = sess.run(merged, feed_dict={X: step * 1.0, Y: 2.0})
        writer.add_summary(summary, step)

# step 5: 콘솔에서 명령 실행
# tensorboard --logdir=./board/sample_2
```

출처:[파이쿵](http://pythonkim.tistory.com/39)
