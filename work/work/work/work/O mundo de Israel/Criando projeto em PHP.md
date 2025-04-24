
Quando seguir a documentação do laravel ele solicita a installação de alguns comandos, mas quando for rodar o **`laravel new nome-do-projeto`** se caso ele não der certo, é preciso procurar o caminho que ele foi instalado como por exmplo:

`C:\Users\GFE-2649\AppData\Roaming\Composer\vendor\bin\laravel` 

Se ele estiver lá e ainda sim o comando **laravel new** não executar ai é preciso rodar o comando: 

`C:\\Users\\GFE-2649\\AppData\\Roaming\\Composer\\vendor\\bin\\laravel new nome-do-projeto`

Meio que aqui a gente passar o caminho para que o comando seja reconhecido, mas o correto é adicionar o caminho nas variaveis de ambiente do windows

------------

**composer create-project laravel/laravel nome-do-projeto**


