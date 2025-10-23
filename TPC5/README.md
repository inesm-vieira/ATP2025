https://github.com/inesm-vieira/ATP2025/blob/83a1998e1996af5ecfcf711474076f0c03c5ddfd/Captura%20de%20ecr%C3%A3%202025-09-24%20210553.png
Inês Maria Moreira Vieira, A111979


Este código permite-nos gerir os dados de alunos de uma turma. Através de um menu o utilizador pode escolher criar uma turma, inserir aluno, listar turma, consultar aluno pelo id, guardar a turma num ficheiro e carregar a turma.



```python

# Estrutura: turma = [aluno1, aluno2, ...]
# aluno = (nome, id, [notaTPC, notaProj, notaTeste])


def criar_turma():
    return []

def inserir_aluno(turma):
    nome = input("Nome do aluno: ")
    id_aluno = input("ID do aluno: ")
    notaTPC = float(input("Nota do TPC: "))
    notaProj = float(input("Nota do Projeto: "))
    notaTeste = float(input("Nota do Teste: "))
    aluno = (nome, id_aluno, [notaTPC, notaProj, notaTeste])
    turma.append(aluno)
    print(" Aluno inserido com sucesso!\n")

def listar_turma(turma):
    if len(turma) == 0:
        print(" Turma vazia.\n")
    else:
        print("\nLista de Alunos")
        for aluno in turma:
            nome, id_aluno, notas = aluno
            print("ID:", id_aluno, "| Nome:", nome, "| Notas:", notas)
        print("        \n")

def consultar_aluno(turma):
    id_procurado = input("ID do aluno a consultar: ")
    encontrado = False
    for aluno in turma:
        nome, id_aluno, notas = aluno
        if id_aluno == id_procurado:
            print("\n Aluno encontrado:")
            print("Nome:", nome)
            print("Notas:", notas, "\n")
            encontrado = True
    if not encontrado:
        print(" Aluno não encontrado.\n")

def guardar_turma(turma):

    f = open("alunos.txt", "w", encoding="utf-8")
    for aluno in turma:
        nome, id_aluno, notas = aluno
        linha = "Nome: " + nome + "  ID:" + id_aluno + "  Nota TPC:" + str(notas[0]) + "  Nota Projeto:" + str(notas[1]) + " Nota Teste:" + str(notas[2]) + "\n"
        f.write(linha)
    f.close()
    print("Turma guardada em alunos.txt!\n")


def carregar_turma():
    
    turma = []
    f = open("alunos.txt", "r", encoding="utf-8")
    for linha in f:
        linha = linha.strip()
        campos = linha.split("::")
        nome = campos[0]
        id_aluno = campos[1]
        notaTPC = float(campos[2])
        notaProj = float(campos[3])
        notaTeste = float(campos[4])
        aluno = (nome, id_aluno, [notaTPC, notaProj, notaTeste])
        turma.append(aluno)
    f.close()
    print(" Turma carregada de alunos.txt!\n")
    return turma

def menu():
    print("""
    MENU 
1 - Criar uma turma
2 - Inserir um aluno
3 - Listar a turma
4 - Consultar aluno por ID
8 - Guardar turma em ficheiro
9 - Carregar turma de ficheiro
0 - Sair

""")

def main():
    turma = []
    opcao = ""
    while opcao != "0":
        menu()
        opcao = input("Escolha uma opção: ")

        if opcao == "1":
            turma = criar_turma()
            print(" Nova turma criada!\n")
        elif opcao == "2":
            inserir_aluno(turma)
        elif opcao == "3":
            listar_turma(turma)
        elif opcao == "4":
            consultar_aluno(turma)
        elif opcao == "8":
            guardar_turma(turma)
        elif opcao == "9":
            turma = carregar_turma()
        elif opcao == "0":
            print(" Operação finalizada \n")
        else:
            print(" Opção inválida.\n")

if __name__ == "__main__":
    main()

    
