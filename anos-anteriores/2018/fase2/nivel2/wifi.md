# Wifi

Acesse o problema [aqui](https://olimpiada.ic.unicamp.br/pratique/p2/2018/f2/wifi/)

## Pré requisitos 
* sweep line
* segmentation tree
* lazy propagation 

## Solução
Para resolver esse problema primeiramente imagino uma linha de varredura da esquerda para a direita fazendo duas operações: adicionando um retângulo e eliminando ele. Eu guardo todas as operações num vector de uma struct que criei com as seguintes informações: o ponto X onde a operação está ocorrendo (pois a linha vai da esquerda para a direita), a própria operação (0 ou 1), as coordenadas Y do retângulo, e o identificador do retângulo. Depois eu ordeno todas as operações de acordo com o X. Agora eu analiso uma só linha vertical do ponto X atual que estou, quando eu adiciono um retangulo, checo se existe algum retângulo que engloba o que estou adicionando (se tiver um retangulo englobando ele, eu marco o "pai" como desnecessario e ignoro ele na resposta) e depois faço um update na seg3 colocando todos os valores de Y1 até Y2 com o id do retangulo. Quando estou deletando um retângulo, apenas faço um update no intervalo Y1 e Y2 com o retangulo que estava antes do atual (o pai dele).   

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
#include <cstring>
#include <set>
#include <stack>
#include <bitset>
#define ll long long
#define INF (1e9)
#define MAX (int) (2e5 + 5)
#define MOD 1000000007
#define par pair<int, int>
#define all(v) v.begin(), v.end()
#define sz(x) (int) ((x).size())
#define esq(x) (x<<1)
#define dir(x) ((x<<1)|1)
#define lsb(x) (x & -x)
#define W(x) cout << #x << ": " << x << endl
#define Wii(x) cout << x.first << ' ' << x.second << endl
#define _ ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);

using namespace std;

struct trect
{
	int op, x, a, b, id;
	int operator<(trect q) const{
		return x<q.x;
	}
};

int n, resp, idx, a, b, c, d, lazy[MAX], st[MAX], pai[MAX], filho[MAX], maior;
vector<int> coord;
map<int, int> val;
vector<trect> rect;

void push(int idx, int i, int j)
{
	if (!lazy[idx]) return;
	st[idx] = lazy[idx];
	if (i != j) lazy[esq(idx)] = lazy[dir(idx)] = lazy[idx];
	lazy[idx] = 0;
}

void update(int idx, int i, int j, int l, int r, int val)
{
	push(idx, i, j);
	if (i > r || j < l) return;
	if (i >= l && j <= r)
	{
		lazy[idx] = val;
		push(idx, i, j);
		return;
	}
	int mid = ((i+j)>>1);
	update(esq(idx), i, mid, l, r, val);
	update(dir(idx), mid+1, j, l, r, val);
}

int query(int idx, int i, int j, int pos)
{
	push(idx, i, j);
	if (i == j) return st[idx];
	int mid = ((i+j)>>1);
	if (pos <= mid) return query(esq(idx), i, mid, pos);
	else return query(dir(idx), mid+1, j, pos);
}

int main()
{_
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		cin >> a >> b >> c >> d;
		coord.push_back(a);
		coord.push_back(b);
		coord.push_back(c);
		coord.push_back(d);
		rect.push_back({1, a, d, b, ++idx});
		rect.push_back({0, c, d, b, idx});
		pai[idx] = idx;
	}

	sort(all(rect));
	sort(all(coord));
	maior = sz(coord);
	for (int i = 1; i < coord.size(); i++) val[coord[i]] = i;

	for (auto[op, x, a, b, id] : rect)
	{
		a = val[a];
		b = val[b];
		if (op)
		{	
			pai[id] = query(1, 1, maior, a);
			filho[pai[id]] = 1;
			update(1, 1, maior, a, b, id);
		}
		else
		{
			update(1, 1, maior, a, b, pai[id]);
		}
	}

	for (int i = 1; i <= n; i++) resp += !filho[i];

	cout << resp << endl;
}	
```
