
Tenho um array:
`$lista = ['pão', 'presunto', 'queijo', 'café', 'suco'];`

para acessar cada item desse array preciso usar o foreach:
`foreach($lista as $l) {
	`var_dump($l) die;`
`}`
Ao imprimir o resultado em um console: 'pão' pois como ele percorre cada item, no momento da chamada eu estou acessando o primeiro item

Agora se ao em vez de simplesmente usar o foreach as $l, eu usar o $key => $l
`foreach($lista as $key => $l) {`
	`if($key == 0){continue;}`
	`var_dump($key, $l);die;`
`}`
Agora além de percorrer o item eu também percorro a posição de cada item, o que o codigo acima faz:
eu fiz uma condição para ignorar o primeiro item da lista, como consequencia o item impresso no console seria: 1, 'presunto'
quando a condição for valida ele chama o **continue**, esse continue ignora o 0 e continua para o proximo item que no caso é o 1,2...


Outro exemplo usando o continue 2

Agora eu tenho outro array, e dentro desse array eu tenho outros arrays 
`$lista = [`
	`'bebidas' => ['suco', 'cafe', 'refrigerante'],`
	`'comidas' => ['pão', 'arroz', 'carne']`
	`];`

para acessar a $lista seria precisa fazer um foreach que me da acesso aos dois arrays que estão dentro dele, mas para acessar cada item da $lista e cada item dos arrays dentro da $lista eu preciso realizar outro foreach
`foreach($lista as $key => $l) {`
	`foreach($l as $item) {`
		`var_dump($item);die;`
	`}`
`}`