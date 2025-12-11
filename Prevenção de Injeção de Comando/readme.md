# 🛡️ Solução Detalhada para a Detecção de Injeção de Comando

O objetivo deste código é proteger o sistema validando a entrada do usuário. Ele funciona buscando por caracteres que, em um ambiente de shell de comando (como Linux ou Windows PowerShell), são usados para encadear ou modificar a execução de comandos, caracterizando uma tentativa de Injeção de Comando.

## 🔍 O Que São Caracteres Suspeitos?

Os caracteres listados abaixo não são comandos por si só, mas sim operadores de controle que alteram o fluxo de execução de um sistema operacional. Ao proibir estes caracteres, a lógica impede que o usuário execute mais de um comando ou acesse variáveis de ambiente.

| Caractere | Função em um Shell                                       | Por que é Suspeito?                                            |
|-----------|--------------------------------------------------------|--------------------------------------------------------------|
| `;`       | Separador de comandos                                   | Permite executar um comando após o outro (ex: `cmd1; cmd2`). |
| `&`       | Execução em background ou encadeamento (`&&`)         | Usado para iniciar processos ou executar comandos condicionalmente. |
| `|`       | Pipe (Redirecionamento)                                | Interconecta a saída de um comando com a entrada de outro.    |
| `$`       | Substituição de variável ou comando                    | Permite acessar dados sensíveis ou executar comandos aninhados (ex: `echo $PATH`). |

## 💻 Código com Explicação Integrada

O código Python abaixo implementa a lógica de verificação usando um loop simples para checar a presença desses operadores de risco.

```python
def verificar_comando(comando):
    # Lista de caracteres suspeitos que indicam uma tentativa de Injeção de Comando.
    caracteres_suspeitos = [';', '&', '|', '$']

    # Inicia um loop para verificar cada caractere suspeito.
    for char in caracteres_suspeitos:
        # A instrução 'if char in comando' é a verificação de segurança.
        if char in comando:
            # Se for encontrado QUALQUER um dos caracteres de risco,
            # o sistema retorna uma string de alerta e encerra a verificação.
            return "Comando Suspeito"

    # Se o loop terminar sem encontrar nenhum caractere suspeito, 
    # o comando é considerado seguro para ser executado.
    return "Comando Seguro"

# --- Execução e Teste ---
# 1. Entrada do usuário (recebe a string do comando a ser analisado)
comando_usuario = input("Digite o comando a ser testado: ")
# 2. Chama a função de segurança e imprime o resultado.
print(verificar_comando(comando_usuario))
