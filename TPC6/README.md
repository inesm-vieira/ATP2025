https://github.com/inesm-vieira/ATP2025/blob/83a1998e1996af5ecfcf711474076f0c03c5ddfd/Captura%20de%20ecr%C3%A3%202025-09-24%20210553.png
Inês Maria Moreira Vieira, A111979


Este código permite analisar dados meteorológicos, calcular médias, amplitudes térmicas e identificar dias chuvosos.

```python

tabMeteo1 = [
    (("2024", "03", "01"), 8.0, 15.0, 12.4),
    (("2024", "03", "02"), 6.5, 14.0, 3.2),
    (("2024", "03", "03"), 9.1, 17.5, 0.0),
    (("2024", "03", "04"), 10.2, 18.3, 1.1),
    (("2024", "03", "05"), 7.5, 13.2, 20.5)
]


def medias(tabMeteo):
    res = []
    for dia in tabMeteo:
        data = dia[0]
        tmin = dia[1]
        tmax = dia[2]
        media = (tmin + tmax) / 2
        res.append((data, media))
    return res



def guardaTabMeteo(t, fnome):
    f = open(fnome, "w", encoding="utf-8")
    for dia in t:
        data = dia[0]
        f.write(f"{data[0]};{data[1]};{data[2]};{dia[1]};{dia[2]};{dia[3]}\n")
    f.close()
    print("A tabela meteorológica foi guardada")




def carregaTabMeteo(fnome):
    res = []
    f = open(fnome, "r", encoding="utf-8")
    for linha in f:
        campos = linha.strip().split(";")
        ano = campos[0]
        mes = campos[1]
        dia = campos[2]
        tmin = float(campos[3])
        tmax = float(campos[4])
        prec = float(campos[5])
        registo = ((ano, mes, dia), tmin, tmax, prec)
        res.append(registo)
    f.close()
    print("A tabela meteorológica foi carregada")
    return res





def minMin(tabMeteo):
    minima = tabMeteo[0][1]  
    for dia in tabMeteo:
        if dia[1] < minima:
            minima = dia[1]
    return minima




def amplTerm(tabMeteo):
    res = []
    for dia in tabMeteo:
        data = dia[0]
        amplitude = dia[2] - dia[1]
        res.append((data, amplitude))
    return res




def maxChuva(tabMeteo):
    max_prec = tabMeteo[0][3]
    max_data = tabMeteo[0][0]
    for dia in tabMeteo:
        if dia[3] > max_prec:
            max_prec = dia[3]
            max_data = dia[0]
    return (max_data, max_prec)



def diasChuvosos(tabMeteo, p):
    res = []
    for dia in tabMeteo:
        if dia[3] > p:
            res.append((dia[0], dia[3]))
    return res




def sequenciaSeca(tabMeteo, p):
    cont = 0
    max_cont = 0
    for dia in tabMeteo:
        if dia[3] < p:
            cont += 1
            if cont > max_cont:
                max_cont = cont
        else:
            cont = 0
    return max_cont



import matplotlib.pyplot as plt

def extraiMin(t):
  res=[]
  for _,tmin,_,_ in t:
    res.append(tmin)
  return res

def extraiMax(t):
  res=[]
  for _,_,tmax,_ in t:
    res.append(tmax)
  return res

def extraiPrecip(t):
    res=[]
    for _,_,_,Precip in t:
        res.append(Precip)
    return res

def grafTabMeteo(t):

    x1=list(range(1,len(t)+1))
    y1= extraiMin(t)
    plt.plot(x1, y1, label= "Temperatura Mínima")

    x2=list(range(1,len(t)+1))
    y2= extraiMax(t)
    plt.plot(x2,y2, label= "Temperatura Máxima")

    x3=list(range(1,len(t)+1))
    y3= extraiPrecip(t)
    plt.plot(x3,y3, label= "Precipitação")

    plt.title("Meterelogia")
    plt.legend()
    plt.show()

    return


def menu():
    print("""
MENU 
1 - Ver médias diárias
2 - Ver amplitude térmica
3 - Ver temperatura mínima registada
4 - Ver dia com mais chuva
5 - Ver dias com precipitação acima de um valor
6 - Ver maior sequência de dias secos
7 - Desenhar gráfico
8 - Guardar tabela em ficheiro
9 - Carregar tabela de ficheiro
0 - Sair
""")

def main():
    tabMeteo = tabMeteo1 

    opcao = ""
    while opcao != "0":
        menu()
        opcao = input("Escolha uma opção: ")

        if opcao == "1":
            print(medias(tabMeteo))
        elif opcao == "2":
            print(amplTerm(tabMeteo))
        elif opcao == "3":
            print("Temperatura mínima absoluta:", minMin(tabMeteo))
        elif opcao == "4":
            print("Dia com mais chuva:", maxChuva(tabMeteo))
        elif opcao == "5":
            p = float(input("Limite de precipitação: "))
            print(diasChuvosos(tabMeteo, p))
        elif opcao == "6":
            p = float(input("Limite para dias secos: "))
            print("Maior sequência de dias secos:", sequenciaSeca(tabMeteo, p))
        elif opcao == "7":
            grafTabMeteo(tabMeteo)
        elif opcao == "8":
            guardaTabMeteo(tabMeteo, "meteorologia.txt")
        elif opcao == "9":
            tabMeteo = carregaTabMeteo("meteorologia.txt")
        elif opcao == "0":
            print("Acabou\n")
        else:
            print("Opção inválida\n")

if __name__ == "__main__":
    main()
