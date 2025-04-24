#work


# Pegar ultimo dia do mês anterior

`$date_initial = AppUtil::getCurrentDate('Y-m-01');`  
  
`$date_initial = AppUtil::addMonthsInDate('-1', $date_initial);`

`$date_final = Carbon::parse($date_initial)->format('Y-m-t');`

`date($format)`: Formata uma data/hora loca

	echo date("Y-m-d H:i:s"); // Saída: Data e hora atual no formato "2023-01-01 12:34:56"

`strtotime($time): Converte uma string de data/hora para um timestamp Unix`
	
	echo strtotime("next Monday"); // Saída: Timestamp Unix para a próxima segunda-feira





