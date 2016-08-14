---
layout: post
title:  "What makes RNNs tick ??"
date:   2016-08-14 07:33:11 -0400
categories: jekyll update
---
Convolutional neural networks (CNNs), aka. dump and regress, are a formidable form of end to end gradient machines that are taking over rapidly in the various domains. 
Indeed, their boom has coincided with that of high end GPUs with rapid processing power.
 
However, in their vanilla form, they stand unable to handle sequence data. These data form the next major barrier in various problem spaces and need to be handled effectively for CNNs to take the next great leap.
Thus, born out of such need was the Recurrent Neural Network (RNN) (http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.49.1968&rep=rep1&type=pdf). 

# Basic Structure
The basic RNN cell is parameterized by 3 variables, $U, V \text{and} W$. Diagrammatically, it can be envisioned as shown below,

It is completely characterized by its input, hidden and output states. In order to handle sequential data, these cells are unrolled 1 after the other in the fashion shown below,

Observe that the previous state's hidden unit feeds into the next cell and this trend continues. This is how RNNs are deemed to track/learn long term relationships between the sequential data. More details on how this occurs will be provided in later posts. For now it is safe to assume that this link/memory is able to track and learn infromation gathered until that point  in the sequential data.

The RNN can be easily understood when equated to a common looping paradigm in programming languages. It essentially consists of unrolling a standard set of operations over a sequence of inputs. The loop's internal parameters are similar to the hidden state. 

# Mathematical formulation
In its vanilla form, a basic RNN is characterized using the following equations,
\begin{equation}
s_t = f(Ux_t + Ws_{t-1})
\label{eq:hidstate}
\end{equation}

\begin{equation}
o_t = softmax(Vs_t)
\label{eq:output}
\end{equation}

\begin{equation}
E(y,\hat{y}) = -\sum_{t} y_t log(\hat{y_t})
\label{eq:celoss}
\end{equation}

Notice the time dependence on each of these parameters, marked by the $t$ or $t-1$. This recursive formulation does not lend itself to an easy or simple back-propagation formula. Get ready to put your calculus hats on people!!

Since the complete RNN system is parameterized by $U,V \text{and} W$. Hence, we need to find the gradients w.r.t. these parameters. 
Hence, we need to find $\frac{dE}{dV}, \frac{dE}{dW} \text{and} \frac{dE}{dU}$. Here, I dropped the time dependence parameters to make it easier to read.

The first partial derivative that can be easily handled is $\frac{dE}{dV}$.
\begin{align*}
\frac{dE_t}{dV} = y_t * log(\hat{y_t}), \text{where} \\
\hat{y_t} = softmax(Vs_t) \\
if Vs_t = z_t \\
\hat{y_t} = \frac{\exp{z^{i}_t}}{\sum{k=1}{K}z^{k}_t} \\ 
\end{align*}

Here, t is assumed to a specific time-step while z is an alias for $Vs_t$.
\begin{equation}
\frac{dE_t}{dV} = \frac{dE_t}{d\hat{y_t}}*\frac{d\hat{y_t}}{dz_t}*\frac{dz_t}{dV} 
\end{equation}


Expanding the first term yields,
\begin{equation}
\frac{dE_t}{d\hat{y_t}} = \frac{y_t}{\hat{y_t}}
\end{equation}

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
