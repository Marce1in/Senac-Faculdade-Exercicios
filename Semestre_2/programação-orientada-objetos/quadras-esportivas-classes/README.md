# Sistema de Reserva para quadras esportivas

Esse sistema permite a criação de quadras esporivas! Nele existem 3 classes,
*Membro*, *Quadra* e *Reserva*.

## Membro

Essa classe encapsula tudo que se relaciona a um membro, cada membro tem:

- nome:

O `nome` deve ser passado como parâmetro na criação da classe e pode ser modificado
a qualquer hora, não precisando ser único

- id:

O `id` é responsável por identificar um determinado membro, **sempre** será único
e **não** pode ser substituído e nem mesmo modificado, é automaticamente selecionado
na criação da classe

## Reserva

Essa classe registra uma reserva, é preciso que cada reserva durante a criação 
tenha o *id* de quem a fez, *id* da quadra que vai ser reservada e qual o horário 
que ela será reservada (exemplo: das 17:00 até 20:30)

- idMembro:

Deve ser passado como parâmetro na criação da classe, é usado para identificar
o membro que fez a determinada reserva

- idQuadra:

Deve ser passado como parâmetro na criação da classe, é usado para identificar
qual quadra está sendo reservada.

- horario:

Uma array que guarda dois valores, a data de início e expiração de determinada 
reserva (exemplo: [17:00, 20:30]), a data de início deve ser lógicamente
menor que a data do fim

- data:

A data da criação de determinada Reserva, nela é contida as horas e o dia (padrão
brasileiro dia/mês/ano) que a Reserva foi criada

## Quadra

### atributos

Essa classe representa uma quadra de esportes

- id:

O `id` é responsável por identificar a reserva, **sempre** será único
e **não** pode ser substituído e nem mesmo modificado, é automaticamente selecionado
na criação da classe

- esporte:

O esporte representa para qual esporte a quadra será, deve ser passado como parâmetro na criação da classe

- apelido:

Basicamente o nome da quadra, pode ser passado com parâmetro na criação da classe,
é completamente opcional

- disponibilidade:

São os horários disponíveis, deve ser passado como parâmetro na criação de classe em
formato de array [primeira hora disponível, última hora disponível] (exemplo [11:00, 17:30]),
os valores devem estar em ordem correta

`disponibilidade` é um atributo privado, para acessa-lo deve usar o método `obterDisponibilidade`

- alugados

Essa array contém todos os horários já alugados, para popula-la deve-se usar o método `alugarQuadra` 

### métodos

- alugarQuadra

Esse método retorna uma `Reserva` e é usado para reservar a quadra por um determinado tempo

Esse método necessita como parâmetro o `id` do membro e o intervalo de tempo que ele deseja reservar a quadra
ex: [14:30, 17:00], é **essencial** que o intervalo seja no mínimo de 30 minuto, não podendo ser números 
quebrados como "12:37" ou "12:54", **somente** "12:00" ou "12:30"

esse método também popula o atributo `alugados` com os respectivos horários alugados

- popularDisponibilidade

É um método privado que auxilîa na criação do atributo `disponibilidade`, gerando uma array com todos os horários
disponíveis

ele recebe o **parâmetro** *disponibilidade* (o par de horários)

ex: se for passado [12:00, 14:30] para o `polularDisponibilidade`, será retornado [12:00, 12:30, 13:00, 13:30, 14:00, 14:30] 

- obterDisponibilidade

Esse método retorna o valor do atributo `disponibilidade`

recebe opcionalmente *n* número de parâmetros, esses parâmetros são arrays com um par de valores
[horarioInicial, horarioFinal], esses valores são usados para "filtrar" o atributo `disponibilidade`

ex: foram passados 3 parâmetros para o método: ([12:00, 14:30], [15:00, 16:00], [10:30, 11:00])
todos os horários entre esses valores não serão retornados por `obterDisponibilidade`

# TODO:


## Uma classe Quadra precisa:

- ter todos os horários disponíveis.
- contar com possíveis intervalos de tempo. Ex: das 11:30 até às 14:00 a quadra não abre.
- alugar horários específicos.

## Como:

- Ter todos os horários disponíveis.

Na criação da classe, um parâmetro chamado "intervalo" deve ser passado. Este 
parâmetro é um array com dois valores que determinam qual será o intervalo de 
tempo que uma quadra estará disponível.

Por exemplo: [11:30, 17:00]. Isso representa que o atributo terá horários das 11:30 até as 17:00.

Quando esse parâmetro for passado para a criação da classe, em seu construtor, esse 
valor será "desmembrado" por meio de um método e salvo dentro de um atributo 
chamado `disponibilidade`

ex: utilizando-se o array do exemplo acima, resultará em 
[11:30, 12:00, 12:30, 13:00, 13:30, 14:00, 14:30, 15:00, 15:30, 16:00, 16:30, 17:00].

- Contar com possíveis intervalos de tempo. Ex: das 11:30 até às 14:00 a quadra não abre.

Para fazer isso, é preciso abstrair o acesso do atributo.

Assim, o atributo `disponibilidade` é declarado como *privado* e para conseguir acessá-lo 
é necessário utilizar o método `obterDisponibilidade()`. Este método retorna o valor do 
atributo `disponibilidade`, mas é possível passar inúmeros parâmetros, sendo cada 
parâmetro um array que representa um intervalo de tempo.

Por exemplo: [11:30, 14:00]. Se isso for passado para o método, todos os horários 
entre 11:30 e 14:00 não serão retornados.

- alugar horários específicos

Para fazer isso, devemos criar um atributo que registre apenas os horários já alugados.

O atributo `alugados` faz exatamente isso. Ele registra em forma de array todos 
os horários já alugados.

Por exemplo: os horários entre 14:30 e 16:00 foram alugados, isso faz o atributo 
`alugados` ter o valor de [14:30, 15:00, 15:30, 16:00].
