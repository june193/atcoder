AtCoderのコンテストで使うライブラリ(テキストエディタにスニペットとして事前に登録してあるPythonのコード)の一覧です。

## スタックによる非再帰のオイラーツアー
```python
#グラフの隣接リストは事前に作っておくこと

path = []
visited = [False]*(N+1)
sta = ●
ET = []
ET.append(~sta)
ET.append(sta)

while ET:
    nex = ET.pop()
    if nex >= 0:
        visited[nex] = True
        path.append(nex)

        for j in G[nex]:
            if visited[j]:
                continue
            ET.append(~j)
            ET.append(j)
    else:
        path.append(~nex)

#=======パスを出力=======
#print(path)
#=======================

inin = [10**10]*(N+1)
out = [-1]*(N+1)

for i,v in enumerate(path):
    inin[v] = min(inin[v],i)
    out[v] = max(out[v],i)
```
## 2次元リストG1を縦にスライド、横にスライドを繰り返してG2と一致させることができるかを判定する
```python
def compare_2D_grid(G1,G2,H,W):
    """
    2次元リストG1を縦にスライド、横にスライドを繰り返して
    G2と一致させることができるかを判定する。
    G1 = 1つめの2次元リスト、G2 = 2つめの2次元リスト
    H = 縦
    W = 横
    """
    for i in range(H):
        for j in range(W):
            flag = True
            for ii in range(H):
                for jj in range(W):
                    if G1[(i+ii)%H][(j+jj)%W] != G2[ii][jj]:
                        flag = False
            if flag:
                return "下に",i,"マス、右に",j,"マスずらすと一致する"
    return False

H,W = 2,2
A = [["#","."],[".","."]]
B = [[".","."],[".","#"]]

ans = compare_2D_grid(A,B,H,W)

if ans == False:
    print("No")
else:
    print("Yes")
    print(ans)
```
## 2次元配列から図形部分だけを切り出す
```python
import copy
def kiri(x):
    """
    ....
    .#.. → #.
    .##..→ ##
    ....

    図形を表現する2次元配列が与えられたときに
    上のように図形部分だけを切り出した2次元配列を返す
    """
    tl,tr,bl,br = [10**10,10**10],[10**10,-1],[-1,10**10],[-1,-1]
    for ii in range(len(x)):
        for jj in range(len(x[ii])):
            if x[ii][jj] == "#":  #←図形を表現する文字列が#じゃないとき適宜書き換える
                tl[0],tl[1] = min(tl[0],ii),min(tl[1],jj)
                tr[0],tr[1] = min(tr[0],ii),max(tr[1],jj)
                bl[0],bl[1] = max(bl[0],ii),min(bl[1],jj)
                br[0],br[1] = max(br[0],ii),max(br[1],jj)
    tmpkiri = []
    tp,btm,lt,rt = min(tl[0],tr[0]),max(bl[0],br[0]),min(tl[1],bl[1]),max(tr[1],br[1])

    for iii in range(tp,btm+1):
        tmpkiri.append(x[iii][lt:rt+1])

    return copy.deepcopy(tmpkiri)
```

