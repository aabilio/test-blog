---
layout: post
title: "Algorithm 1"
tags: [Algorithms]
icon: /img_src/cats/algo.svg
toc: true
keywords: "chunker slide slicing rolling batches windows list sequence split imshow plot true false grid squares bernoulli distribution algorithm python"
notfull: true
---

{% assign img-url = '/img/post/algorithms' %}

This note contains questions/puzzle and algorithms to answer these problems. Most of the codes in this type of note are in [**Python**](/notes#python).

## Make chunkers / windows

Split a sequence into windows with size and slide.

~~~ python
def chunker(seq, size, slide=None, exact_size=False):
    if slide is None:
        slide = size
    if exact_size:
        return [seq[pos:pos + size] for pos in range(0, len(seq), slide) if len(seq[pos:pos + size]) == size]
    else:
        return [seq[pos:pos + size] for pos in range(0, len(seq), slide)]
~~~

::: code-output-flex
~~~ python
seq = [i for i in range(10)]

chunker(seq, 3)
chunker(seq, 3, exact_size=True)
chunker(seq, 3, slide=2)
~~~

~~~
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

[[0, 1, 2], [3, 4, 5], [6, 7, 8], [9]]
[[0, 1, 2], [3, 4, 5], [6, 7, 8]]
[[0, 1, 2], [2, 3, 4], [4, 5, 6], [6, 7, 8], [8, 9]]
~~~
:::

Make all arrays equal in size, filled with `np.nan`,

~~~ python
def chunker2(seq, size, slide=None):
    if slide is None:
        slide = size
    return [np.append( seq[pos:pos + size], np.repeat(np.nan, size-len(seq[pos:pos + size])) )
            for pos in range(0, len(seq), slide)]
~~~

::: code-output-flex
~~~ python
seq = [i for i in range(10)]

chunker2(seq, size=4, slide=2)
~~~

~~~
[array([0., 1., 2., 3.]),
 array([2., 3., 4., 5.]),
 array([4., 5., 6., 7.]),
 array([6., 7., 8., 9.]),
 array([ 8.,  9., nan, nan])]
~~~
:::

## Plot a grid of squares

Plot a square of `NxN` small other squares. Each one has a probability `Pxi/N` of being coloured, where `i` is the line where it stands.

<div class="col-2-equal">

~~~ python
N = 100
P = 0.5
im_size = 5

image = np.repeat(np.array(range(1,N+1)).reshape(N, 1), N, axis=1)

# LESS understandable but executing FASTER
image = (P/N * image) <= np.random.rand(N,N)

# MORE understandable but executing SLOWER
def bernoulli(num, P, N):
  return 1-np.random.binomial(1, P*num/N)
vfunc = np.vectorize(bernoulli)
image = vfunc(image, P, N)

plt.figure(figsize=(im_size, im_size))
plt.imshow(image, cmap='gray')
plt.show()
~~~
![Bernoulli squares]({{img-url}}/bernoulli-squares.png){:.img-full-90}
</div>