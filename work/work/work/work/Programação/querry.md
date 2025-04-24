#work 

select * from aluno  
inner join usuario on aluno.usuario_id = [usuario.id](http://usuario.id)  
where aluno.cpf = 10018645658;


select * from aluno as a  
inner join usuario as u on a.usuario_id = [u.id](http://u.id)  
where a.cpf = 10018645658;


select * from aluno a  
inner join usuario u on a.usuario_id = [u.id](http://u.id)  
where a. cpf = 10018645658;