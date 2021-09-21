# Piso da Escola
 
  Acesse o problema [aqui](https://neps.academy/br/exercise/167)
  
  ## Solução
  As diagonais dos quadrados sempre valem 1, então sempre terão ao menos LxC lajotas do tipo 1. E como entre cada par de lajotas que não estão nas extremidades
  existe outra lajota do tipo 1, teremos que somar (L-1)*(C-1) na quantidade de lajotas do tipo 1.
  Entre cada par de lajotas do tipo 1 que estão ambos nas extremidades das linhas ou das colunas, existe uma lajota do tipo 2. 
  Com isso, podemos afirmar que existem 2*(L-1)+2*(C-1) lajotas do tipo 2. 
   
  ## Código
  ```cpp
  #include <iostream>
#include <iomanip>

using namespace std;

int main()
{
    int a, b;
    cin >> a >> b;
    cout << a * b + ((a - 1) * (b - 1)) << endl;
    cout << 2 * (a - 1 + b - 1) << endl;
}
  ```
