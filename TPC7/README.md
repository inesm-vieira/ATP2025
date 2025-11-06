https://github.com/inesm-vieira/ATP2025/blob/83a1998e1996af5ecfcf711474076f0c03c5ddfd/Captura%20de%20ecr%C3%A3%202025-09-24%20210553.png
Inês Maria Moreira Vieira, A111979

Resolução do teste de aferição.
Resolução do tpc1 e tpc2, mais abaixo encontra-se a resolução do TPC3.

```python
#TPC1
#-------------------

print("TPC1")
#a)
lista1 = [1, 2, 3, 4, 5]
lista2 = [4, 5, 6, 7, 8]

ncomuns = [x for x in lista1 if x not in lista2] + [x for x in lista2 if x not in lista1]
print(ncomuns)
# [1, 2, 3, 6, 7, 8]

#b)
texto = """Vivia há já não poucos anos algures num concelho do Ribatejo 
    um pequeno lavrador e negociante de gado chamado Manuel Peres Vigário"""

lista = [palavra for palavra in texto.split() if len(palavra) > 3]
print(lista)
# ['Vivia', 'poucos', 'anos', 'algures', 'concelho', 'concelho', 'Ribatejo', 'pequeno', 'lavrador', 'negociante', 'gado', 'chamado', 'Manuel', 'Vigário']

#c)
lista = ['anaconda', 'burro', 'cavalo', 'macaco']
listaRes = [(i+1, valor) for i, valor in enumerate(lista)]
print(listaRes)
# [(1,'anaconda'), (2,'burro'), (3,'cavalo'), (4,'macaco')]


#TPC2
#----------------------

print(" ")
print("TPC2")
#a)
def strCount(s, subs):
    count = 0
    i = 0
    while i <= len(s) - len(subs):
        if s[i:i+len(subs)] == subs:
            count += 1
            i += len(subs)
        else:
            i += 1
    return count
print(f"a) Ex1: {strCount("catcowcat", "cat")}")
print(f"   Ex2: {strCount("catcowcat", "cow")}")
print(f"   Ex3: {strCount("catcowcat", "dog")}")

# Exemplos:
# strCount("catcowcat", "cat") → 2
# strCount("catcowcat", "cow") → 1
# strCount("catcowcat", "dog") → 0


#b)
def produtoM3(lista):
    lista_ordenada = sorted(lista)
    return lista_ordenada[0] * lista_ordenada[1] * lista_ordenada[2]

print(f"b) {produtoM3([12,3,7,10,12,8,9])}")
# produtoM3([12,3,7,10,12,8,9]) → 168


#c)
def reduxInt(n):
    while n >= 10:
        n = sum(int(dig) for dig in str(n))
    return n

print(f"c) Ex1: {reduxInt(38)} | Ex2: {reduxInt(777)}")
# reduxInt(38) → 2
# reduxInt(777) → 3


#d)
def myIndexOf(s1, s2):
    for i in range(len(s1) - len(s2) + 1):
        if s1[i:i+len(s2)] == s2:
            return i
    return -1

print(f"d) Ex1: {myIndexOf("Hoje está um belo dia de sol!", "belo")}")
print(f"   Ex2: {myIndexOf("Hoje está um belo dia de sol!", "chuva")}")
# myIndexOf("Hoje está um belo dia de sol!", "belo") → 13
# myIndexOf("Hoje está um belo dia de sol!", "chuva") → -1

```

