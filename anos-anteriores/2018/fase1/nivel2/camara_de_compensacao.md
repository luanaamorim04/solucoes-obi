# Câmara de Compensação

Acesse o problema [aqui](https://neps.academy/br/exercise/169)

## Solução
O problema da uma lista de compensação e quer saber se é possível diminuir o total compensado e qual seria o total mínimo de valores compensados (a soma dos cheques emitidos).
É possível perceber que é melhor fazer uma transação direta do que indireta, como por exemplo: Temos as pessoas A, B e C, a pessoas A empresta 5 dinheiros para B e B
empresta 4 dinheiros para a pessoa C (a soma total fica igual a 9), ao final A fica devendo 5 dinheiros, B ganhou 1 dinheiro e C ganhou 4 dinheiros. Mas seria melhor que A desse 1 dinheiro para B
e depois desse 4 dinheiros para C. O total compensado sempre vai ser a <b>soma de saldos positivos</b>, pois sempre uma pessoa que acaba devendo pode enviar diretamente esse
dinheiro para outra pessoa com saldo positivo.

## Código
```cpp
#include <iostream>
#include <queue>
#include <string>
#include <algorithm> 
#include <vector>
#include <cmath> 
#include <iomanip>
#include <map>
#define INF 99999999
#define MOD 1000000007
#define par pair<int, int>
#define _ ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);

using namespace std;

int n, m, saldo[1000009], ans, a1;

int main()
{_
    cin >> m >> n;
    for (int i = 0; i < m; i++)
    {
        int a, b, v;
        cin >> a >> v >> b;
        saldo[a] -= v;
        saldo[b] += v;
        a1 += v;
    }

    for (int i = 1; i <= n; i++)
    {
        if (saldo[i] > 0) ans += saldo[i];
    }

    cout << (ans == a1 ? "N" : "S") << endl;
    cout << ans << endl;
}
```
