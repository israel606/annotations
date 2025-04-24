

### **`route()`**

- **Uso**: Gerar URLs para rotas nomeadas.
- **Exemplo**:
    
    php
    
    Copiar
    
    `$url = route('user.profile', ['id' => 1]);`
    
- **Por que usar**: Facilita a criação de URLs, especialmente quando você tem rotas nomeadas. Isso torna o código mais limpo e fácil de manter.

### 2. **`redirect()`**

- **Uso**: Realizar redirecionamentos para outras páginas.
- **Exemplo**:
    
    php
    
    Copiar
    
    `return redirect()->route('home');`
    
- **Por que usar**: Facilita o fluxo de navegação do usuário, redirecionando para outras páginas da aplicação.

### 3. **`view()`**

- **Uso**: Retornar uma view (página HTML) para o navegador.
- **Exemplo**:
    
    php
    
    Copiar
    
    `return view('welcome', ['name' => 'John']);`
    
- **Por que usar**: Um dos pilares do Laravel para gerar respostas HTTP em forma de HTML. Usado para renderizar as views com dados passados do controlador.

### 4. **`response()`**

- **Uso**: Criar respostas HTTP personalizadas, incluindo retornos JSON, headers, etc.
- **Exemplo**:
    
    php
    
    Copiar
    
    `return response()->json(['message' => 'Success']);`
    
- **Por que usar**: Ideal para APIs, onde você precisa responder com dados no formato JSON, ou quando precisa personalizar o código de status, cabeçalhos, etc.

### 5. **`Storage::disk()`**

- **Uso**: Interagir com sistemas de arquivos (local, S3, Azure, etc.).
- **Exemplo**:
    
    php
    
    Copiar
    
    `Storage::disk('s3')->put('file.txt', 'Conteúdo do arquivo');`
    
- **Por que usar**: Laravel fornece uma camada de abstração para trabalhar com diferentes sistemas de armazenamento de maneira uniforme. Isso facilita o gerenciamento de arquivos, seja local ou em nuvem.

### 6. **`DB::table()`**

- **Uso**: Consultar diretamente o banco de dados usando a Query Builder.
- **Exemplo**:
    
    php
    
    Copiar
    
    `$users = DB::table('users')->get();`
    
- **Por que usar**: Quando você não precisa de um modelo Eloquent completo, mas ainda precisa interagir com o banco de dados de forma fluida e eficiente.

### 7. **`Model::create()`**

- **Uso**: Criar registros no banco de dados usando Eloquent.
- **Exemplo**:
    
    php
    
    Copiar
    
    `User::create(['name' => 'John', 'email' => 'john@example.com']);`
    
- **Por que usar**: Eloquent é a ORM (Object-Relational Mapping) do Laravel e facilita a interação com o banco de dados de forma orientada a objetos, tornando o código mais limpo e expressivo.

### 8. **`$request->input()` / `request()`**

- **Uso**: Recuperar dados da requisição HTTP (dados do formulário, parâmetros, etc.).
- **Exemplo**:
    
    php
    
    Copiar
    
    `$name = $request->input('name');`
    
    ou
    
    php
    
    Copiar
    
    `$name = request('name');`
    
- **Por que usar**: Essencial para acessar dados que vêm de formulários ou da URL na requisição HTTP.

### 9. **`session()`**

- **Uso**: Trabalhar com sessões de usuário.
- **Exemplo**:
    
    php
    
    Copiar
    
    `session(['key' => 'value']); $value = session('key');`
    
- **Por que usar**: Permite armazenar dados temporários entre requisições, como informações de login, preferências do usuário, mensagens flash, etc.

### 10. **`validate()`**

- **Uso**: Validar dados de entrada em requests.
- **Exemplo**:
    
    php
    
    Copiar
    
    `$request->validate([     'email' => 'required|email',     'password' => 'required|min:6', ]);`
    
- **Por que usar**: Valida dados de forma simples e eficaz, com mensagens de erro personalizáveis. Isso ajuda a garantir que os dados recebidos de formulários sejam corretos.

### 11. **`abort()`**

- **Uso**: Interromper a execução e retornar um código de erro HTTP (geralmente usado para erros de autorização ou quando a página não existe).
- **Exemplo**:
    
    php
    
    Copiar
    
    `abort(404);`
    
- **Por que usar**: Uma maneira rápida de retornar erros HTTP personalizados, como 404 (não encontrado) ou 403 (proibido).

### 12. **`dispatch()`**

- **Uso**: Enviar um job para a fila de trabalho (assíncrono).
- **Exemplo**:
    
    php
    
    Copiar
    
    `ProcessVideo::dispatch($video);`
    
- **Por que usar**: Para processos demorados (como o upload de arquivos, processamento de vídeos, etc.), onde você deseja que o trabalho seja feito em segundo plano sem bloquear a execução da aplicação.

### 13. **`event()`**

- **Uso**: Disparar eventos.
- **Exemplo**:
    
    php
    
    Copiar
    
    `event(new UserRegistered($user));`
    
- **Por que usar**: Laravel permite que você crie um fluxo de eventos para a aplicação, onde você pode reagir a certas ações, como o registro de um novo usuário, sem misturar toda a lógica no mesmo lugar.

### 14. **`auth()`**

- **Uso**: Gerenciar autenticação de usuários.
- **Exemplo**:
    
    php
    
    Copiar
    
    `$user = auth()->user();`
    
- **Por que usar**: Permite verificar o status de autenticação, obter o usuário autenticado, ou realizar login/logout de forma simples.

### 15. **`Cache::get()` / `Cache::put()`**

- **Uso**: Trabalhar com o cache para otimizar a performance da aplicação.
- **Exemplo**:
    
    php
    
    Copiar
    
    `Cache::put('key', 'value', 600);  // Armazenar no cache por 10 minutos $value = Cache::get('key');`
    
- **Por que usar**: Usar o cache ajuda a reduzir o tempo de resposta de sua aplicação e minimizar chamadas repetitivas ao banco de dados ou a sistemas externos.

### 16. **`collect()`**

- **Uso**: Trabalhar com coleções de dados (geralmente usados quando você tem arrays de dados).
- **Exemplo**:
    
    php
    
    Copiar
    
    `$collection = collect([1, 2, 3]); $filtered = $collection->filter(fn($item) => $item > 1);`
    
- **Por que usar**: A classe `Collection` oferece métodos poderosos para manipulação de arrays de maneira fluida e mais legível.