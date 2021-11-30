# SistemasEmbarcados

## Lab 1
O resultado do programa HelloWorld deve aparecer no terminal I/O. Para visualizar esse terminal, o programa deve estar em modo debug.

## Lab 2
Variáveis volatile:
Essas variáveis são declaradas assim para sinalizar ao compilador que ele não deve otimizar nada relacionado a essa variável, para facilitar o acesso a hardware, mapeamento de memória de I/O e uso de threads.

## Lab 5
![tabela 2](https://user-images.githubusercontent.com/49958403/142776783-88bc68ae-6f9c-4ad3-9752-850ffa53fa32.png)

![tabela 1](https://user-images.githubusercontent.com/49958403/142777095-51775021-5020-47d7-9cdb-4bc6c737fd0c.png)

![diagrama](https://user-images.githubusercontent.com/49958403/142777681-886f950a-45c7-4c5a-b909-6a81180b15f5.png)


## Lab 6

O tempo de execução do loop medido com cronometro (opção 3) foi de aproximadamente 1.6us. Essa medida foi feita rodando o loop 10 milhões de vezes e constatando que esse processo levou 16 segundos. 

### Métodos de escalonamento:

* Escalonamento por time-slice de 50 ms. Todas as tarefas com mesma prioridade.

O time slice significa que as threads alternam entre si a cada 50 ms, se estão prontas para executar. Caso só uma thread esteja pronta, esta executa sem interrupções. O efeito disso são os leds piscando alternadamente de maneira rápida.

* Escalonamento sem time-slice e sem preempção. Prioridades estabelecidas no passo 3. A preempção pode ser evitada com o “preemption threshold” do ThreadX.

Nesse caso, como as threads não são interrompidas por conta desabilitação da preempção, então prioridade maior não significa que a thread será executada assim que pronta, e sim dependendo da liberação do processador. Nesse modo, o efeito visto é que o leds piscam alternadamente entre si, mas não se interrompem, só começam a piscar quando o anterior parou.

* Escalonamento preemptivo por prioridade.

Aqui, as 3 threads podem se interromper. Leds com maior prioridade podem interromper a execução de outros. Após a interrupção, o led anterior volta a piscar. Isso causa um efeito visual meio imprevisível, já que as interrupçoes fazem os leds altenarem rapidamente. 

* Implemente um Mutex compartilhado entre T1 e T3. No início de cada job estas tarefas devem solicitar este mutex e liberá-lo no final. Use mutex sem herança de prioridade. Observe o efeito na temporização das tarefas.

Os períodos das 3 threads podem ser alterados por conta do mutex. Isso faz com que os leds alternem entre si, e  o tempo entre um led desligar e outro ligar é tambem variável.

* Idem acima, mas com herança de prioridade.

Idem ao caso acima, porém T2 pode aumentar seu período caso T3 esteja executando, pela herança de prioridade do mutex. O efeito visual é muito parecido.
