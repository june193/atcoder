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

