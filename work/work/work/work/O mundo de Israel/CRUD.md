
Route::get('nome-da-rota', [NomeDaController::class, 'index']); // Listar todos 
Route::post('nome-da-rota', [NomeDaController::class, 'store']); // Criar um novo 
Route::get('nome-da-rota/{id}', [NomeDaController::class, 'show']); // Exibir um específico Route::put('nome-da-rota/{id}', [NomeDaController::class, 'update']); // Atualizar  Route::delete('nome-da-rota/{id}', [NomeDaController::class, 'destroy']); // Deletar 