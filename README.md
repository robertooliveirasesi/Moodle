# MOODLE - PRÉ REQUISITOS PARA INICIAR A INSTALAÇÃO #

Antes de iniciar a instalação é necessário que todo o ambiente web que funcionará por trás do Moodle esteja com as configurações mínimas para o perfeito funcionamento do Moodle. Além disso, as configurações devem suportar pelo menos 1000 (hum mil) usuários simultâneos na plataforma.

Servidor virtual para a aplicação (Produção)
  • Sistema operacional Linux; 
  • 8 x Vcpus de 2.4 Ghz; 
  • 12 GB de memória RAM; 
  • 90 GB de disco rígido; 
  • Link de 10 Mbit a 40 Mbit.

Servidor virtual para o banco de dados:
  • Sistema operacional Linux; • 8 x Vcpus de 2.4 Ghz; • 8 GB de memória RAM; • 90 GB de disco rígido.

Espaço em disco:
O espaço em disco necessário para o programa principal do Moodle é mínimo (1GB), no entanto, o que realmente é preciso é de espaço para armazenar os materiais que podem ficar em um servidor de arquivos externo.

#vMemória: A regra geral é que o Moodle pode suportar de 10 a 15 usuários concorrente para cada 1 GB de RAM, mas isso varia de acordo com a sua combinação de hardware e software específico e do tipo de uso. (Concorrente não é online. Concorrente também não significa o número de usuários cadastrados no banco. Concorrente não é o número de logins. Concorrente é o número de processos que o servidor realiza ao mesmo tempo, ou seja, concorrendo os processadores)

Requisitos mínimos necessários de software:
• Servidor Apache (nginx); • Banco de dados MariaDB 10.2.29 ou MySQL 8 • Linguagem de programação PHP na versão 7.4.0; • PhpMyAdmin • Imagem docker do Moodle
