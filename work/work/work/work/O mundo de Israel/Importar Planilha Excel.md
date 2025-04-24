
Existe uma biblioteca chamada **Maatwebsite Excel** ela não vem por padrão no Laravel é preciso instalar

`$variavel_qualquer = Excel::toArray([],$file)` 

Na maioria das vezes ao carregar uma planilha ela virá com um numero muito grande de dados, nesse caso preciso usar um foreach para acessar cada array
![[Pasted image 20250120161847.png]]

Existem dois foreach nesse caso, um por conta das abas da planilha, então eu percorro cada uma dessas abas **(Não usar isso quando a planilho tem somente uma aba)**

O segundo foreach percorro cada linha da tabela

Ambos os foreach eu passo a $key, que significa que eu estou pegando a chave(posição de determinado no array que eu estou acessando)

Depois eu passo em duas verificações 'IF' e se ás consições forem verdadeira eu coloquei **continue** e **continue 2**

O **continue** se a condição for verdadeira eu literalmente continuo simplesmente indo para o proximo item
Ex: Supondo que eu tenho uma lista de frutas e ela é um array com duas posições 
`$frutas = ['maça', 'banana'];` ao dar o continue ele ignora a **maça** e já vai direto para **banana** 
Eu posso passar um `var_dump($key, $frutas);die;` para poder saber a posição e o item que eu estou, o resultado nesse caso seria `1, banana`