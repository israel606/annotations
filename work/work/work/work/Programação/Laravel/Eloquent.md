#work

having( )

**Exemplo simples**: Imagine que você tem uma tabela de vendas e quer saber quais produtos foram vendidos **exatamente uma vez**. Você faz uma contagem de quantas vezes cada produto foi vendido e depois usa o `having()` para pegar só os produtos que foram vendidos 1 vez.

`SELECT produto_id, COUNT(*) 
`FROM vendas` 
`GROUP BY produto_id` 
`HAVING COUNT(produto_id) = 1;`

Isso faz:
- Conta quantas vendas cada produto teve (`COUNT(produto_id)`).
- Depois filtra para mostrar **só os produtos que foram vendidos 1 vez** (usando o `having`).

No caso do seu exemplo, `having('count(ac.id) = 1')` quer dizer: "Mostre só os aluno_curso que tem somente um curso.


Pluck("alguma_coisa")

$course_area = Curso::whereIn('id', $ids_cousers_array)  
    ->groupBy('curso.curso_area_id')  
    ->pluck('curso_area_id');

apos obeter um resultado esse resultado se ele estivesse somente com o groupBy ele iria retornar uma resposta complexa com varios arrays que contem outras informações além da do curso
	ao utilizar o pluck ele extrai somente os id's que eu preciso em um array simples ou seja tira todo o "lixo" que veio junto na consulta e manda somente o id's necessarios



->groupBy("aluma_coisa")

Agrupa os registros do banco de dados com base no valor de uma ou mais colunas.
Se eu to fazendo uma consulta de quantos cursos um aluno possui, e varios alunos possuem mais de um curso, sendo assim esses alunos que possuem mais de um curso seriam contados mais de uma vez, sendo assim podemos usar o groupBy para agrupar os alunos que possuem mais de um registro e eles não seriam contados mais de uma vez.