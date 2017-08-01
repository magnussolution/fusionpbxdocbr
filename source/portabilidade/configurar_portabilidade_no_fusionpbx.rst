******************************************
Como configurar portabilidade no FusionPBX
******************************************

**FusionPBX** é um dos novos sistemas PBX, que muitos estão usando para substituir Elastix, uma alternativa muito usada em todo o mundo. E nosso sistema de portabilidade integra com facilidade a portabilidade neste fantástico PBX.
Para isso vamos adicionar a conta da portabilidade como um gateway SIP. Este novo GATEWAY sera quem vai conectar seu FreeSwitch com nossos servidores.


- Para adicionar o gateway va ao menu Accounts -> Gateways, clique em no sinal de + para adicionar novo Gateways.

	Gateways coloque PortabilidadeCelular
	Username: SEU_USUARIO_NO_SITE_PORTABILIDADECELULAR.COM
	Password: SUA_SENHA_NO_SITE_PORTABILIDADECELULAR.COM
	Proxy: sip.portabilidadecelular.com
	Context: public
	Profile:external
	 
	Salve e veja se registrou
 
- Agora vamos ao menu Dialplan -> Outbound Routes e clique no sinal de + para adicionar nova rota.
	Gateway: selecione o gateway criado.
	Dialplan Expression: (^0[1-9][1-9]9[0-9]{8}$) 
	Esta regra vai permitir vc ligar 0 DDD numero, ja com novo digito.
	Salve
 
- Agora temos que adicionar nosso gateways para completar a chamada após a consulta a portabilidade.
	Menu Account - > Gateways, adicione normalmente seus gateways para cada operadora.
 
- Agora criamos os DialPlan para enviar para os gateways conforme a operadora recebida. Va novamente para o menu Dialplan, outbound routes e clique em adicionar.
	Temos que criar uma Route para para operadoras que temos.
 
	Exemplo para TIM:
	Gateway: Selecionamos o gateway que vai completar chamada TIM.
	DialPlan Expression: (^553410)(\d*$)
	Prefixo: Aqui podemos colocar o código que precisamos enviar para nosso gateway quando a chamada for TIM. Por exemplo posso enviar 041.
	Context: redirected
	Salvar
 
- Agora temos que editar a rota criada e na ultima linha opção bridge, mudar a variável $1 para $2 deixando assim sofia/gateway/SEUTRONCO/$2
	A variable $2, é a que contem o numero recebido menos o 553410 ou seja 51982464731
	 
	Neste caso se eu disquei 0 DDD numero, ex 051 982464731 , e a consulta da portabilidade adicionou 55341. Sendo assim o numero entrara neste dialplan assim 55341051982464731.
	Por isso que no DialPlan Expression, dividimos o numero recebido em dois, e usamos do Bridge a variável $2. Veja que no bridge antes do tronco tem o prefixo que tínhamos adicionado, e como falei que gostaria de envia para meu gateway 041 DDD numero,  o comando bridge deveria ficar assim
	 sofia/gateway/SEUTRONCO/041$2
	 
	Esta regra vai pegar chamada que inicia com 55341, que é o codigo da TIM, seguido de qualquer numero, os  parênteses divide o números recebido em duas variasse $1 e $2
 
Ficou com duvida? Entre em contato pelo site . `portabilidade celular`_ 


video: https://youtu.be/S-JT5AVfmtI

.. _portabilidade celular: https://www.portabilidadecelular.com/contato.html