```python
MyFaceBook = [
    {
        'id': '10023',
        'conteudo': 'Olá, hoje está um belo dia!',
        'autor': 'António',
        'dataCriacao': '2025-11-05',
        'comentarios': [
            {'comentario': 'Bem-vindo!', 'autor': 'prh'},
            {'comentario': 'Olá!', 'autor': 'jj'}
        ]
    },
    {
        'id': '11004',
        'conteudo': 'Mais um dia de trabalho.',
        'autor': 'Joana',
        'dataCriacao': '2025-11-06',
        'comentarios': [
            {'comentario': 'Força!', 'autor': 'jcr'}
        ]
    }
]

def quantosPost(redeSocial):
    return len(redeSocial)

def postsAutor(redeSocial, autor):
    return [post for post in redeSocial if post['autor'] == autor]

def autores(redeSocial):
    return sorted({post['autor'] for post in redeSocial})

def insPost(redeSocial, conteudo, autor, dataCriacao, comentarios):
    novo_id = f"p{len(redeSocial) + 1}"
    redeSocial.append({
        'id': novo_id,
        'conteudo': conteudo,
        'autor': autor,
        'dataCriacao': dataCriacao,
        'comentarios': comentarios
    })

def remPost(redeSocial, id):
    novaLista = []
    for post in redeSocial:
        if post['id'] != id:
            novaLista.append(post)
    return novaLista

def postsPorAutor(redeSocial):
    dist = {}
    for post in redeSocial:
        autor = post['autor']
        if autor in dist:
            dist[autor] += 1
        else:
            dist[autor] = 1
    return dist

def comentadoPor(redeSocial, autor):
    resultado = []
    for post in redeSocial:
        encontrou = False
        for com in post['comentarios']:
            if com['autor'] == autor:
                encontrou = True
        if encontrou:
            resultado.append(post)
    return resultado

def mostrarPosts(posts):
    if not posts:
        print(" Nenhum post encontrado.")
        return
    for p in posts:
        print(f"\nID: {p['id']}")
        print(f"Autor: {p['autor']}")
        print(f"Data: {p['dataCriacao']}")
        print(f"Conteúdo: {p['conteudo']}")
        print("Comentários:")
        if p['comentarios']:
            for c in p['comentarios']:
                print(f"  - ({c['autor']}) {c['comentario']}")
        else:
            print("  (Sem comentários)")
    print()

def menu():
    a_correr = True
    while a_correr:
        print("""

Menu

1 - Mostrar todos os posts
2 - Quantos posts existem
3 - Ver posts de um autor
4 - Ver lista de autores
5 - Inserir novo post
6 - Remover post por ID
7 - Mostrar nº de posts por autor
8 - Ver posts comentados por um autor
0 - Sair

""")
        op = input("Escolha uma opção: ")

        if op == '1':
            mostrarPosts(MyFaceBook)

        elif op == '2':
            print(f"Há {quantosPost(MyFaceBook)} posts na rede.")

        elif op == '3':
            autor = input("Autor: ")
            mostrarPosts(postsAutor(MyFaceBook, autor))

        elif op == '4':
            print("Autores registados:", ", ".join(autores(MyFaceBook)))

        elif op == '5':
            conteudo = input("Conteúdo do post: ")
            autor = input("Autor: ")
            data = input("Data de criação (AAAA-MM-DD): ")
            comentarios = []
            mais = "s"
            while mais == "s":
                mais = input("Adicionar comentário? (s/n): ").lower()
                if mais == "s":
                    texto = input("Comentário: ")
                    aut = input("Autor do comentário: ")
                    comentarios.append({'comentario': texto, 'autor': aut})
            insPost(MyFaceBook, conteudo, autor, data, comentarios)
            print("Post inserido com sucesso!")

        elif op == '6':
            idp = input("ID do post a remover (ex: p1): ")
            MyFaceBook[:] = remPost(MyFaceBook, idp)
            print(" Post removido")

        elif op == '7':
            dist = postsPorAutor(MyFaceBook)
            print("\nPosts por autor:")
            for a, n in dist.items():
                print(f" - {a}: {n} post(s)")
            print()

        elif op == '8':
            autor = input("Autor dos comentários: ")
            mostrarPosts(comentadoPor(MyFaceBook, autor))

        elif op == '0':
            print("Acabou")
            a_correr = False

        else:
            print("Opção inválida.")

if __name__ == "__main__":
    menu()
