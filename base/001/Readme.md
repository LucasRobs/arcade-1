# Calculadora com bateria

<!--TOC_BEGIN-->
- [Requisitos](#requisitos)
- [Shell](#shell)
- [Diagrama](#diagrama)
- [Ajuda](#ajuda)
- [Main não interativa](#main-não-interativa)
- [Respostas](#respostas)

<!--TOC_END-->

![](figura.jpg)

O objetivo dessa atividade é implementar uma calculadora a bateria. Se há bateria, ela executa operações de soma, multiplicação e divisão. É possível também mostrar a quantidade de bateria e recarregar a calculadora. Ela avisa quando está sem bateria e se há tentativa de divisão por 0.


***
## Requisitos

- Mostrar bateria da calculadora.
- Recarregar a bateria.
- Realizar operações matemáticas de soma e divisão.
- Se o usuário tentar realizar operações e a bateria estiver vazia, deverá ser mostrada uma notificação sobre falta de bateria.
- Se o resultado da divisão for zero, deve ser notificado o erro.


***
## Shell

```bash
#__case iniciar mostrar e recarregar
# O comando "$init M" inicia uma calculadora com carga inicial 0 e bateria máxima M.
# O comando "$show" mostra o valor da última operação bem sucedida no display e o estado da bateria
# O comando "$charge V" recarrega a bateria de V
$init 5
$show
display = 0.00, battery = 0
$charge 3
$show
display = 0.00, battery = 3
$charge 1
$show
display = 0.00, battery = 4
$charge 2
$show
display = 0.00, battery = 5
$init 4
$charge 2
$show
display = 0.00, battery = 2
$charge 3
$show
display = 0.00, battery = 4
$end	
```	
```bash
#__case somando
# O comando "$sum V1 V2" soma e mostra o resultado da soma. Para isso ele precisa gastar uma unidade de bateria. Caso não exista bateria suficiente informe.
$init 2
$charge 2
$sum 4 3
$show
display = 7.00, battery = 1
$sum 2 3
$show
display = 5.00, battery = 0
$sum -4 -1
fail: bateria insuficiente
$charge 1
$show
display = 5.00, battery = 1
$sum -4 -2
$show
display = -6.00, battery = 0
$end
```
```bash
#__case dividindo
# O comando "$div A B" consome uma unidade de bateria e apresenta o resultado da divisão inteira entre os números inteiros A e B. Se B for 0 ou não houver bateria, informe os erros. Tentar dividir por 0 consome uma unidade de bateria.
$init 3
$charge 3
$div 6 3
$div 7 0
fail: divisao por zero
$show
display = 2.00, battery = 1
$div 7 2
$div 10 2
fail: bateria insuficiente
$show
display = 3.50, battery = 0
$end
```
## Diagrama
![](diagrama.png)

***    

## Ajuda

Você pode formatar floats com duas casas decimais em java usando essa classe

```java
import java.text.*;
  
class Decimals {
  public static void main(String[] args) {
    float f = 125.0f;
    DecimalFormat form = new DecimalFormat("0.00");
    System.out.println(form.format(f));
  }
}
```

## Main não interativa
```java
Calculadora calc = new Calculadora(5);
System.out.println(calc);
//display = 0.00, battery = 0
calc.charge(3);
System.out.println(calc);
//display = 0.00, battery = 3
calc.charge(1);
System.out.println(calc);
//display = 0.00, battery = 4
calc.charge(2);
System.out.println(calc);
//display = 0.00, battery = 5

calc = new Calculadora(4);
calc.charge(2);
System.out.println(calc);
//display = 0.00, battery = 2
calc.charge(3);
System.out.println(calc);
//display = 0.00, battery = 4

calc = new Calculadora(2);
calc.charge(2);
calc.soma(4, 3);
System.out.println(calc);
//display = 7.00, battery = 1
calc.soma(2, 3);
System.out.println(calc);
//display = 5.00, battery = 0
calc.soma(-4, -1);
//fail: bateria insuficiente
calc.charge(1);
System.out.println(calc);
//display = 5.00, battery = 1
calc.soma(-4, -2);
System.out.println(calc);
//display = -6.00, battery = 0

calc = new Calculadora(3);
calc.charge(3);
calc.div(6, 3);
calc.div(7, 0);
//fail: divisao por zero
System.out.println(calc);
//display = 2.00, battery = 1
calc.div(7, 2);
calc.div(10, 2);
//fail: bateria insuficiente
System.out.println(calc);
//display = 3.50, battery = 0
```

## Respostas

- Respostas
    - [C++](solver.cpp)
    - [Java](Solver.java)