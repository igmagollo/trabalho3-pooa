# trabalho3-pooa
Terceiro trabalho da disciplina Programação Orientada a Objetos Avançada

Autores:
- Igor Raphael Magollo 743550
- Gabriel Olivato 743537

# Descrição da solução

Partindo do mais abstrato, existe uma classe ```System``` responsável por implementar o funcionamento do sistema, essa classe tem a responsabilidade de apenas orquestrar as responsabilidades das outras partes sem ter conhecimento de como tudo está funcionando.

Ela tem como dependência as interfaces para a execução dos principais requisitos do sistema: ```TableManInterface```(faz a interface para comunicação com o mesário), ```UserNotifierInterface``` (responsável pelas notificações para o usuário), ```VoteReceiverInterface``` (responsável pelo recebimento da entrada do usuário) e ```VoteRegisterInterface``` (responsável pelo registro dos votos).

## TableManInterface

Essa interface descreve as operações que o driver do componente de hardware responsável pela comunicação com o mesário deve disponibilizar. Assim, como o hardware pode mudar de equipamento para equipamento, o código encapsulado no driver facilita sua alteração.

## UserNotificationModule

Nesse modulo está a interface ```UserNotifierInterface``` que descreve apenas o método para emitir a notificação. A classe ```UserNotifier``` que implementa essa interface, utiliza o padrão de design _**Observer**_ para criar três canais de notificação, um canal de texto, um canal de imagem e um canal de audio. Dessa forma os componentes disponiveis para notificação só precisam implementar a interface ```ChannelObserver``` e serem registrados para observar os canais de interesse durante a contrução da classe ```UserNotifier``` (por exemplo, o componente Tela pode ser registrado nos canais de texto e de imagem, assim sempre que uma notificação de texto ou imagem for emitida, a tela receberá e exibirá, enquanto o componente de fone de ouvido pode se registrar no canal de audio).

Vale ressaltar que dessa forma é possível notificar o usuário de várias maneiras simultaneamente.

## VoteReceiveModule

Nesse modulo duas interfaces são utilizadas para descrever as operações de recebimento do voto e de notificar a confirmação do voto (feedback de confirmação), que são ```VoteReceiverInterface``` e ```VoteConfirmNotifierInterface```, dessa forma as classes que implementão a interface ```VoteReceiverInterface``` podem receber apenas uma instância da interface ```UserInputInterface``` para receber a entrada do usuário e utilizar um uma instância da interface ```VoteConfirmNotifierInterface``` para notificar o usuário da confirmação do voto.

## VoteRegisterModule

Neste módulo é definida a interface ```VoteRegisterInterface``` que sua única função é receber o voto e registrar ao longo das instâncias da interface ```DataWriterUnitInterface```.

## CommonInterfaces

Aqui estão as interfaces que não pertencem a nenhum módulo específico ou que devem interfacear implementações de drivers como é o caso das interfaces ```UserInputInterface``` e ```DataWriterUnitInterface```.

## Drivers

Aqui são exemplos de classes que implementam controladores para os diferentes componentes de hardware, independente do hardware ou de como esses drivers são implementados, uma vez que eles cumpram com a interface que estão implementando, o código funciona sem que as classes que dependem desses hardware precisem ser alteradas.
