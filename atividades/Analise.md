Atividade 01:
Sem sincronização As threads se atropelam: o consumidor às vezes age antes do produtor, há leituras repetidas (“Consumidor: 29” várias vezes) e a ordem é caótica.

Com sincronização A execução fica ordenada: o produtor gera e o consumidor consome na sequência correta, com menos repetições e sem corrida de threads.
A sincronização elimina o acesso simultâneo descontrolado e garante coerência entre produtor e consumidor.



atividade 02:
MeuDadoMonitorJava introduz controle de sincronização (monitor), o que evita o comportamento concorrente desordenado visto nos logs de MeuDadoThreadsJava. Em resumo, ele mostra um código corrigido e coordenado, enquanto os outros logs mostram threads atuando sem sincronização.

Atividade 03:

MeuDadoEventJava mostra um sistema sincronizado por eventos, eficiente, sem travamentos e com execução fluida entre produtor e consumidor — uma evolução clara em relação aos modelos anteriores.