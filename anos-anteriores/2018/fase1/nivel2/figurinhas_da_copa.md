# Figurinhas da Copa

Acesse o problema [aqui](https://neps.academy/br/exercise/168)

## Solução

No problema é dado a quantidade total de espaços do álbum, a quantidade de figurinhas carimbadas e a quantidade de figurinhas que foram compradas.
É preciso imprimir a quantidade de figurinhas carimbadas que faltam para completar o álbum. Inicialmente a resposta é a quantidade de figurinhas carimbadas
 já que não adicionamos nada ainda. Podemos passar por cada figurinha comprada e verificar se ela é carimbada, 
caso ela seja, diminuimos 1 da resposta e marcamos ela como visitada (para não contar figurinhas repetidas).

## Código

```cpp
#include <iostream>

using namespace std;

int main()
{
    int n, c, m;
    cin >> n >> c >> m;
    int stamp[c], fig, res = c;

    for (int i = 0; i < c; i++)
        cin >> stamp[i];

    for (int i = 0; i < m; i++)
    {
        cin >> fig;
        for (int j = 0; j < c; j++)
        {
            if (fig == stamp[j])
            {
                res--;
                stamp[j] = -1;
                break;
            }
        }
    }

    cout << res << endl;
}
```
