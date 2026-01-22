Para esse teste, fiz a alteração da arquitetura do modelo, ao inves da camada de encoder e decoder terem valores diferentes, o modelo passou a ser simetrico onde a camada de decoder tem os mesmos valores que a de encoder.
Usando uma seed fixa 42.
Os parametros ajustados foram:
- learning_rate
- n_layers (o mesmo para encoder_n_layers e decoder_layers)
- hidden_size_comum (o mesmo para encoder_hidden_size e decoder_hidden_size)
- dropout

No caso do dropout, se o valor de n_layers_comum for igual a 1 não faz sentido usar dropout pois não existe uma "próxima camada" para inserir o Dropout antes dela, então nesses casos o dropout é 0.0. 
Por conta disso no json salvo com os valores dos parametros ajutados, se n_layers_comum o valor de dropout nem aparece (por isso o param_base usa dropout como 0.0 para ser usado nesses casos).

Nessa versão também foi removido o uso da transformação logarítmica, pois com ela seria como se etive fazendo duas transformações ao mesmo tempo (transformação logarítmica e hevin).

Outra mudança foi a alteração do calculo do erro para os dados de validação, onde ao inves de ser o erro com base na produtividade, o erro foi ponderado pela area de produção, assim o modelo era treinado para perceber a produtividade e aprender com o clima e penalizado com base na produção para ter um ajuste melhor em produtores mais relevantes.