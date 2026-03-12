# NetPractice — Projeto 42 School

*Este projeto foi criado como parte do currículo da 42 por lbento.*

---

## Descrição

**NetPractice** é um exercício prático desenvolvido para apresentar os fundamentos de redes de computadores. Ao longo de 10 níveis progressivos, você irá configurar endereços IP, conectar dispositivos por meio de roteadores e entender como os dados trafegam pelas redes.

O objetivo é corrigir diagramas de rede com falhas para que todos os dispositivos consigam se comunicar corretamente. Cada nível apresenta uma configuração de rede não funcionando, e sua tarefa é preencher os valores ausentes (endereços IP, máscaras de sub-rede, gateways) até que a rede funcione.

> ⚠️ As redes neste projeto são simuladas — não são redes reais.

---

## Instruções

### Como executar a interface de treinamento

1. Baixe os arquivos do projeto na página do projeto na intranet da 42.
2. Extraia o arquivo baixado em qualquer pasta da sua máquina.
3. Abra o arquivo `index.html` no seu navegador (sem necessidade de servidor).
4. A interface do **NetPractice** será carregada no seu navegador.

### Usando a interface

- **Insira seu login** no campo de entrada para usar sua configuração personalizada. Isso é **obrigatório** para a entrega.
- Use a aba **"Practice"** (com seu login) durante o treinamento.
- Use a aba **"Evaluation"** para uma configuração aleatória — o mesmo formato usado durante a defesa entre pares.

### Resolvendo um nível

1. Leia o(s) **objetivo(s)** exibido(s) na parte superior da tela.
2. Modifique os **campos sem sombreamento** (os editáveis — IPs, máscaras, gateways, rotas).
3. Clique em **[Check again]** para verificar sua configuração.
4. Leia os **logs na parte inferior** da página para diagnosticar quaisquer problemas (gateway ausente, IP inválido, sub-rede incorreta, etc.).
5. Assim que o nível for concluído, um novo botão aparecerá — clique nele para avançar.

### Exportando sua configuração

Antes de passar para o próximo nível, **sempre clique em [Get my config]** para baixar seu arquivo de configuração. Este é o arquivo que você irá entregar.

### Requisitos de entrega

- Você deve completar e exportar **10 arquivos de configuração** (um por nível).
- Coloque todos os 10 arquivos na **raiz do seu repositório Git**.
- Certifique-se de que seu **login está inserido** na interface antes de exportar — ele deve aparecer no nome do arquivo/configuração.
- Durante a defesa, você terá que resolver **3 níveis aleatórios**, com limite de 15 minutos.
- Ferramentas externas **não são permitidas** durante a avaliação (apenas a calculadora `bc` é tolerada).

---

## Conceitos de Redes Estudados

Para completar o NetPractice, você deve entender os seguintes conceitos:

### Endereçamento TCP/IP
O sistema de endereçamento usado na internet e na maioria das redes locais. Cada dispositivo recebe um endereço IP que o identifica de forma única em uma rede.

### Estrutura de Endereço IPv4
Um endereço IPv4 tem 32 bits de comprimento, escrito como quatro octetos (ex.: `192.168.1.1`). Cada octeto varia de 0 a 255.

### Máscara de Sub-rede
Uma máscara de sub-rede define qual parte de um endereço IP identifica a **rede** e qual identifica o **host**. Exemplo: `255.255.255.0` (ou `/24`) significa que os primeiros 24 bits são a parte da rede.

| CIDR | Máscara de Sub-rede | Hosts por sub-rede |
|------|---------------------|-------------------|
| /24  | 255.255.255.0       | 254               |
| /25  | 255.255.255.128     | 126               |
| /26  | 255.255.255.192     | 62                |
| /27  | 255.255.255.224     | 30                |
| /28  | 255.255.255.240     | 14                |
| /30  | 255.255.255.252     | 2                 |

### Endereço de Rede e Broadcast
- O **primeiro endereço** de uma sub-rede é o **endereço de rede** (não pode ser atribuído a hosts).
- O **último endereço** é o **endereço de broadcast** (não pode ser atribuído a hosts).
- Os endereços de host utilizáveis são todos os que estão entre eles.

