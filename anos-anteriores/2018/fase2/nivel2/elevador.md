# Elevador

Acesse o problema [aqui](https://olimpiada.ic.unicamp.br/pratique/p2/2018/f2/elevador/)

## Solução
No problema são aprensentadas 2 cabines que podem levar uma caixa por vez cada uma uma. Porém não é possível fazer a viagem se as caixas nas 2 cabines tiverem uma diferença de peso maior que 8 e o problema quer saber se é possível levar todas as caixas para o segundo andar. Para isso eu ordeno o array que contém os pesos das caixas e vejo se duas caixas consecutivas tem diferença maior do que 8, caso elas tenham então não será possível.

## Código
```cpp
#include <iostream>
#include <queue>
#include <string>
#include <algorithm> 
#include <vector>
#include <cmath> 
#define INF 999999999
#define par pair<int, int>
#define _ ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);

using namespace std;

int n, v[10009];

int main()
{_
    cin >> n;
    v[0] = 0;
    for (int i = 1; i <= n; i++)
        cin >> v[i];

    sort(v, v+n+1);

    for (int i = 1; i <= n; i++)
    {
        if (v[i] - v[i - 1] > 8)
        {
            cout << 'N';
            return 0;
        }
    }

    cout << 'S';
}
```
