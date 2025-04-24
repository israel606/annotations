
php artisan make:test TesteDeEndPoints ->para criar um teste

vendor/bin/phpunit --version -> olhar a versão do phpUnit

php artisan test tests/Feature/NarutoMissaoTest.php -> para rodar um unico teste

php artisan make:test Services/MeuServicoTest -> criar um teste dentro de um diretorio

php artisan make:test CommissionTest --feature ->para criar um test em feature
php artisan make:test CommissionTest --unit

php artisan test --testsuite=Feature ->para rodar todos os testes da pasta Feature


https://www.devmedia.com.br/teste-unitario-com-phpunit/41231 -> configurações sobre os testes

Documents -> https://docs.phpunit.de/en/12.0/ | https://github.com/sebastianbergmann/phpunit-documentation-brazilian-portuguese/blob/main/src/assertions.rst


olhar os videos da nota [[Punit]]