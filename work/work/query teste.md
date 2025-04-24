

`private function _getItem($selected_agents, $initial_date, $final_date, $agent): object`  
`{`  
    `$name = AppUtil::convertDateToMonthAndYear($initial_date);`  
  
    `if(!AppUtil::isEmpty($agent->usuario->equipe_usuario) && $agent->usuario->equipe_usuario[0]->equipe_id == PageUtil::getConfig('equipe_leader_farmer')) {`  
        `$comission_agent = ComissaoFechamentoRepository::getComissaoByAgenciador($selected_agents, $initial_date, $final_date);`  
    `} else {`  
        `$comission_agent = ComissaoFechamentoRepository::getComissaoByAgenciador2($selected_agents, $initial_date, $final_date);`  
    `}`  
  
    `$comission_agent_data = ComissaoFechamentoItemRepository::getFechamentoUsuarioData($agent->usuario, $initial_date, $final_date);`  
    `$enrolments = ComissaoFechamentoRepository::getVendasByAgenciadorMes($selected_agents, $initial_date, $final_date);`  
  
  
    `$managed_agents = Agenciador::getAgenciadoresGerenciados($agent, Agenciador::AMBIENTE_LOCAL);`  
    `$managed_agents_remote = Agenciador::getAgenciadoresGerenciados($agent,Agenciador::AMBIENTE_REMOTO);`  
  
    `$user_group_leader_id = $agent->usuario->usuario_perfil_id == PageUtil::getConfig('usuario_perfil_lider');`  
  
    `if(!empty($managed_agents)) {`  
        `$close_agents = AgenciadorRepository::getFechamentoUsuario($managed_agents, $initial_date, $final_date, $user_group_leader_id);`  
    `}`  
  
    `if(!empty($managed_agents_remote)) {`  
        `$remote_close_agents = self::_getFechamentoRemoto($managed_agents_remote, $initial_date, $final_date);`  
        `if(!AppUtil::isEmpty($remote_close_agents->matriculas ?? null)) {`  
            `$enrolments = array_merge($enrolments->toArray(), $remote_close_agents->matriculas);`  
        `}`  
    `}`  
  
    `$student_quantity = 0;`  
    `$enrolments_quantity = 0;`  
    `$billing_value = 0;`  
    `$billing_value_fees = 0;`  
    `foreach ($comission_agent as $comissions_agent_item) {`  
        `$student_quantity += $comissions_agent_item->aluno_quantidade;`  
        `$enrolments_quantity += $comissions_agent_item->matricula_quantidade;`  
        `$billing_value += $comissions_agent_item->faturamento_valor;`  
        `$billing_value_fees += $comissions_agent_item->faturamento_valor_taxas;`  
    `}`  
  
    `if(!empty($remote_close_agents->list_comissao_agenciador)) {`  
        `foreach ($remote_close_agents->list_comissao_agenciador as $managed_agents_remote_item) {`  
            `$student_quantity += $managed_agents_remote_item->aluno_quantidade;`  
            `$enrolments_quantity += $managed_agents_remote_item->matricula_quantidade;`  
            `$billing_value += $managed_agents_remote_item->faturamento_valor;`  
            `$billing_value_fees += $managed_agents_remote_item->faturamento_valor_taxas;`  
        `}`  
    `}`  
  
    `$meta_sales_agent = AgenciadorMeta::where('data_referencia', '=', AppUtil::getDateToMonthAndYear($initial_date))`  
        `->where('agenciador_id', '=', $agent->id)`  
        `->first();`  
  
    `$commission_value = 0;`  
    `if($agent->usuario->usuario_perfil_id == PageUtil::getConfig('usuario_perfil_consultor')) {`  
        `$commission_table = Auth::user()->comissao_tabela_usuario->comissao_tabela ?? null;`  
        `$commission_value = ComissaoTabela::getComissaoByMatriculaAndFaturamento($commission_table, $enrolments_quantity, $billing_value);`  
  
        `$commission_value = $commission_value->total_valor;`  
    `}`  
  
    `return (object) array (`  
        `'name' => $name,`  
        `'date' => $initial_date,`  
        `'date_final' => $final_date,`  
        `'student_quantity' => $student_quantity,`  
        `'meta_enrolment' => $meta_sales_agent->meta_matricula ?? '-1',`  
        `'enrolments_quantity' => $enrolments_quantity,`  
        `'billing_value' => AppUtil::convertFloatToString($billing_value, '.', '0,00'),`  
        `'ticket_average' => $enrolments_quantity > 0 ? AppUtil::convertFloatToString($billing_value_fees/$enrolments_quantity, '.', '0,00') : "0,00",`  
        `'commission_value' => AppUtil::convertFloatToString($commission_value, '.', '0,00'),`  
        `'closing' => !empty($comission_agent_data->toArray()),`  
        `'enrolments' => $enrolments ?? [],`  
        `'close_agents' => $close_agents ?? [],`  
        `'user_profile' => $agent->usuario->usuario_perfil_id,`  
        `'user_team' => $meta_sales_agent->equipe_id ?? null,`  
    `);`  
`}`