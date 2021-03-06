---
title: 【十分性】メルセンヌ数が素数であることの判定法を春から東大生の人が頑張って読んでみる
date: 2021-03-18 14:54:10
tags: 数学
categories: blog
authorId: hanaofan
---

こんにちは。ドット会中の人です。
今までは大学受験について色々書いてきたわけですが，
今回は，ちょっとテーマを変えて，大学での勉強の予習(?)をしてみたので，それについてです。

題材にしたのは，[リュカ-レーマー・テスト](https://ja.wikipedia.org/wiki/%E3%83%AA%E3%83%A5%E3%82%AB%E2%80%93%E3%83%AC%E3%83%BC%E3%83%9E%E3%83%BC%E3%83%BB%E3%83%86%E3%82%B9%E3%83%88%E3%81%AE%E8%A8%BC%E6%98%8E)です。これはメルセンヌ数 $ M_p=2^p-1 $ が素数かどうかを判定するテストです。ドット会の別の中の人に教えてもらい，興味を持ちました。

**数論は，論理を理解するだけなら高校数学レベルで対応できる**ことが多いので，ちょうどいいかなと思いました。実際，論理をたどっていくと，**受験勉強で使ったテクニックが盛りだくさん**で，びっくりしました。皆さんにその感覚が伝わるよう，分かりやすく書いたつもりです。

ただ，このテストは本当は必要十分条件を示してくれているのですが，**必要性に関しては，平方剰余の相互法則という難しそうなもの**が必要だったので，今回は，一般的な高校生だったドット会の中の人でも理解できた，十分性の方だけでお許しください。

なお，証明の流れはWikipediaを参考にしました。参考文献でWikipediaを使うのはあまりよくないのは承知していますが，他にソースをまだ知らないので，お許しください。

## 2021/03/22 追記

このテストの成立背景をたまたま別の本で見かけたので，こちらについても別の記事でまとめてみました。

{% hatenablogcard https://dotkai.netlify.app/lucas-lehmer-test-2/ %}

証明と背景を知って，2度楽しむことができました。

## 概要

メルセンヌ数$M_n$は，$M_n=2^n-1$と定義される（$n$は自然数）。
数列${S_n}$を，次のように定義する。

$$
S_0=4,S_n=S_{n-1}^2-2 (n\geq1)
$$

この時，$p$ を奇素数$(p\geq3)$として，$S_{p-2}$が$M_p$で割り切れるならば，$M_p$が素数であることを示す。

## 証明

### 背理法の仮定

> ここはWikipediaとほぼ同じです。背理法を用いて証明します。

$S_{p-2}$が$M_p$で割り切れ，かつ$M_p$が合成数であると仮定する（背理法）。
すると，$S_{p-2}$は，$M_p$の素因数のうち，一番小さい素因数$F$を用いて，$S_{p-2}=kF$（$k$は自然数）と表せる。…①

### $S_n$の一般項の導出

> 個人的にまずこの部分がワクワクしました。
> Wikipediaとほぼ同じ説明となりますが，(前項)²と定数項が含まれる漸化式の処理の仕方は，勉強になりました。
> $a_n=a_{n-1}^2$の場合は，$a_n=A^{2^n}$の形に持ち込めますが，この場合はそうはいきません。
> そこで，指数が$2^n$となる項を2つ用意して，一般項が$S_n=A^{2^n}+B^{2^n}$の形に落ち着くことを見込んで処理しています。

$S_0=\alpha+\beta$とすると，$S_1=\alpha^2+2\alpha\beta+\beta^2-2$。
よって，$S_0=4$より，$\alpha+\beta=4$，$2\alpha\beta-2=0$すなわち$\alpha\beta=1$となるように$\alpha,\beta$を定めれば，
$$ S_n = \alpha^{2^n}+\beta^{2^n} $$ と表せる。

> 2021/03/22 追記：[成立背景を踏まえる](https://dotkai.netlify.app/lucas-lehmer-test-2/)と，リュカ数列の一般項$L_n=\alpha^n+\beta^n$（$\alpha,\beta$は$x^2-x-1=0$の解）を参考にしていると言った方がいいかもしれませんね。$\alpha,\beta$の2文字を用いるのは技巧的ですごいな，と思ったのですが，実は発想は自然だったのかもしれませんね。

> このような$\alpha,\beta$は，2次方程式を作って解けばいいですね。**高校数学・受験数学で散々使ったテクニックがここでも生きるのは，気持ちいいですね**。

$\alpha,\beta$を解に持つ2次方程式$t^2-4t+1=0$を解くと，
$$
\alpha=2+\sqrt{3},\beta=2-\sqrt{3}
$$
となる。

### $\alpha^{2^p}$の剰余取り出し

> ここはWikipediaとほぼ同じです。**剰余の矛盾から題意を示すのは，東大2019理系数学第4問でも登場した考え方です**（今回の証明では，最後の一押しは大小関係を利用していますが）。
> $a+b\sqrt{3}$という数がよく登場します。**剰余の概念を，そのような数にも当てはめられるように拡張しています**。この形の数は，ガウス整数に似ていますね。

①より，
$$
\alpha^{2^{p-2}}+\beta^{2^{p-2}}=kF
$$
となる。

$\alpha\beta=1$なので，両辺に$\alpha^{2^{p-2}}$をかけて，整理すると，

$$
\alpha^{2^{p-1}}=kF\alpha^{2^{p-2}}-1
$$

…②

両辺2乗して，

$$
\alpha^{2^p}=k^2 F^2\alpha^{2^{p-1}}-2kF\alpha^{2^{p-2}}+1
$$

よって，

$$
\alpha^{2^p}\equiv 1 \pmod F
$$

となる。…③

ただし，$a+b\sqrt{3}$と$c+d\sqrt{3}$（$a,b,c,d$は整数）で表される2数について，$a\equiv c \pmod F$かつ $b\equiv d \pmod F$のとき，2数は$F$を法として合同であるとする。

### 鳩の巣原理の利用

> ここはWikipediaと説明を変えました。ただ，どちらの説明も，受験数学でも頻出な，鳩の巣原理を用いています。

$n$を整数として，$g_n=a_n+b_n\sqrt{3}$ とする。
ただし，整数$a_n,b_n$を，$0\leq a_n&lt;F,0\leq b_n&lt; F, g_n\equiv \alpha^n \pmod F$を満たすように定める。
このとき，$g_n$ はただ1つに定まる。

以下，$\alpha\neq 0$であることに注意する。
$n=0$の時，$g_n\equiv\alpha^0=1 \pmod F$である。
$n\neq 0$のすべての整数$n$について，$g_n \cdot g_{-n} \equiv \alpha^n\cdot\alpha^{-n}=1 \pmod F$である。
これらのことから，すべての整数$n$について，$g_n\not\equiv 0 \pmod F$である。
一方，$g_n=0$ならば，$g_n\equiv 0 \pmod F$となるはずである。
よって，$g_n\neq 0$である。つまり，$a_n$と$b_n$のどちらか一方は$0$でない。
すると，$g_n$の取りうる値は，高々$F^2-1$種類である。なぜなら，$a_n,b_n$の取りうる値がそれぞれ$F$種類であり，また$(a_n,b_n)\neq(0,0)$だからである。

> 正直，「高々$F^2$種類」の評価でも十分な気がしますが，ここは英語版Wikipediaでも，$F^2-1$にしていたので，少し面倒な説明を加え，評価を厳しくしておきました。なんでだろう。

これらのことから，$0\leq i&lt;j\leq F^2-1$として，$g_i=g_j$となる$(i,j)$の組が必ず存在する（鳩の巣原理）。
すると，$i>0$の時は，$g_{i-1}=g_{j-1},g_{i-2}=g_{j-2},...,g_0=g_{j-i}$も順々に成立することが分かる。(※厳密な証明は後ろの補題参照)
これらのことから，$0\leq i$で$g_0=g_{j-i}$が成立する。
ここで，$0&lt;j-i\leq F^2-1$である。$j-i=e$とすると，$g_e=g_0$。
$g_0\equiv \alpha^0=1$であることと定義より，$g_0=1$なので，$g_e=1$

> ↑の説明は，**東大2014理系数学第5問とほぼ同じです**。よくあるテクニックなのでしょうか。

以下，このような$e$で考えられるもののうち，$e$が最小の自然数となるものについて考える。すると，$g_{r}=g_{je+r}$が成立（$j$は$0$以上の整数，$r$は$0\leq r&lt;e$を満たす整数）。
$0&lt;r&lt;e$ならば，$g_r\neq 1$（$e$は考えられるもののうち最小の自然数のため）なので，全ての自然数$n$に対して，$g_n=1$であることと，$n$が$e$の倍数であることは同値である。

#### ※補題の証明

先ほどの(※)の説明には，次のような補題の証明が必要でした。
##### 補題
$a+b\sqrt{3}$（$a,b$は整数）と表せる数$A,B,C$について，
$AC\equiv BC \pmod F$ならば，$A\equiv B \pmod F$である。

ただし，$P=a+b\sqrt{3}$（$a,b$は整数）の時，$\bar{P}=a-b\sqrt{3}$と表記したとき，
$ C\not\equiv 0 \pmod F, \bar{C}\not\equiv 0 \pmod F $であるとする。

これを示す。
##### 証明
$A=a+b\sqrt{3},B=c+d\sqrt{3},C=p+q\sqrt{3}$とする（$a,b,c,d,p,q$は整数）。

$$
AC=(a+b\sqrt{3})(p+q\sqrt{3})=ap+3bq+(ap+bq)\sqrt{3},\\\\
BC=(c+d\sqrt{3})(p+q\sqrt{3})=cp+3dq+(cq+dp)\sqrt{3}
$$
よって，
$$AC-BC=(a-c)p+3(b-d)q+\\{q(a-c)+p(b-d)\\}\sqrt{3}$$
$AC\equiv BC \pmod F$なので，$k,l$を整数として，
$$
(a-c)p+3(b-d)q=kF,q(a-c)+p(b-d)=lF
$$
と表せる。
これらから，次の2式を得る。
$$
(p^2-3q^2)(a-c)=(kp-3lq)F,(3q^2-p^2)(b-d)=(kq-lp)F
$$

ここで，$ C\not\equiv 0 \pmod F, \bar{C}\not\equiv 0 \pmod F $であることから，$p^2-3q^2$は$F$で割り切れない。
また，$F$は素因数であることから，それぞれ，$a-c,b-d$が$F$で割り切れることがわかり，$A-B\equiv 0 \pmod F$が成り立つ。

これらのことから，$A\equiv B \pmod F$が示された。

##### 補題の適用法

$ g_i\equiv g_{i-1}\alpha, g_j\equiv g_{j-1}\alpha \pmod F$であることから，$ g_i\equiv g_j $より，$ g_{i-1}\alpha\equiv g_{j-1}\alpha $である。
$\alpha\not\equiv 0,\bar{\alpha}\not\equiv 0 \pmod F$は明らかなので，$g_{i-1}\equiv g_{j-1} \pmod F$が示された。

### 剰余の利用

> ここはWikipediaとほぼ同じです。

③より，
$$
\alpha^{2^p}\equiv 1,\alpha^e\equiv 1 \pmod F
$$

このことから，$2^p$は$e$の倍数。明らかに，$2^p>0$である。$2^p>e$であるとすると，$e$は$2^p$の約数なので，$e=2^t$（$t$は$0\leq t\leq p-1$を満たす整数）となる。すなわち，$e=2^t\leq2^{p-1}$となり，$2^{p-1}$は$e$の倍数。よって，

$$
\alpha^{2^{p-1}}\equiv 1 \pmod F
$$

が成立する。しかし，②より，
$$
\alpha^{2^{p-1}}\equiv -1 \pmod F
$$
である。この2つが両立するには，$1-(-1)=2$が$F$の倍数である必要があり，$F$は素因数であるから，$F=2$である。しかし，仮定より，$S_{p-2}$は$M_p$の倍数であり，$M_p=2^p-1$で奇数なので，$S_{p-2}$が素因数$2$を持つことはない。

よって，$2^p=e$であると言える。しかし，$F$は$M_p$の一番小さい素因数であり，$M_p$は合成数なので，$F^2 \leq M_p$

$$
F^2\leq M_p=2^p-1&lt; 2^p=e
$$

よって，$F^2&lt;e$となるが，$e\leq F^2-1$であるので，
$F^2&lt;F^2-1$が成立してしまい，これは矛盾。

> $F^2\leq F^2-1$でも十分な気がするので，先ほどの評価はやはり無駄に厳しくなっていたように思えます。

よって，$S_{p-2}$が$M_p$で割り切れるならば，$M_p$が素数であることが示された。

## まとめ

思いのほか，登場したテクニックが受験数学と同じでびっくりです。
入試問題を解いているような感覚で考えられました。

その点では，入試問題のような鮮やかさがあって，面白かったです。
（まだ僕がつかめていない面白さも，この問題には眠っているのかもしれませんが）

結構受験勉強は，その後の勉強にも役に立つのかもしれないですね。

また，**Wikipediaの説明が雑すぎる気がしました**。**論理の飛躍や，必要な場合分けが抜けている箇所が多かった**ように感じます。常識すぎるから省略しているだけなのでしょうか。
