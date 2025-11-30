# 🛡️ Projeto de Simulação de Malware para Fins Educacionais

## Visão Geral do Projeto

Este projeto foi desenvolvido como parte do curso **CyberSegurança Santander DIO** com o objetivo de **semelhante, analisar e documentar** o funcionamento de duas ameaças digitais comuns — **Ransomware** e **Keylogger** — utilizando Python.

**⚠️ Aviso Importante:**O objetivo principal é exercer medidas de **⚠️ Aviso Importante:** Todos os scripts foram executados e testados em um **ambiente 100% isolado (Maquina Virtual)** e possivelmente fins estratificados 

---

## 1. Ransomware Simulado (Cripto-Malware)

A simulação demonstra como o Ransomware utiliza criptografia simétrica para sequestrar dados e exigir um resgate.

### ⚙️ Detalhes da Implementação

| Recurso | Descrição | Tecnologia |
| :--- | :--- | :--- |
| **Criptografia/Descriptografia** | Usa uma chave simétrica gerada de forma segura para criptografia do conteúdo de arquivos de teste. | `criptografia.fernet` |
| **Arquivos Alvo** | Cria arquivos de texto *espaço reservado* para dados importantes semelhantes (ex: `. . . . . . txt`). | Módulo `os` |
| **Mensagem de Resgate** | Gera um arquivo `LEIA_ME_RESGATE.txt` após a criptografia. | Manipulação de Arquivos |
| **Extensão** | Adiciona a extensão `. . . . . .bloqueado` (ou `. . . . . .bloqueado`) aos arquivos criptografados. | Módulo `os` |

### 🛠️ Estrutura e Execução

O processo é dividido em três fases simuladas:

1.   3. Cenários de Ataque Simulados e Análise`ransomware_parte1_preparacao.py`**: Cria arquivos de teste e geração a `chav_chave` (simulando a geração da chave no servidor do atacante).
2.  **`ransomware_parte2_criptografar.py`**: Leia a chave, itera sobre a massa de teste e criptografia todos os arquivos, deixando uma nota de resgate.
3.Os testes foram realizados utilizando uma ferrama 3.Medusa**`** para validar a exposição de serviços a ataques de dicionário e 

---

## 2. Keylogger Simulado (Captura e Exfiltração de Dados)

O Keylogger simula a captura de técnicas digitais e o ambiente furtivo dos dados para um ataque via e-mail.

### ⚙️ Detalhes da Implementação

| Recurso | Descrição | Tecnologia |
| :--- | :--- | :--- |
| **Captura de Teclas** | Registra tanto caracteres alfanuméricos quanto teclas especiais (Shift, Enter) em um arquivo de log. | `pynput` |
| **Registro Furtivo** | Execução como um *listener* em segundo plano para capturar os eventos do teclado de forma discreta. | `pynput.keyboard.Listener` |
| **Exfiltração (Envio Automático)** | Envia o arquivo de log como anexo via e-mail utilizando o protocolo SMTP. | `smtplib` e `email.mime` |
| **Segurança do Envio** | Utiliza **TLS** (`server.starttls()`) para criptografar a comunicação com o servidor SMTP, imitando uma prática comum em ataques. | `smtplib` |

---

## 3. 🧠 Reflexão e Estratégias de Defesa (Defesa em Profundidade)

A conclusão principal deste desafio é o entendimento de como mitigar esses ataques. A defesa não se limita a uma música ferrama, mas a uma abordagem em camadas (*Defesa em Profundidade*).

### 🛡️ Medidas de Prevenção e Mitigação

| Camada de Defesa | Ransomware | Keylogger |
| :--- | :--- | :--- |
| **1. Proteção de Ponto Final** | **EDR/Antivírus:** Detecção de **comportamento** (criptografia rápida de múltiplos arquivos). | **Detecção de Ganchos:** Bloco de APIs de monitoramento de texto ou processos suspeitos. |
| **2. Proteção de Dados** | **Backup 3-2-1:** Ter cópias offline/imutáveis é a única garantia de recuperação sem pagamento ou resgate. | **Gerenciadores de Senhas:** Elimina a necessidade de digitalizar credenciais, tornando o Keylogger ineficaz para capturar senhas. |
| **3. Segurança de Rede** | **Firewall:** Bloco de conexões de saúde suspeitas (Servidor C&C) para transmissão da chave de criptografia. | **Filtros de Saída:** Bloco da exfiltração de dados (envio do log) para servidores SMTP descartados ou não autorizados. |
| **4. Isolamento** | **Sandboxing / Máquinas Virtuais:** Executar algoritmos suspeitos em ambientes isolados para que a criptografia não afete o sistema principal. | Prevenir a instalação do *ouvinte* sem sistema operacional. |
| **5. Conscientização** | Tratamento contra Phishing e Engenharia Social, que são os principais vetores de entrega do malware. | Não baixar ou executar arquivos de fontes descobertas ou e-mails suspeitos. |

### 💡 Lições Aprendidas

1.  **Velocidade do Ransomware:** Uma criptografia simétrica é extremamente rápida. A janela de detecção é curta, reforçando a necessidade de EDRs que reajam ao comportamento, e não apenas a assinaturas.
2.  **O Ponto Fraco do Keylogger:** A fase mais vulnerável do Keylogger é a **Exfiltração**. Bloquear o ambiente de dados via rede (mesmo via canais criptografados como TLS) é uma defesa fundamental.
3.  **Ambiente Controlado:** A importância de ambientes de teste (VMs) para estudos de segurança é inegável, permitindo uma análise de códigos maliciosos sem riscos.
