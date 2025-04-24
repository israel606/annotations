
Dbvear
vscode
php storm
anydesk
chrome 
opera GX
Obsidian
Xampp
ferramenta de captura
postman









`$ref = Lancamento::on('mysql_outra_base')`  
        `->whereBetween('pagamento_data', [$start_date, $end_date])`  
        `->groupBy('pagamento_data')`  
        `->leftJoinSub()`  
        `->get();`  
  
    `$ti = Lancamento::select(`  
            `DB::raw('date_format(lancamento.pagamento_data, "%Y-%m-%d") as referencia'),`  
`DB::raw('sum(lancamento.pagamento_valor) as taxa_inscricao'),`  
`DB::raw('count(lancamento.pagamento_valor) as taxa_inscricao_qtd'),`  
        `)`  
        `->join('plano_de_contas', 'plano_de_contas.id', '=', 'lancamento.plano_de_contas_id')`  
        `->leftJoin('venda', 'venda.id', '=', 'lancamento.venda_id')`  
        `->whereBetween('pagamento_data', [$start_date, $end_date])`  
        `->whereNotNull(['lancamento.pagamento_data'])`  
        `->whereIn('plano_de_contas.id', [PlanoDeContas::TAXA_INSCRICAO])`  
        `->where('lancamento.status', '!=', Lancamento::EXCLUIDO)`  
        `->groupBy('lancamento.pagamento_data')`  
        `->get();`  
  
    `$m = Lancamento::select(`  
        `DB::raw('date_format(lancamento.pagamento_data, "%Y-%m-%d") as referencia'),`  
        `DB::raw('sum(lancamento.pagamento_valor) as mensalidade'),`  
        `DB::raw('count(lancamento.pagamento_valor) as mensalidade_qtd'),`  
    `)`  
        `->join('plano_de_contas', 'plano_de_contas.id', '=', 'lancamento.plano_de_contas_id')`  
        `->leftJoin('venda', 'venda.id', '=', 'lancamento.venda_id')`  
        `->whereBetween('venda.data_venda', [$start_date, $end_date])`  
        `->whereBetween('pagamento_data', [$start_date, $end_date])`  
        `->whereNotNull(['lancamento.pagamento_data'])`  
        `->whereIn('plano_de_contas.id', [PlanoDeContas::MENSALIDADE])`  
        `->where('lancamento.status', '!=', Lancamento::EXCLUIDO)`  
        `->groupBy('lancamento.pagamento_data')`  
        `->get();`  
  
    `$c = Lancamento::select(`  
        `DB::raw('date_format(lancamento.pagamento_data, "%Y-%m-%d") as referencia'),`  
        `DB::raw('sum(lancamento.pagamento_valor) as mensalidade'),`  
        `DB::raw('count(lancamento.pagamento_valor) as mensalidade_qtd'),`  
    `)`  
        `->join('plano_de_contas', 'plano_de_contas.id', '=', 'lancamento.plano_de_contas_id')`  
        `->leftJoin('venda', 'venda.id', '=', 'lancamento.venda_id')`  
        `->whereBetween('pagamento_data', [$start_date, $end_date])`  
        `->whereNotNull(['lancamento.pagamento_data'])`  
        `->whereIn('plano_de_contas.id', [`  
            `PageUtil::getConfig('plano_de_contas_acordo_negociacao'),`  
            `PageUtil::getConfig('plano_de_contas_acordo_carencia'),`  
            `PageUtil::getConfig('plano_de_contas_acordo_antecipacao'),`  
        `])`  
        `->groupBy('lancamento.pagamento_data')`  
        `->get();`  
  
    `$r = Lancamento::select(`  
        `DB::raw('date_format(venda.data_venda, "%Y-%m-%d") as referencia'),`  
        `DB::raw('sum(lancamento.vencimento_valor) as recorrencia'),`  
        `DB::raw('count(lancamento.vencimento_valor) as recorrencia_qtd'),`  
    `)`  
        `->join('plano_de_contas', 'plano_de_contas.id', '=', 'lancamento.plano_de_contas_id')`  
        `->leftJoin('venda', 'venda.id', '=', 'lancamento.venda_id')`  
        `->whereBetween('venda.data_venda', [$start_date, $end_date])`  
        `->whereNull(['lancamento.pagamento_data'])`  
        `->whereIn('plano_de_contas.id', [PlanoDeContas::MENSALIDADE])`  
        `->where('lancamento.status', '!=', Lancamento::EXCLUIDO)`  
        `->groupBy('venda.data_venda')`  
        `->get();`  
  
    `$g = Lancamento::select(`  
        `DB::raw('date_format(lancamento.vencimento_data, "%Y-%m-%d") as referencia'),`  
        `DB::raw('sum(lancamento.vencimento_valor) as gerado_geral '),`  
        `DB::raw('count(lancamento.vencimento_valor) as gerado_geral_qtd'),`  
    `)`  
        `->join('plano_de_contas', 'plano_de_contas.id', '=', 'lancamento.plano_de_contas_id')`  
        `->whereBetween('lancamento.vencimento_data', [$start_date, $end_date])`  
        `->whereNull(['lancamento.pagamento_data'])`  
        `->where('lancamento.status', '!=', Lancamento::EXCLUIDO)`  
        `->groupBy('lancamento.vencimento_data')`  
        `->get();`  
  
    `$p = Lancamento::select(`  
        `DB::raw('date_format(lancamento.pagamento_data, "%Y-%m-%d") as referencia'),`  
        `DB::raw('sum(lancamento.vencimento_valor) as pago_geral '),`  
        `DB::raw('count(lancamento.vencimento_valor) as pago_geral_qtd'),`  
    `)`  
        `->join('plano_de_contas', 'plano_de_contas.id', '=', 'lancamento.plano_de_contas_id')`  
        `->whereBetween('lancamento.pagamento_data', [$start_date, $end_date])`  
        `->whereNotNull(['lancamento.pagamento_data'])`  
        `->where('lancamento.status', '!=', Lancamento::EXCLUIDO)`  
        `->groupBy('lancamento.pagamento_data')`  
        `->get();`