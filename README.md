# ESP32 - Controle de Botão com Wi-Fi e API

Projeto desenvolvido durante a **Aula 07 - ESP32 - Wi-Fi**, com o objetivo de integrar uma placa ESP32 a uma API utilizando conexão Wi-Fi e requisições HTTP POST.

O projeto utiliza um botão físico conectado à protoboard. Quando pressionado, o ESP32 envia uma requisição POST para o back-end, transmitindo um dado no formato JSON.

---

##  Tecnologias Utilizadas

- ESP32
- Arduino IDE
- Linguagem C++
- Wi-Fi
- HTTP
- Node.js
- Express
- Protoboard

---

##  Componentes Utilizados

- 1 placa ESP32
- 1 protoboard
- 1 botão *push button*
- Fios jumper

---

##  Ligações do Circuito

O botão foi conectado à protoboard seguindo as seguintes ligações:

| Componente             | Pino da ESP32 |
| ---------------------- | ------------- |
| Botão (uma das pernas) | D4 (GPIO 4)   |
| Botão (outra perna)    | GND           |

> **Nota:** Foi utilizada a configuração `INPUT_PULLUP`, que ativa o resistor interno da ESP32, dispensando o uso de um resistor externo.

---

##  Funcionamento

O funcionamento do projeto acontece nas seguintes etapas:

1. A ESP32 inicia e se conecta à rede Wi-Fi.
2. O programa monitora continuamente o estado do botão.
3. Quando o botão é pressionado, a ESP32 identifica o acionamento.
4. Uma requisição HTTP POST é enviada para a API.
5. O back-end recebe os dados enviados no formato JSON.
6. A API retorna uma resposta confirmando o recebimento.

*O envio acontece somente quando o botão é pressionado.*

---

##  Dados Enviados para a API

A requisição POST utiliza a rota `/comandos` e envia o seguinte conteúdo JSON:

```json
{
  "botao": 1
}
```

O cabeçalho da requisição é configurado como:

```http
Content-Type: application/json
```

---

##  Configuração da API

Para executar o back-end, é necessário iniciar o servidor Node.js utilizando o comando:

```bash
npm run dev
```

O endereço IP do computador deve ser configurado no código da ESP32, juntamente com a rota `/comandos`.

Exemplo:

```cpp
const char* apiUrl = "http://IP_DO_COMPUTADOR:3000/comandos";
```

---

##  Resultado Esperado

Ao pressionar o botão, o Monitor Serial apresenta as mensagens de envio da requisição e a resposta recebida da API.

**Monitor Serial:**

```text
WIFI conectado
Botao pressionado!
Enviando requisicao POST...
Codigo HTTP: 200
"dados recebidos"
```

**Terminal do Back-end:**

```text
{ botao: 1 }
```

---

## Objetivo da Atividade

Aplicar os conhecimentos sobre comunicação Wi-Fi na ESP32, leitura de entradas digitais e integração entre dispositivos físicos e aplicações back-end por meio de requisições HTTP POST.
