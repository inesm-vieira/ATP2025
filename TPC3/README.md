https://github.com/inesm-vieira/ATP2025/blob/83a1998e1996af5ecfcf711474076f0c03c5ddfd/Captura%20de%20ecr%C3%A3%202025-09-24%20210553.png

Inês Maria Moreira Vieira, A111979


Com este programa podemos criar, ler e analisar listas de números inteiros.
O utilizador pode, através de um menu, escolher gerar listas aleatórias ou introduzi-las manualmente, calcular a soma,  a média, o maior e menor número, verificar se a lista está ordenada de forma crescente ou decrescente e procurar a posição de um elemento específico, caso este faça parte da lista.


```python
import random

menu="""
MENU    
(1) Criar Lista 
(2) Ler Lista
(3) Soma
(4) Média
(5) Maior
(6) Menor
(7) estaOrdenada por ordem crescente
(8) estaOrdenada por ordem decrescente
(9) Procura um elemento
(0) Sair"""

def criarListaAleatoria():
    num1 = int(input("Quantos elementos pretende gerar? "))
    res = []
    i = 0
    while i < num1:
        res.append(random.randint(1, 100))
        i += 1
    return res

def lerLista(N):
    lista=[]
    i=1
    while i<= N:
        x=int(input(f"Introduza o número {i}: "))
        lista.append(x)                                     
        i=i+1
    return lista


def somaLista(lista):
    i=0
    for elem in lista:
        i=elem+i                               
    return i

def mediaLista(lista):
    i=0
    for elem in lista:
        i=elem+i 
    return i / len(lista) if lista else 0

def maiorLista(lista):
    res=lista[0]
    for elem in lista:   
        if elem>res:
            res=elem
    return res

def menorLista(lista):
    res=lista[0]
    for elem in lista[1:]:
        if elem<res:
            res=elem
    return res

def OrdenadaCrescente(lista):
    for i in range(len(lista) - 1):        
        if lista[i] > lista[i + 1]:       
            return "Não está ordenada"    
    return "Está ordenada"

def OrdenadaDecrescente(lista):
    for i in range(len(lista) - 1):        
        if lista[i] < lista[i + 1]:       
            return "Não está ordenada"    
    return "Está ordenada"

def procurarElemento(lista):
    elemento = int(input("Qual o número a procurar? "))
    i = 0
    while i < len(lista):
        if lista[i] == elemento:
            return i   
        i += 1
    return -1  
    


lista = []
print(menu)
op=input("Escolha uma opção: ")


while op!="0":

    if op == "1":
        lista = criarListaAleatoria()
        print("Lista criada com sucesso:", lista)
        print(menu)
        op=input("Escolha uma opção: ")

    elif op == "2":
        N=int(input("Quantos números deseja digitar? "))
        lista = lerLista(N)
        print("Lista introduzida:", lista)
        print(menu)
        op=input("Escolha uma opção: ")
    elif op == "3":
        if lista:
            print("Soma dos elementos:", somaLista(lista))
        else:
            print("A lista está vazia.")
        print(menu)
        op=input("Escolha uma opção: ")
    elif op == "4":
        if lista:
            print("Média dos elementos:", mediaLista(lista))

        else:
            print("A lista está vazia.")
        print(menu)
        op=input("Escolha uma opção: ")
    elif op == "5":
        if lista:
            print("Maior elemento:", maiorLista(lista))
            
        else:
            print("A lista está vazia.")
        print(menu)
        op=input("Escolha uma opção: ")
    elif op == "6":
        if lista:
            print("Menor elemento:", menorLista(lista))
            
        else:
            print("A lista está vazia.")
        print(menu)
        op=input("Escolha uma opção: ")
    elif op == "7":
        if lista:
            print("Ordenada por ordem crescente:" , OrdenadaCrescente(lista))
            
        else:
            print("A lista está vazia.")
        print(menu)
        op=input("Escolha uma opção: ")

    elif op == "8":
        if lista:
            print("Ordenada por ordem decrescente:", OrdenadaDecrescente(lista))
            
        else:
            print("A lista está vazia.")
        print(menu)
        op=input("Escolha uma opção: ")

    elif op == "9":
        if lista:
            posicao = procurarElemento(lista)
            if posicao != -1:
                print(f"O elemento foi encontrado na posição {posicao}.")
            else:
                print("O elemento não foi encontrado.")
        else:
            print("A lista está vazia.")
        print(menu)
        op=input("Escolha uma opção: ")

if op=="0":
        print("Até à próxima!")

```
