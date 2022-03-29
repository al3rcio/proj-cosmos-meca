# Cosmos - Máquina de criar imagens

Cosmos - Máquina de criar imagens é o projeto final do curso técnico em Mecatrônica do IFSUL-NH, desenvolvido no último semestre do curso, com data de início em dezembro de 2021. 

# Atualizando

Várias coisas mudaram, ainda não tive tempo de reorganizar as coisas por aqui, pra ficar tudo mais claro e preciso.
Num futuro breve, espero.

## Liberando pinos para uso

Esse [guia](https://www.inf.pucrs.br/emoreno/undergraduate/CC/progperif/class_files/Aula03/material/tutorial_gpio.pdf) da PUC-RS me ajudou a entender melhor como funcionam os pinos, no Linux, e como liberar eles, já que na configuração dos `pinMode()` o programa tava bloqueando o acesso. 

> Abaixo serão listados comandos que deverão ser usados em uma próxima etapa para fazer
acesso aos pinos de entrada e saída. Praticamente tudo no Linux é um “arquivo”. Isso inclui os
pinos de GPIO. Para habilitar o acesso a algum pino de GPIO, identifique isso para o sistema
escrevendo o número do pino no arquivo “/sys/class/gpio/export”. Por exemplo, para acessar o
pino 18:

`echo "18" > /sys/class/gpio/export`

Aí eu basicamente fui olhando meu esquemático de pinos e liberando cada um deles no terminal. Com o comando acima, ele criava a estrutura de pastas no sistema. Com esse próximo, ele liberava o uso:

`chmod -R 777 /sys/class/gpio/gpio18`

Claro, eu só ia trocando o 18 do exemplo pelos pinos que eu vou usar no projeto (que são meio que todos, mas logo vou colocar imagens do esquemático eletrônico e coisas afins). O pino GPIO-07, que faz parte do grupo dos SPI, foi o único que ainda não consegui liberar. Os outros pinos SPI tão sendo utilizados pro conversor AD ([MCP3008](https://github.com/processing/processing/tree/master/java/libraries/io/examples/AnalogDigital_SPI_MCP3008)), talvez tenha alguma relação por aí, preciso pesquisar ainda e tentar descobrir isso. No guia da PUC ensina também a configurar direção (IN, OUT), valor (0 ou 1) e outras coisas, mas isso tô fazendo pelo próprio Processing, por isso não comentei nada por aqui.

## A partir daqui coisas velhas que precisam ser atualizadas


## Instalando sistema no SD

~~Usei o sistema distribuído pelo site da Fundação Processing, 
que já vem com o Processing e Java 8 pré-instalados.
Tutorial disponível em: https://pi.processing.org/get-started/ | Acesso em 11/02/2022.

Baixar e instalar um programa chamado Etcher (monta a imagem do SO no SD)
~~Baixar a imagem disponibilizada Raspbian com Processing.

Agora que voltei a usar por Java, usei direto a versão mais atual disponível no site da Fundação Raspberry.

## Configurando Raspberry remotamente

Tutorial disponível em https://help.realvnc.com/hc/en-us/articles/360002249917-VNC-Connect-and-Raspberry-Pi#setting-up-your-raspberry-pi-0-0 | Acesso em 11/02/2022.

Na Raspberry, utilizando monitor, mouse e teclado, aperte Ctrl + alt + T para abrir o Terminal.

```
sudo apt-get update
sudo apt-get install realvnc-vnc-server
sudo apt-get update
```

Depois, rode o commando

```
sudo raspi-config
```

E navega até **Interfacing Options > VNC** e selecione **YES**

Após, digite `ifconfig` para descobrir o IP da Raspberry. 
O IP será usado para entrar pelo computador pessoal, utilizando o aplicativo VNC.

~~## Preparando pra rodar Processing em Python mode via CLI~~
Não rolou trabalhar com Python e Processing com a Raspberry, porque não funcionaram as bibliotecas de pinos nativas de Python, sendo compiladas e Java. Por isso tachei tudo, num futuro organizo melhor aqui. Mas voltei a usar o Java, pelo Vim Editor (então, as configurações, a maioria delas, acabam sendo úteis, pelo menos pro Vim)

~~Primeiro, por que rodar Processing via Python e não em Java?
Acredito que haja mais bibliotecas pra trabalhar com Raspberry e uma comunidade mais extensa, tanto em português quanto em inglês, pra ajudar nesse percurso.

~~E por que usar Linha de Comando (CLI) e VIM editor?
Trabalhando com a Raspberry 3, com 1gb de memória RAM, achei que o sistema ficou lento pra trabalhar rodando a IDE do Processing. Talvez isso não seja um problema em modelos mais recentes, com mais memória RAM. O VIM, apesar de uma curva de aprendizado extremamente difícil, conforme tu vai usando tu vai descobrindo facilidades incríveis e acaba agilizando a produção de código.

~~Ao processo: segui [este](https://py.processing.org/tutorials/command-line/) tutorial do site oficial da fundação Processing. A vantagem de ter usado no começo a imagem do OS feito pela Processing é que o Java já tava configurado com a versão correta pra funcionar o CLI. O único porém é que precisa de um arquivo, que tem o link no site, mas aparentemente o link não tava funcionando quando tentei acessar. Digitando direto na barra do navegador rolou de fazer o download: https://py.processing.org/processing.py-linux64.tgz - só baixar esse arquivo no Raspberry. Aí, pelo terminal dá pra navegar até a pasta, no meu caso

~~`cd ~/Downloads`

~~E usar o comando tar pra extrair o arquivo. 

~~`tar -xzvf NOME_DO_ARQUIVO.tgz -C /PASTA_DESEJADA`

~~Depois disso, é só salvar uma cópia do arquivo **processing-py.jar** (ele tá nessa pasta onde o arquivo tgz foi extraído) junto com a pasta de cada sketch escrito em Python. Pra copiar via terminal, de dentro da pasta onde o arquivo tá:

~~`cp processing-py.jar ~/CAMINHO/PASTA/DESEJADA`

~~Depois, quando quiser rodar a sketch, de dentro da pasta, no terminal, onde estão o arquivo .py e o **processing-py.jar** é só digitar:

~~`java -jar processing-py.jar NOME_SKETCH.py`

~~Voilà! [pelo menos por aqui a coisa tá funcionando! :]

## Transformando VIM em uma (entre aspas) IDE

Como a minha ideia aqui é rodar sobretudo programas escritos em Python, resolvi seguir esse tutorial [aqui](https://realpython.com/vim-and-python-a-match-made-in-heaven/).
Ele é bem autoexplicativo, mesmo sendo em inglês. 

Quando chegou na parte da instalação do YouCompleteMe, alguns problemas apareceram. A versão do VIM precisa ser 8.1+ e o Python 3.6+, ambas versões estavam desatualizadas no Pi. 
O Python precisou ser compilado ~na mão~. Segui as instruções dessesite [aqui](https://raspberrytips.com/install-latest-python-raspberry-pi/), e instalei a versão 3.9.5, com esses passos aqui:

```
wget https://www.python.org/ftp/python/3.9.5/Python-3.9.5.tgz
tar -zxvf Python-3.9.5.tgz
cd Python-3.9.5
./configure --enable-optimizations
sudo make altinstall
```

Ali na execução das confiurações leva um tempinho, e depois na instalação mesmo são mais vários minutos. Depois, vale a pena atualizar manualmente o uso dos aliases python e python3 pra versão mais recente.

```
cd /usr/bin
sudo rm python
sudo ln -s /usr/local/bin/python3.9 python
python --version
```

Aí tá descrito como fazer pra python, mas dá pra usar pro python3, só fazendo as respectivas mudanças.

Pra deixar o python configurado pro VIM, como `+python3` foi um certo perrengue. Tive que compilar *na mão* o VIM. Segui basicamente esse [site](https://en.dlyang.me/install-vim-on-raspberry-pi-with-python3-support/). Tive só que fazer as adaptações pra versão do Python que eu tinha instalado. Isso deu um pouco de trabalho, até entender exatamente em que pasta ele estaria. Nessas buscas, descobri o comando `python3.9-config` no meu caso, que deu as informações de diretório que eu precisava, ou pelo menos como acessar elas. O comando é no terminal, e pode ser usado pra versão que tiver instalada, só mudaro número depois de python. Depois, na hora de compilar, ou logo antes, na pasta `/vim/src` 

```
./configure --with-features=huge --enable-cscope --enable-multibyte \
  		--enable-rubyinterp --enable-pythoninterp --enable-python3interp \
		--with-python3-command=python \
                --with-python3-config-dir=/usr/local/lib/python3.9/config-3.9-arm-linux-gnueabihf \
```

<strike>Isso que funcionou pra mim! :) </strike>

Tive que recompilar a versão de python, com uma configuração adicional, a flag `--enable-shared`. No site da fundação Python tem uma [lista extensa](https://docs.python.org/3/using/configure.html) de configurações adicionais que dá pra usar na hora de compilar na mão.

```
./configure --enable-optimizations --enable-shared
```






