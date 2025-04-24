#work
`strlen($string)`: Retorna o comprimento de uma string.

`array_push($array, $value)`: Adiciona um ou mais elementos no final de um array.

`count($array)`: Conta todos os elementos de um array.

`var_dump($variable);`para obter mais informações sobre um valor, por exemplo, o tipo que o PHP vê

**`isset`**: Pergunta "Esta variável existe e não é nula?"

php artisan serve --port=8001

`in_array` ele verificar se o que você passou fora do array está dentro do array

	Ex: tenho uma arquivo jpg e um array contendo: ["doc", "docx"] 
	Eu uso  in_array (jpg ["doc", "docx"]) 
	eu pergunto tem jpg dentro do meu array?

`pluck` é usado para extrair uma única coluna de todas as linhas que corresponde á consulta
Ex: 
	`$vacation_employees = Administrador::whereHas('usuario.equipe_usuario', function` `($query) {`  
	    `$query->where('equipe_id', '=', Equipe::EQUIPE_RELACIONAMENTO);`  
    `})`  
    `->where('data_inicio_ferias', '<=', AppUtil::getCurrentDate('Y-m-d'))`  
    `->where('data_fim_ferias', '>=', AppUtil::getCurrentDate('Y-m-d'))`  
    `->pluck('usuario_id')`  
    `->toArray();`
Esse comando vai buscar todos os valores da coluna `usuario_id` das linhas que satisfazem as condições definidas na consulta. Ele retorna esses valores em forma de um array.
Por exemplo, se a consulta retornar 3 registros com `usuario_id` 1, 2 e 3, o `pluck('usuario_id')` vai gerar um array assim: "[1, 2, 3]"


`echo gettype($variavel);` 


`implode(', ', $variavel); -> usar `implode`, pode transformá-lo em uma string, 
ou seja ele transforma um array em uma string cada vez que ele encontrar uma virgula

`explode(', ', $variavel); -> Nesse caso é ao contrario ele transforma uma string em array toda vez que ele encontrar um virgula`


`str_contains($texto, "palavra-qualquer") -> para saber se contem alguma palavra dentro da str`
