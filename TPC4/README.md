https://github.com/inesm-vieira/ATP2025/blob/83a1998e1996af5ecfcf711474076f0c03c5ddfd/Captura%20de%20ecr%C3%A3%202025-09-24%20210553.png
Inês Maria Moreira Vieira, A111979

O programa permite gerir um cinema. O utilizador pode listar os filmes em exibição, inserir novas salas e verificar quantos lugares estão disponíveis em cada uma. Também é possível comprar e anular bilhetes, bem como ver a percentagem de ocupação da sala.


```python

import random


sala1 = (150, [], "Twilight")
sala2 = (200, [], "Hannibal")
sala3 = (140, [], "The Purge")
cinema = [sala1, sala2, sala3]


def listar(cinema):
    print("""
  Neste momento temos os seguintes filmes em exibição:""")
    for sala in cinema:
        print("   -", sala[2])
    return


def disponivel(cinema, filme, lugar):
    
    for sala in cinema:
        if filme.lower() == sala[2].lower():
            if lugar < 1 or lugar > sala[0]:
                print("      O lugar que indicou é inválido.")
                return False
            if lugar in sala[1]:
                print("      O lugar não está disponível.")
                return False
            else:
                print("      O lugar está disponível.")
                return True

    print("      Parece que o filme que inseriu não se encontra no nosso sistema. Tente novamente.")
    return False


def vendebilhete(cinema, filme, lugar):
   
    for sala in cinema:
        if filme.lower() == sala[2].lower():
            if lugar < 1 or lugar > sala[0]:
                print("      O lugar que indicou é inválido.")
                return
            if lugar in sala[1]:
                print("      Infelizmente esse lugar já não está disponível.")
                return
            sala[1].append(lugar)
            sala[1].sort()
            print("      O seu lugar foi reservado com sucesso. Obrigada pela preferência.")
            return
    print("      O filme indicado não foi encontrado.")
    return


def listardisponibilidades(cinema):
    
    for sala in cinema:
        disponiveis = sala[0] - len(sala[1])
        print(f"""   
          - Para '{sala[2]}' temos {disponiveis} lugares disponíveis.""")
    return


def inserirSala(cinema, sala):
   
    for sa in cinema:
        if sala[2].lower() == sa[2].lower():
            print("      O filme que inseriu já se encontra numa das nossas salas.")
            return
    cinema.append(sala)
    print(f"      Sala com o filme '{sala[2]}' adicionada com sucesso!")
    return


def anularBilhete(cinema, filme, lugar):
    """Anula (remove) um bilhete vendido"""
    for sala in cinema:
        if filme.lower() == sala[2].lower():
            if lugar in sala[1]:
                sala[1].remove(lugar)
                print("      O seu bilhete foi anulado. O seu reembolso acontecerá dentro de momentos.")
                return
            print("      Parece que esse lugar não está marcado como ocupado. Verifique o seu bilhete novamente.")
            return
    print("      Filme não encontrado.")
    return


def ocupacao(cinema, filme):
    
    for sala in cinema:
        if filme.lower() == sala[2].lower():
            disponiveis = sala[0] - len(sala[1])
            percentagem = (disponiveis / sala[0]) * 100
            print(f"      Para o filme '{filme}', a sala está {percentagem:.2f}% desocupada.")
            return
    print("      Parece que o filme que escolheu não está no catálogo.")
    return



def menu():
    print("""
  Escolha a opção que melhor se adequa à ação que quer realizar:
      1. Listar os filmes no catálogo
      2. Verificar disponibilidade de lugar
      3. Comprar bilhete
      4. Listar disponibilidades
      5. Inserir nova sala
      6. Anular compra de bilhete
      7. Ocupação de sala
      8. Sair""")
    escolha = input("      Insira aqui a sua opção: ")
    return escolha


print("Seja bem-vinda/o à nossa aplicação de gestão de cinemas!")

c = True
while c:
    escolha = menu()

    if escolha == "1":
        listar(cinema)

    elif escolha == "2":
        filme = input("      Insira o nome do filme que quer ver: ").strip()
        try:
            lugar = int(input("      Insira o lugar: "))
        except ValueError:
            print("      Valor inválido. O lugar deve ser um número.")
            continue
        disponivel(cinema, filme, lugar)

    elif escolha == "3":
        print("      As nossas salas estão organizadas por números. Cada sala tem um número limitado de lugares.")
        filme = input("      Insira o nome do filme que quer ver: ").strip()
        try:
            lugar = int(input("      Insira o lugar que quer: "))
        except ValueError:
            print("      Valor inválido. O lugar deve ser um número.")
            continue
        vendebilhete(cinema, filme, lugar)

    elif escolha == "4":
        listardisponibilidades(cinema)

    elif escolha == "5":
        filme = input("      Qual filme quer inserir? ").strip()
        try:
            lugar = int(input("      Quantos lugares quer que a sala tenha? "))
        except ValueError:
            print("      Valor inválido. Deve inserir um número.")
            continue
        if lugar <= 0:
            print("      O número de lugares deve ser positivo.")
            continue
        sala = (lugar, [], filme)
        inserirSala(cinema, sala)

    elif escolha == "6":
        filme = input("      Insira o filme para o qual quer anular o seu bilhete: ").strip()
        try:
            lugar = int(input("      Insira o lugar que quer anular na sala: "))
        except ValueError:
            print("      Valor inválido. O lugar deve ser um número.")
            continue
        anularBilhete(cinema, filme, lugar)

    elif escolha == "7":
        filme = input("      Insira o filme: ").strip()
        ocupacao(cinema, filme)

    elif escolha == "8":
        c = False
        print("""
      Obrigada pela preferência! Tenha um bom dia.""")

    else:
        print("      Opção inválida. Por favor, tente novamente.")




        ```
