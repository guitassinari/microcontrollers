# Trabalho Microcontroladores
#### Guilherme de Oliveira Tassinari
#### Engenharia de Computação
#### Universidade Federal do Rio Grande do Sul
#### Cartão: 00231060

### Objetivo geral

Desenvolver um shield para a placa Galileo Gen2 capaz de acionar pelo menos uma das juntas do robô Quanser 2DSFJE.
O hardware deve ser capaz de:

- Acionar o motor (27V x 3A)
- Ler sensores (encoder + 2 sensores de fim de curso magnético)

### Entrega

A entrega inclui:

- Placa de circuito impresso a ser encaixada diretamente no conector shield da Galileo, com conectores para o robô e fontes.
- API para controle do robô
- Controlador PID utilizando API

### Especificações do trabalho

#### Placa impressa

###### Como e onde serão conectados os encoders do robô?
`A definição do trabalho diz que a placa deve ter os conectores para robô e fontes.
Como faço isso?`

##### Acionamento de motores

- O motor deve ser acionado por PWM (com resolução de, pelo menos, 8 bits)
    - Mais sobre PWM: https://www.kompulsa.com/introduction-pwm-pulse-width-modulation-works/
- Acionamento do motor por PWM deve ser:
    - 0%: motor girando a velocidade máxima em uma direção
    - 100%: motor girando a velocidade máxima na outra direção
    - A variação deve ser linear
    
##### Leitura de sensores

- Encoders devem ser decodificados em quadratura
    - Mais sobre encoders de quadratura aqui: http://www.creative-robotics.com/quadrature-intro
    - Mais sobre resolução de encoders de quadratura: https://www.linearmotiontips.com/how-encoder-resolution-is-determined/
- Contagem, ao menos parcial, feita em hardware para evitar perdas

![image](https://user-images.githubusercontent.com/10967861/64137996-5a65f100-cdd1-11e9-8ba2-51b4beeeba1f.png)

####### Contagem parcial em hardware?
``Se eu utilizar um circuito digital responsável por realizar a leitura do encoder de quadratura, serve?`

#### API

Deve ser fornecida uma biblioteca, com os arquivos de cabeçalho, com uma API para ser utilizada pelos desenvolvedores do controlador.
A API deve possibilitar:

- comando do motor em Volts
- leitura dos encoders em Radianos
- leitura dos sensores de fim de curso

A API deve ser executada em sistema Linux no espaço de usuário (sem permissões de superusuário).
É permitida a existência de módulos de kernel para implementar drivers ou outras funcionalidades que não possam ser feitas em espaço de usuário.

Deve ser feito um script de inicialização para configurar as permissões necessárias e carregar eventuais módulos do kernel.

#### Controlador PID

Para comprovar o funcionamento da API, deve ser implementado um controlador PID (proportional-integral-derivative), que definirá a tensão do motor pela funcão


O ajuste de ganhos pode ser feito por um método empírico, como Ziegler-Nichols ou método de ganho crítico.

O programa deve ser executado em sistema Linux no espaço de usuário (sem permissões de superusuário).
É permitida a existência de módulos de kernel para implementar drivers ou outras funcionalidades que não possam ser feitas em espaço de usuário.


### Avaliação

A avaliação do projeto inclui o hardware e o sofwtare necessário para a demonstração do trabalho. Em especial, o particionamento entre espaço de kernel e espaço de usuário.

Os nodos no `/dev` que forem necessários devem ser criados pelo próprio driver, para o qual deve ser criado o arquivo de regras para o `udev`

###### O que raios são nodos?

### Relatório

O relatório do trabaho deve incluir os esquemáticos do hardware, feitos em um sistema CAD apropriado e em folhas A4 ou A3.
