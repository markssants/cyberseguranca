# 🔒 Desafio de Autenticação: Bloqueio de Conta por Tentativas Inválidas

## 🚀 Visão Geral do Desafio

Em sistemas de segurança digital, é crucial prevenir ataques de força bruta. Este desafio implementa um mecanismo de segurança simples: **bloquear uma conta se houver 3 ou mais tentativas de login falhas consecutivas**.

O objetivo é processar uma lista cronológica de resultados de login e determinar se a conta deve ser bloqueada.

---

## 🎯 Regra de Bloqueio

Uma conta deve ser bloqueada se e somente se houver **três (3) ou mais** ocorrências da string **"falha"** em sequência.

* Uma tentativa de **"sucesso"** quebra a sequência de falhas e **reseta** o contador.

---

## 💻 Implementação em Python

O código utiliza um laço de repetição (`for`) para iterar sobre as tentativas e uma variável (`falhas_consecutivas`) para rastrear a contagem atual.

### 📝 Código

```python
import sys

def verificar_bloqueio(entrada):
    """
    Verifica se uma conta deve ser bloqueada com base em tentativas de login consecutivas.
    """
    # Divide a string de entrada em uma lista de tentativas, garantindo minúsculas e sem espaços
    tentativas = [item.strip().lower() for item in entrada.split(',')]

    # Inicializa o contador de falhas consecutivas
    falhas_consecutivas = 0
    
    # Flag para rastrear o estado de bloqueio
    bloqueada = False

    # Percorre cada tentativa
    for tentativa in tentativas:
        if tentativa == "falha":
            # Incrementa o contador de falhas
            falhas_consecutivas += 1
            
            # Verifica a condição de bloqueio (3 ou mais)
            if falhas_consecutivas >= 3:
                print("Conta Bloqueada")
                bloqueada = True
                break  # Para a verificação imediatamente após o bloqueio
        else:
            # Se for "sucesso", reseta o contador de falhas consecutivas
            falhas_consecutivas = 0  

    # Se o loop terminar sem que a flag de bloqueio tenha sido ativada
    if not bloqueada:
        print("Acesso Normal")

# --- Entrada ---
try:
    # Leitura da entrada (por exemplo: "sucesso, falha, falha, falha")
    entrada = sys.stdin.read().strip()
    if entrada:
        verificar_bloqueio(entrada)
    else:
        # Se nenhuma entrada for fornecida
        print("Acesso Normal")
        
except EOFError:
    # Trata o caso de entrada vazia ou fim de arquivo
    print("Acesso Normal")
```

# 🧠 Explicação da Lógica

## Pré-processamento da Entrada
A string de entrada (`"sucesso, falha, falha"`) é transformada em uma lista de strings: ['sucesso', 'falha', 'falha']


Isso facilita a iteração item a item.

---

## Variáveis de Controle

- **falhas_consecutivas**: Contador que registra quantas falhas ocorreram de forma consecutiva.  
  É resetado para `0` sempre que ocorre um "sucesso".

- **bloqueada**: Flag booleana (`True`/`False`) usada para indicar se o limite de falhas foi atingido.

---

## Iteração e Condicionais

- Para cada `"falha"` encontrada, o contador `falhas_consecutivas` é incrementado em `1`.
- Se, após o incremento, o contador for **maior ou igual a 3**, o programa:
  - Imprime: **"Conta Bloqueada"**
  - Define `bloqueada = True`
  - Encerra o loop imediatamente com `break`
- Para qualquer `"sucesso"`, o contador é zerado para `0`.

---

## Saída Final

Após o loop, o programa verifica o valor da flag `bloqueada`:

- Se **bloqueada == False**, significa que **não** ocorreram 3 falhas consecutivas → saída: **"Acesso Normal"**

---

# 🧪 Exemplos de Teste

| Entrada                                   | Falhas Consecutivas (Max) | Saída Esperada     |
|-------------------------------------------|----------------------------|---------------------|
| sucesso, falha, falha, falha              | 3 (atingido)               | Conta Bloqueada     |
| falha, falha, sucesso, falha              | 2                          | Acesso Normal       |
| falha, falha, falha, sucesso              | 3 (atingido)               | Conta Bloqueada     |
| sucesso, sucesso, falha, sucesso          | 1                          | Acesso Normal       |
| falha, falha, falha, falha, falha         | 5                          | Conta Bloqueada     |
