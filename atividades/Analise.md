Atividade 01:
Sem sincronização As threads se atropelam: o consumidor às vezes age antes do produtor, há leituras repetidas (“Consumidor: 29” várias vezes) e a ordem é caótica.

Com sincronização A execução fica ordenada: o produtor gera e o consumidor consome na sequência correta, com menos repetições e sem corrida de threads.
A sincronização elimina o acesso simultâneo descontrolado e garante coerência entre produtor e consumidor.