# Agenda 3 - Favoritos

![](figura.jpg)

<!--TOC_BEGIN-->
- [Requisitos Novos](#requisitos-novos)
- [Shell](#shell)
- [Ajuda](#ajuda)
- [Raio X](#raio-x)
- [Raio X2](#raio-x2)

<!--TOC_END-->

Ampliando a atividade de agenda 2, vamos criar uma agenda que gerencia os nossos contatos.


## Requisitos Novos

O sistema deverá:

- Mostrando
    - Ordenar os contatos pelo idContato.
    - Se o contato não for favorito use - antes do idContato.
    - Marque os contatos que são favoritados com um @ antes do idContato. 

- Favoritando
    - Favoritar contatos
    - Desfavoritar contatos.
    - Mostrar apenas os favoritos.

## Shell

```bash
#__case iniciando agenda
$add eva oi:8585 claro:9999
$add ana tim:3434 
$add ana casa:4567 oi:8754
$add bia vivo:5454
$add rui casa:3233
$add zac fixo:3131

$agenda
- ana [0:casa:4567][1:oi:8754]
- bia [0:vivo:5454]
- eva [0:oi:8585][1:claro:9999]
- rui [0:casa:3233]
- zac [0:fixo:3131]

#__case favoritando
$fav eva
$fav ana
$fav ana
$fav zac
$fav rex
fail: contato rex nao existe

$agenda
@ ana [0:casa:4567][1:oi:8754]
- bia [0:vivo:5454]
@ eva [0:oi:8585][1:claro:9999]
- rui [0:casa:3233]
@ zac [0:fixo:3131]

#__case lista de favoritos
$favorited
@ ana [0:casa:4567][1:oi:8754]
@ eva [0:oi:8585][1:claro:9999]
@ zac [0:fixo:3131]

#__case removendo contato
$rmContato zac

$agenda
@ ana [0:casa:4567][1:oi:8754]
- bia [0:vivo:5454]
@ eva [0:oi:8585][1:claro:9999]
- rui [0:casa:3233]
@ zac [0:fixo:3131]

$favorited
@ ana [0:casa:4567][1:oi:8754]
@ eva [0:oi:8585][1:claro:9999]

#__case desfavoritando
$unfav ana

$favorited
@ eva [0:oi:8585][1:claro:9999]

$agenda
- ana [0:casa:4567][1:oi:8754]
- bia [0:vivo:5454]
@ eva [0:oi:8585][1:claro:9999]
- rui [0:casa:3233]
$end
```


***
## Ajuda
- Favoritar
    - Favoritar no nosso exemplo, implica tanto em colocar o contato na lista de favoritos, como também definir o atribuito favorito do contato para `true`. - Você pode utilizar um vetor de Contatos para guardar os favoritos ou uma estrutura chave valor.
- Remover
    - Quando remover um contato, lembre de removê-lo dos favoritos se necessário.
- Desfavoritar
    - Quando desfavoritar um contato, lembre de tanto remover da lista de favoritos como também alterar o valor do atributo `favorited` no próprio contato.

***
## Raio X

```c++
class Fone
- id: string
- number: string
--
+ _validar_(number): bool
--
+ constructor(id, number)
```

```c++
class Contato
- id: string
- fones: Fone[]
- favorited: bool
--
+ addFone(id, number)
+ rmFone(id)
--
+ constructor(id, number)
```

```c++
class Agenda
- contatos: Contato[]
- favoritos: Contato[]

    map<string, Contato> contatos;
    map<string, Contato*> favoritos;
--
+ addContato(idContato, Contato): void
    se contatos

+ rmContato(id): void
    se contato existe
        remove da lista de contatos
        e remove da lista de favoritos

+ getAllContatos(): Contato[]

+ favoritar(id)
    contato = getContato(id)
    if not contato.favorited:
        contato.favorited = true
        favoritos[id] = contato

+ desfavoritar(id)
    contato = getContato(id)
    if contato.favorited:
        contato.favorited = false
        favoritos.remove(id)
    
+ getFavoritos(): Contato[]
    return favorited
--
```

___
## Raio X2

```c++
class Fone
- id: string
- number: string
--
+ _validar_(number): bool
--
+ constructor(id, number)
```

```c++
class Contato
- id: string
- fones: Fone[]
--
+ addFone(id, number)
+ rmFone(id)
--
+ constructor(id, number)
```

```c++
class Agenda
- contatos: Contato[]
--
+ addContato(idContato, Contato): void
+ rmContato(id): void
+ getAllContatos(): Contato[]
```

```c++
class ServicoFavoritagem
+ agenda: Agenda
+ favoritos: Contato[]

+ favoritar(id)
    pegar o contato na agenda
    adicionar o contato nos favoritos

+ desfavoritar(id)
    pegar o contato na agenda
    remover o contato dos favoritos

+ getFavoritos(): Contato[]
    retornar os favoritos

+ agendaComFavoritos(): string
--
ServicoFavoritagem(agenda: Agenda)
```