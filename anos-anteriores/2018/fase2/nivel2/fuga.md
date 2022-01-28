# Fuga

Acesse o problema [aqui](https://olimpiada.ic.unicamp.br/pratique/p2/2018/f2/fuga/)

## Solução
Para solucionar esse problema é importante perceber que qualquer caminho que não passe por posições em que o x e o y são ambos pares, é válida, ou seja, sempre é possível derrubar todos os armários de forma que nenhum interfira no caminho traçado. Com isso eu fiz uma função que gera todas as possibilidades de caminhos e imprimo a maior.


## Código
```cpp
#include <iostream>
#include <queue>
#include <string>
#include <algorithm> 
#include <vector>
#include <cmath> 
#include <iomanip>
#include <stack>
#include <map>
#define INF 99999999
#define MOD 1000000007
#define par pair<int, int>
#define MAXN (int) 1e5 + 9
#define lsb(x) ((x) & (-x))
#define _ ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);

using namespace std;

int n, m, a, b, c, d, n_pode[15][15], k, ans;

void f(int a, int b)
{
    if (a < 1 || b < 1 || a > n || b > m) return;
    if (a % 2 == 0 && b % 2 == 0) return;
    n_pode[a][b] = 1;
    k++;
    if (a == c && b == d) 
    {
        ans = max(ans, k);
    }
    else
    {
        for (int i = -1; i <= 1; i++)
            for (int j = -1; j <= 1; j++)
                if ((!i || !j) && !n_pode[a + i][b + j]) f(a + i, b + j);
    }
    
    k--;
    n_pode[a][b] = 0;
}   

int main()
{_  
    cin >> n >> m >> a >> b >> c >> d;
    f(a, b);
    cout << ans << endl;
}
```