### Gateway Padrão
O endereço IP da interface do roteador que um dispositivo usa para enviar pacotes a destinos fora de sua própria rede. Todo dispositivo que precisa alcançar outra rede deve ter um gateway configurado.

### Roteadores
Dispositivos que encaminham pacotes entre diferentes redes. Cada interface de roteador pertence a uma rede diferente e possui seu próprio endereço IP.

### Switches
Dispositivos que conectam múltiplos dispositivos dentro da **mesma rede** (mesma sub-rede). Ao contrário dos roteadores, os switches não separam redes — todas as portas compartilham o mesmo endereço de rede.

### Tabela de Roteamento
Uma tabela em um roteador ou host que mapeia redes de destino para o próximo salto (gateway). A rota especial `0.0.0.0/0` é a **rota padrão** — ela corresponde a qualquer destino não correspondido por rotas mais específicas.

### Modelo OSI (referência)
O modelo de 7 camadas que descreve como os dados se movem por uma rede:
1. Física
2. Enlace de Dados
3. **Rede** ← O endereçamento IP fica aqui
4. Transporte
5. Sessão
6. Apresentação
7. Aplicação


## Recursos

### Oficiais e Documentação
- [RFC 791 — Internet Protocol](https://datatracker.ietf.org/doc/html/rfc791)
- [Cisco Networking Basics](https://www.cisco.com/c/en/us/solutions/small-business/resource-center/networking/networking-basics.html)
- [Calculadora de Sub-rede](https://www.subnet-calculator.com/)
- [Referência CIDR para Máscara de Sub-rede](https://cidr.xyz/)

### Tutoriais e Guias
- [Como Funciona o Subnetting — Practical Networking](https://www.practicalnetworking.net/stand-alone/subnetting-mastery/)
- [Guia TCP/IP (livro online gratuito)](http://www.tcpipguide.com/free/index.htm)
- [Cheat Sheet do NetPractice — notas comuns da comunidade](https://github.com/lpaube/NetPractice)

---

## Meu guia

Aqui está um guia visual rápido que fiz enquanto estudava o NetPractice.

**Para ver o guia, basta abrir o arquivo `net_practice_guide.html` no seu navegador (sem necessidade de servidor).**

![Guia NetPractice](guide.png)


## Referência Rápida: Regras para resolver os níveis

1. **Dispositivos no mesmo switch devem estar na mesma sub-rede.**
2. **Duas interfaces de roteador conectando duas redes devem estar em sub-redes diferentes.**
3. **Todo dispositivo que se comunica fora de sua sub-rede precisa de um gateway.**
4. **O gateway deve ser um IP na mesma sub-rede que o dispositivo.**
5. **Tabelas de roteamento: `0.0.0.0/0` como destino = rota padrão (enviar tudo aqui).**
6. **Nunca atribua o endereço de rede ou o endereço de broadcast a um dispositivo.**
7. **Um roteador roteia entre redes — suas interfaces estão em sub-redes diferentes.**


## Soluções

Aqui estão todas as soluções para os 10 níveis.

### Nível 6

<details>
  <summary>mostrar</summary>

  ![Nível 6](https://github.com/lucabarbosa/Net_Practice/blob/main/solved_levels/ex_6.png)
  
</details>

### Nível 7

<details>
  <summary>mostrar</summary>

  ![Nível 7](https://github.com/lucabarbosa/Net_Practice/blob/main/solved_levels/ex_7.png)
  
</details>

### Nível 8

<details>
  <summary>mostrar</summary>

  ![Nível 8](https://github.com/lucabarbosa/Net_Practice/blob/main/solved_levels/ex_8.png)
  
</details>

### Nível 9

<details>
  <summary>mostrar</summary>

  ![Nível 9](https://github.com/lucabarbosa/Net_Practice/blob/main/solved_levels/ex_9.png)
  
</details>

### Nível 10

<details>
  <summary>mostrar</summary>

  ![Nível 10](https://github.com/lucabarbosa/Net_Practice/blob/main/solved_levels/ex_10.png)
  
</details>