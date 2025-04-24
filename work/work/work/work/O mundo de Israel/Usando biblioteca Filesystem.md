


**`$file->store('temp', 'local')`**: Aqui, você está pedindo ao Laravel para salvar o arquivo. O método `store` faz exatamente isso. Ele pega o arquivo e o move para um diretório dentro do seu servidor. No caso:

- **'temp'**: É o nome da pasta onde o arquivo será salvo.
- **'local'**: Refere-se ao tipo de "disco" onde o arquivo será armazenado. O Laravel tem vários tipos de "discos", como `local` (onde fica o armazenamento no servidor), `public` (para tornar o arquivo acessível via URL), etc. No seu caso, o `local` significa que o arquivo será salvo no servidor em uma pasta dentro de `storage/app/temp`.

O Laravel vai gerar um nome único para o arquivo, para evitar conflitos com outros arquivos (se dois usuários enviarem um arquivo com o mesmo nome, por exemplo).

----------------

**`Storage::disk('local')->delete($this->filePath)`**: Após o processamento do arquivo, você provavelmente não precisa mais dele, então você pode **removê-lo**.

- **`Storage::disk('local')`**: Diz ao Laravel para procurar o arquivo no disco `local`, ou seja, dentro de `storage/app` (onde você armazenou o arquivo anteriormente).
- **`$this->filePath`**: Esse é o caminho do arquivo que você passou para o job. Quando o job foi chamado, o caminho do arquivo foi enviado para ele.
- **`delete($this->filePath)`**: Isso deleta o arquivo do servidor, removendo-o permanentemente de `storage/app/temp`.

Portanto, após o processamento, o arquivo é excluído para não ocupar mais espaço desnecessário.

--------------

Os arquivos ficam armazenados em `storage/app/temp/{nome_do_arquivo}`

----------------
// Recupera o arquivo
    $file = $request->file('file');

    // Gerando um nome único para o arquivo com base em um hash
    $uniqueName = Str::random(40) . '.' . $file->getClientOriginalExtension();

    // Salva o arquivo com o nome único no diretório 'temp' no disco local
    $path = $file->storeAs('temp', $uniqueName, 'local'); 

    // Retorna o caminho onde o arquivo foi armazenado
    return $path;

**`Str::random(40)`**: Gera uma string aleatória de 40 caracteres usando caracteres alfanuméricos. Isso é útil para garantir que o nome do arquivo seja único e difícil de prever. Por exemplo, isso pode gerar algo como **`c8d7f99ac7e6d96d098f61b2a378a3f0ad7b4a9c4d26c5d8`**.

**`$file->getClientOriginalExtension()`**: Esse método pega a **extensão original do arquivo** (por exemplo, **`jpg`**, **`png`**, **`pdf`**, etc.) com base no arquivo enviado.
- - **Por que isso é importante?** Você precisa manter a **extensão do arquivo** para garantir que ele possa ser aberto ou processado corretamente.
- O código então concatena o **hash aleatório** gerado com a **extensão** do arquivo, formando um nome único para o arquivo. Por exemplo, se o arquivo for uma imagem JPEG, o nome poderia ser algo como **`c8d7f99ac7e6d96d098f61b2a378a3f0ad7b4a9c4d26c5d8.jpg`**.

- **`$file->storeAs('temp', $uniqueName, 'local')`**: Aqui, o método **`storeAs()`** é usado para salvar o arquivo com o nome único gerado no diretório **`temp`**.
    - O primeiro parâmetro **`'temp'`** é o nome do diretório onde o arquivo será armazenado dentro da pasta de armazenamento configurada no Laravel.
    - O segundo parâmetro **`$uniqueName`** é o nome que o arquivo terá quando for salvo (o nome único gerado na etapa anterior).
    - O terceiro parâmetro **`'local'`** especifica que o arquivo deve ser armazenado no disco **`local`**, que corresponde ao diretório **`storage/app`**.
- **Resultado**: O arquivo é movido para o diretório **`storage/app/temp`** no seu sistema de arquivos local com o nome gerado. O caminho completo para o arquivo é armazenado na variável **`$path`**.
-----------


Usando store para salvar aquivos do request

`$file = $request->file('image'); // Obtém o arquivo enviado no request 
`$path =$file->store('public/uploads'); // Armazena o arquivo em storage/app/public/uploads`

`$file = $request->file('image');` → Obtém o arquivo enviado pelo usuário via formulário (`<input type="file" name="image">`) Se um dia precisar de frontend ele recebe por formulario.

`$path = $file->store('public/uploads');` → Salva o arquivo na pasta `storage/app/public/uploads` e retorna o caminho do arquivo.

-----------
Usando o put 

`Storage::put('public/texto.txt', 'arquivo de teste')`;

Cria um arquivo chamado `texto.txt` dentro de `storage/app/public/`.
 Insere o conteúdo `"Este é um arquivo de teste."` dentro do arquivo.


**Diferença entre `store` e `put`:**

- `store()` é usado para **arquivos enviados pelo usuário**.
- `put()` é usado para **criar arquivos e armazenar conteúdo manualmente**.

---------------------

get 

`$conteudo = Storage::get('public/texto.txt'); 
`echo $conteudo;`

- `Storage::get('public/texto.txt');` → Lê o conteúdo do arquivo `texto.txt` dentro de `storage/app/public/`.
- `echo $conteudo;` → Exibe o conteúdo do arquivo na tela.

verificando se existe
`if (Storage::exists('public/texto.txt')) {`
	  `echo "O arquivo existe!";` 
  `} else` 
    `{` 
	    `echo "Arquivo não encontrado!";` 
    `}`

--------------

delete arquivo

`Storage::delete('public/texto.txt');` 
`echo "Arquivo deletado!";`

--------------

listando files

`$arquivos = Storage::files('public/uploads');`

`foreach ($arquivos as $arquivo) {`
    `echo $arquivo . "<br>";`
`}`

1. `Storage::files('public/uploads');` → Retorna um array com os nomes dos arquivos dentro da pasta `storage/app/public/uploads/`.
2. `foreach ($arquivos as $arquivo)` → Percorre cada arquivo encontrado.
3. `echo $arquivo . "<br>";` → Exibe o nome do arquivo na tela, quebrando a linha.

 Para listar diretórios, use `directories()`. -> pesquisar sobre isso

--------------

Criando e excluindo diretorios 

`Storage::makeDirectory('public/novapasta');`

`Storage::makeDirectory('public/novapasta'); → Cria uma pasta chamada novapasta dentro de storage/app/public/.`


`Storage::deleteDirectory('public/novapasta');`
`Storage::deleteDirectory('public/novapasta'); → Remove a pasta novapasta e todos os arquivos dentro dela.`


-----

Baixando um arquivo 

`return Storage::download('public/uploads/exemplo.pdf');`

`Storage::download('public/uploads/exemplo.pdf');` → Faz o navegador baixar o arquivo `exemplo.pdf`.


----------
Manipulando String

`$slug = Str::slug('Meu exemplo!', '-');` 
`dd($slug); // "meu-exemplo"`


`$result = Str::endsWith('arquivo.txt', '.txt');` 
`dd($result); // true`


-------------

Acessar link

http://localhost:8002/storage/famart/contracts/accept_term/103230/4B6rWIkNaJHAUDY8.FfCF9HfIthtVybQluXmDWi9QdTE5SitweVduWEl6MlNFUnN4RC85TGN0TThIMmM4S0hhWGJpb29OczJnTVdiZSs2SkRsQ1hiRk9xWng3Nys=.png

php artisan storage:link -> para gerar os links 

php artisan storage:unlink -> para destruir os links gerados






