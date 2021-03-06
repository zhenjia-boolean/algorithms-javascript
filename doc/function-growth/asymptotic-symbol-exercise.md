### 渐进记号习题

#### `问题1`

***

设$f(n)$与$g(n)$都是渐进非负函数。利用$\Theta$记号的基本定义来证明$max(f(n),g(n))=\Theta(f(n)+g(n))$。


#### `答案`

根据$\Theta$记号的定义，只需要证明存在常量$c_1$和$c_2$，使得$0≤c1(f(n)+g(n))≤max(f(n),g(n))≤c2(f(n)+g(n))$，

这里使$c_1 = 0.5，c_2 = 1$，便可使等式成立。



#### `问题2`

***

证明对任意实常数$a$和$b$，其中$b \gt 0$，有$(n+a)^b=\Theta(n^b)$。

#### `答案`

上述问题即证明 $0 \le c1(n^b) \le (n+a)^b \le c2(n^b)$

等式同除以$n^b$，即证明  $0 \le c1 \le (1+{a \over n})^b \le c2$

取$n_0 = a$，即证明  $0 \le c1 \le 2^b \le c2$

因此可取$c_1 = {1\over2}^b、c_2=3^b、n_0=a$使得等式 $0 \le c1(n^b) \le (n+a)^b \le c2(n^b)$成功，因此有$(n+a)^b=\Theta(n^b)$


#### `问题3`

***

解释为什么“算法A的运行时间至少是$O(n^2)$”这句话是无意义的。

#### `答案`

$O$记号标识的运行上界，而**至少是**表明的是运行下界。


#### `问题4`

***

$2^{(n+1)}=O(2^n)$成立吗？$2^{(2n)}=O(2^n)$成立吗？


#### `答案`

（1）成立，根据定义只需要存在$c$，使得$0≤2^{n+1}≤c2^n$，满足$c \gt 2$即可。
（2）不成立，根据定义需要存在$c$，使得$0≤2^{2n}≤c2^n$，即使得$0≤2^{n}≤c$，由于$n$是变化的，因此不可能存在常量$c$。



#### `问题5`

***

证明定理：对任意两个函数$f(n)$和$g(n)$，我们有$f(n)=\Theta(g(n))$，当且仅当$f(n)=O(g(n))$且$f(n)=Ω(g(n))$。

#### `答案`

充分性：$f(n)=Θ(g(n))$意味着存在$c_1、c_2和n_0$（其中$n \ge n_0$）使得$0 \le c_1g(n) \le f(n) \le c_2g(n)$。我们由此可推出以下两个结论：
存在$c_1$和$n_0$（其中$n \ge n_0$）使得$0 \le c_1g(n) \le f(n)$，即$f(n)=Ω(g(n))$
存在$c_2$和$n_0$（其中$n \ge n_0$）使得$0 \le f(n) \le c_2g(n)$，即$f(n)=O(g(n))$

必要性：$f(n)=Ω(g(n))$意味着存在$c_1$和$n_1$（其中$n \ge n_1$）使得$0 \le c_1g(n) \le f(n)$。类似的，$f(n)=O(g(n))$意味着存在$c_2$和$n_2$（其中$n \ge n2$）使得$0 \le f(n) \le c_2g(n)$。 令$n0=max(n_1, n_2)$，由$Θ$的定义我们有：$f(n) = Θ(g(n))$。

#### `问题6`

***

证明：一个算法的运行时间是$\Theta(g(n))$当且仅当其最坏情况运行时间$O(g(n))$，且最佳情况运行时间是$Ω(g(n))$。

#### `答案`

同问题5。

#### `问题7`

***

证明$o(g(n))∩ω(g(n))$是空集。

#### `答案`

对于$g(n)$而言，一个是非渐进上界，一个是非渐进下界，两个自然无交集。

证明略。


#### `问题8`

***

可以将我们的表示法扩展到有两个参数n和m的情形，其中n和m的值可以以不同的速率，互相独立地趋于无穷。对给定的函数$g(n,m)$，$O(g(n,m))$为函数集

$$O(g(n,m))= \\{ f(n,m): 存在正整数c,n0和m0，使对所有n>=n0或m>=m0，有0<=f(n,m)<=cg(n,m) \\}$$

给出对应的$Ω(g(n,m))$和$Θ(g(n,m))$的定义。


#### `答案`

定义略，比较简单。



