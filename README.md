# Cosmos - Máquina de criar imagens

Cosmos - Máquina de criar imagens é o projeto final do curso técnico em Mecatrônica do IFSUL-NH, desenvolvido no último semestre do curso, com data de início em dezembro de 2021. 


## Instalando sistema no SD

Usei o sistema distribuído pelo site da Fundação Processing, 
que já vem com o Processing e Java 8 pré-instalados.
Tutorial disponível em: https://pi.processing.org/get-started/ | Acesso em 11/02/2022.

Baixar e instalar um programa chamado Etcher (monta a imagem do SO no SD)
Baixar a imagem disponibilizada Raspbian com Processing.

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

## Preparando pra rodar Processing em Python mode via CLI

Primeiro, por que rodar Processing via Python e não em Java?
Acredito que haja mais bibliotecas pra trabalhar com Raspberry e uma comunidade mais extensa, tanto em português quanto em inglês, pra ajudar nesse percurso.

E por que usar Linha de Comando (CLI) e VIM editor?
Trabalhando com a Raspberry 3, com 1gb de memória RAM, achei que o sistema ficou lento pra trabalhar rodando a IDE do Processing. Talvez isso não seja um problema em modelos mais recentes, com mais memória RAM. O VIM, apesar de uma curva de aprendizado extremamente difícil, conforme tu vai usando tu vai descobrindo facilidades incríveis e acaba agilizando a produção de código.

Ao processo: segui [este](https://py.processing.org/tutorials/command-line/) tutorial do site oficial da fundação Processing. A vantagem de ter usado no começo a imagem do OS feito pela Processing é que o Java já tava configurado com a versão correta pra funcionar o CLI. O único porém é que precisa de um arquivo, que tem o link no site, mas aparentemente o link não tava funcionando quando tentei acessar. Digitando direto na barra do navegador rolou de fazer o download: https://py.processing.org/processing;py-linux64.tgz - só baixar esse arquivo no Raspberry. Aí, pelo terminal dá pra navegar até a pasta, no meu caso

`cd ~/Downloads`

E usar o comando tar pra extrair o arquivo. 

`tar -xzvf NOME_DO_ARQUIVO.tgz -C /PASTA_DESEJADA`

Depois disso, é só salvar uma cópia do arquivo **processing-py.jar** (ele tá nessa pasta onde o arquivo tgz foi extraído) junto com a pasta de cada sketch escrito em Python. Pra copiar via terminal, de dentro da pasta onde o arquivo tá:

`cp processing-py.jar ~/CAMINHO/PASTA/DESEJADA`

Depois, quando quiser rodar a sketch, de dentro da pasta, no terminal, onde estão o arquivo .py e o **processing-py.jar** é só digitar:

`java -jar processing-py.jar NOME_SKETCH.py`

Voilà! [pelo menos por aqui a coisa tá funcionando! :]


