
Use o comando:

`php artisan make:migration add_nome_da_coluna_to_nome_da_tabela`

Abra o arquivo gerado em **`database/migrations/`** e dentro do método `up()`, adicione a nova coluna:

`use Illuminate\Database\Migrations\Migration;`
`use Illuminate\Database\Schema\Blueprint;`
`use Illuminate\Support\Facades\Schema;`

`return new class extends Migration {`
    `public function up(): void`
    `{`
        `Schema::table('users', function (Blueprint $table) {`
            `$table->string('status')->nullable(); // Adiciona uma nova coluna 'status'`
        `});`
    `}`

    `public function down(): void`
    `{`
        `Schema::table('users', function (Blueprint $table) {`
            `$table->dropColumn('status'); // Remove a coluna caso seja necessário reverter`
        `});`
    `}`
`};`

