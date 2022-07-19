想定解で必要になる知識は

**・セグメント木**

**・包除原理**

です。

$[P.S]$**ウェーブレット行列**というデータ構造を用いると簡単に解けるようです。(未知かつ非想定でした。)

そちらの$verify$としてもお使いください。**他にも色々なデータ構造を用いて解けるようです。**

[**解説**]

クエリの条件は

・[$l_1 \le L \le l_2, r_1 \le R \le r_2$]　→ $[①(l1 \le L) \&(②L \le l_2)\&(③r_1 \le R) \&(④R \le r_2)]$

です。

ここで、余事象を考えると、求める個数は

$ans =$ $n -  not[①\&②\&③\&④]$ ($※$)

です。

$(1) = not①,(2) = not②,(3) = not③,(4) = not④$

とした時、

($※$) $= n - [(1) or (2) or (3) or (4)]$

$= n - [(1)+ (2) + (3) + (4) -(1\&2) - (1\&3) - (1\&4) - (2\&3) - (2\&4) - (3\&4) + (1\&2\&3) + (1\&2\&4) + (1\&3\&4) + (2\&3\&4) - (1\&2\&3\&4)]$

です。

ですが、よく考えると

$(1) = [l_1 > L]$,$(2) = [L > l_2]$,$(3) = [r_1 > R]$,$(4) = [R > r_2]$より、

$(1)\&(2)=∅,(3)\&(4)=∅$です。

つまり上記の式は
$= n - [(1)+ (2) + (3) + (4) - (1\&3) - (1\&4) - (2\&3) - (2\&4)]$

となります。

各クエリにおいて、$(1),(2),(3),(4)$の個数は、$A$の閉区間$[L,R]$の情報を$L,R$について、累積和をとることで$O(1)$で答えることができるのでよいです。

$(1\&3) , (1\&4)$についてですが、これはクエリそれぞれに対して

・$[l_1 > L], [r_1 > R]$なる閉区間の個数

・$[l_1 > L], [R > r_2]$なる閉区間の個数

の個数がわかれば良いです。

これは、クエリを$l_1$で昇順ソートし、順に$l_1 > L$の閉区間$[L,R]$の$R$をセグメント木に足し合わせて更新をしてゆくことでクエリ全体で$O((Q+N)logN)$で回答できます。

$(2\&3) , (2\&4)$についても同様に考えることで、こちらもクエリ全体で$O((Q+N)logN)$で回答できます。

以上より、クエリ全体で$O((Q+N)logN)$で回答をすることができました。