# Instalando sistema no SD

Usei o sistema distribuído pelo site da Fundação Processing, 
que já vem com o Processing e Java 8 pré-instalados.
Tutorial disponível em: https://pi.processing.org/get-started/ | Acesso em 11/02/2022.

Baixar e instalar um programa chamado Etcher (monta a imagem do SO no SD)
Baixar a imagem disponibilizada Raspbian com Processing.

# Configurando Raspberry remotamente

Tutorial disponível em ://help.realvnc.com/hc/en-us/articles/360002249917-VNC-Connect-and-Raspberry-Pi#setting-up-your-raspberry-pi-0-0 | Acesso em 11/02/2022.

Na Raspberry, utilizando monitor, mouse e teclado, aperte Ctrl + alt + T para abrir o Terminal.

` sudo apt-get update`

` sudo apt-get install realvnc-vnc-server`

Depois, rode o commando

` sudo raspi-config`

E navega até **Interfacing Options > VNC** e selecione **YES**

Após, digite `ifconfig` para descobrir o IP da Raspberry. 
O IP será usado para entrar pelo computador pessoal, utilizando o aplicativo VNC.


