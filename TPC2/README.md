https://github.com/inesm-vieira/ATP2025/blob/83a1998e1996af5ecfcf711474076f0c03c5ddfd/Captura%20de%20ecr%C3%A3%202025-09-24%20210553.png
Inês Maria Moreira Vieira, A111979

Jogo dos 21 fósforos:


import random

def jogo():

    jogador=input("Deseja jogar em primeiro ou em segundo lugar? ")
    p=1                #variavel que me permite verificar se no segundo caso o jogador ganha ou perde

    if jogador=="primeiro":
        cc=21
        while cc>1:
            print(f"O número de fósforos é: {cc}")
            n=int(input("Escolha um número de 1 a 4"))
            if n>=1 and n<=4:
                cc=cc-n
                t=5-n
                print(f"O número de fósforos é: {cc} eu retiro {t}")
                cc=cc-t
            else:
                print("jogada inválida")
        print("Perdeste só sobrou 1 fósforo")

    elif jogador=="segundo":
        cc=21
        x=random.randint(1 , 4)              #para gerar um número aleatório
        print(f"O número de fósforos é: {cc} eu retiro {x}")
        cc=cc-x
        while cc>1:
            print(f"O número de fósforos é: {cc}")
            n=int(input("Escolha um número de 1 a 4: "))
            if  n>=1 and n<=4:
                cc=cc-n
                if (x+n)<5 :                  
                    t=5-(x+n)
                    print(f"O número de fósforos é: {cc} eu retiro {t}")
                    cc=cc-t
                    x=0
                    p=0
                else:
                    x=random.randint(1 , 4)
                    while x>cc:
                        x=random.randint(1 , 4)
                    print(f"O número de fósforos é: {cc} eu retiro {x}")
                    cc=cc-x   
                    p=1 
            else:
                print("jogada inválida")
        if p==0:
            print("Perdeste só sobrou um fósforo")
        else:
            print ("Ganhaste")
    else:
        print("Jogada inválida")
jogo()


