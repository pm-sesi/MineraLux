# MineraLux – Monitoramento Inteligente de Iluminação em Mineração

Plataforma web para monitorar, de forma remota, torres de iluminação móveis e autônomas em minas a céu aberto. O sistema mostra o estado de cada torre (bateria, temperatura, luminosidade, consumo e falhas), gera alertas, guarda o histórico e exibe a localização das torres em um mapa interativo.

Um protótipo com **ESP32** e sensores fornece dados reais. As demais torres são **simuladas por software** para demonstrar o funcionamento em escala.

> **Status:** em desenvolvimento. Projeto acadêmico (TCC). A estrutura e os endpoints abaixo são o plano inicial e podem mudar.

## Contexto

- **Desafio:** Startup Challenge SAGA SENAI de Inovação 2026.
- **Demanda:** "Soluções Inteligentes em Iluminação", da Mineração Morro do Ipê S.A. (MG).
- **Problema:** as vias da mina mudam com frequência, há trechos remotos e baixa visibilidade (como serração), e as luminárias convencionais falham, consomem muito e exigem manutenção constante.
- **Nossa proposta:** uma camada de monitoramento e controle que avisa antes de a falha comprometer a via e mostra onde cada torre está.
- **Escola:** SESI/SENAI Horto, curso técnico de Informática para a Internet.

## Funcionalidades

- [ ] Recepção das leituras do ESP32 e do simulador por HTTP (JSON), com token por dispositivo
- [ ] Dashboard de status das luminárias
- [ ] Alertas automáticos (ex.: bateria abaixo de 20%, falha no sensor de luz, sem comunicação)
- [ ] Mapa 2D interativo da mina, com cor por estado e posição editável das torres
- [ ] Histórico e gráficos por luminária e período, com exportação CSV
- [ ] Acionamento remoto básico (ligar, desligar e dimerizar)
- [ ] Login com perfis de operador e manutenção

A baixa visibilidade é **estimada** a partir de umidade e luminosidade. Não é uma medição direta de neblina.

## Arquitetura

```
ESP32 (dados reais) ──┐
                      ├─ HTTP/JSON ─▶ API em PHP ─▶ MySQL
Simulador em PHP ─────┘                   ▲
                                          │ consulta a cada 5 s
                              Interface web (HTML, CSS e JavaScript)
```

## Tecnologias

| Camada | Tecnologia |
| --- | --- |
| Front-end | HTML, CSS e JavaScript |
| Back-end | PHP |
| Banco de dados | MySQL |
| Protótipo físico | ESP32 e sensores (temperatura/umidade, luminosidade, tensão da bateria) |

## Estrutura de pastas (planejada)

```
.
├── api/          # endpoints PHP (recepção de dados, alertas, comandos)
├── public/       # interface web (dashboard, mapa, histórico, login)
├── database/     # script SQL das tabelas e dados de exemplo
├── firmware/     # código do ESP32
├── simulator/    # script PHP que simula as demais torres
└── docs/         # documentação do TCC
```

## Como executar (ambiente local)

Requisitos: WAMP/XAMPP (ou outro ambiente com PHP e MySQL) e, para o protótipo, uma placa ESP32 na mesma rede Wi-Fi do servidor.

1. Clone o repositório dentro da pasta do servidor web: `htdocs` no XAMPP ou `www` no WAMP.
2. Inicie o Apache e o MySQL.
3. Crie o banco e importe o script de `database/` (quando estiver disponível).
4. Copie o arquivo de configuração de exemplo, ajuste as credenciais do banco e salve como o arquivo de configuração real (não o envie ao GitHub).
5. Acesse `http://localhost/` e o caminho da pasta `public/` no navegador.

## Exemplo de envio de leitura (plano)

```json
{
  "device_id": "T01",
  "token": "...",
  "bateria": 78,
  "temperatura": 31.5,
  "umidade": 62,
  "lux": 420,
  "consumo_w": 9.8
}
```

## Cronograma

Calendário sugerido pelo instrutor (não definitivo):

| Data | Marco |
| --- | --- |
| 27/11 | Planejamento técnico |
| 02/12 | MVP e demonstração intermediária |
| 04/12 | Validação |
| 08/12 | Documentação e vídeo pitch |
| 10/12 | Banca final |

## Equipe

- Jonathan Santos Blard
- Pedro Maia Fontes Lage

## Aviso

Projeto acadêmico, sem fins comerciais. Os dados de torres, luminárias e da mina usados nas demonstrações são simulados ou de protótipo. Licença a definir.
