"Algorithme Chiffrement RSA par Antoine CHEN"


print ('Bienvenue dans mon algorithme de déchiffrement RSA!')

# Fonction pour trouver la décomposition
# en facteurs premiers d'un nombre

def decomposition(n):
    resultat = []
    d = 2
    while n % 2 == 0:
        resultat.append(d)
        q = int(n/d)
        n = q
    d = 3
    while d <= n:
        while n % d == 0:
            resultat.append(d)
            q = int(n/d)
            n = q
        d = d + 2   
    return resultat    
    


# Fonction pour calculer le plus grand diviseur commun
# de deux nombres

def euclidien(a, b):
    if b == 0:
        return a
    else:
        r = a % b
        return euclidien(b, r)
    
    
    
#Fonction pour vérifier si un nombre est premier      
  
def prime(num):
    if num == 2:
        return True
    if num < 2 or num % 2 == 0:
        return False
    for n in range(3, int(num**0.5) + 2, 2):
        if num % n == 0:
            return False
    return True


     
# Fonction pour trouver la clé secrète d
# en connaissant le totient d'euler et e

def multiplicative_inverse(totient, e):    
    r1 = totient
    r2 = e
    s1 = int(1)
    s2 = int(0)
    t1 = int(0)
    t2 = int(1)  
    while r2 > 0:   
        q = r1//r2
        r = r1-q * r2
        r1 = r2
        r2 = r
        s = s1-q * s2
        s1 = s2
        s2 = s
        t = t1-q * t2
        t1 = t2
        t2 = t   
    if t1 < 0:
        t1 = t1 % totient
    return (r1, t1)
 
    
 
# Entrer deux nombres premiers p et q

p = int(input("Entrer un nombre premier = "))
q = int(input("Entrer un autre nombre premier = "))

while not (prime(p) and prime(q)):
    print("Les 2 nombres ne sont pas tous les deux premiers. Veuillez ressaisir deux nombres premiers.")
    p = int(input("Entrer un nombre premier = "))
    q = int(input("Entrer un autre nombre premier = "))
    
n = p * q
totient = (p - 1) * (q - 1)
 


# Génération de la clé publique (n,e) potentielle
# telle que 1 < e < totient

choose_public_key = []
 
for i in range(2, totient):
     
    plus_grand_div_commun = euclidien(totient, i)
     
    if plus_grand_div_commun == 1:
        choose_public_key.append(i)

print("choose_public_key=",choose_public_key)
 


# Sélection de la clé publique e
# parmi la liste ci-dessus

e = int(input("Choisir e parmi la liste ci-dessus = "))

 

# Génération de la clé secrète d

reste, d = multiplicative_inverse(totient, e)

while (reste!=1 or e not in choose_public_key):
     print("La multiplication inverse pour la clé publique choisie n'existe pas. Choisir une autre clé publique.")
     e = int(input("Choisir e parmi la liste ci-dessus = "))
     reste, d = multiplicative_inverse(totient, e)
     
d = int(d)           
public = (e, n)
private = (d, n)
print("La clé publique est:", public)
print("La clé secrète est:", private)



#Algorithme de chiffrement

def chiffrement(public, n_text):
    e, n = public
    x = []
    m = 0
    for i in n_text:
        if (i.isupper()):
            m = ord(i) - 6511
            c = (m**e) % n
            x.append(c)
        elif (i.islower()):               
            m = ord(i) - 97
            c = (m**e) % n
            x.append(c)
        elif (i.isspace()):
            x.append(400)
    return x
     
 
    
#Algorithme de déchiffrement

def dechiffrement(private, c_text):
    d, n = private
    txt = c_text.split(',')
    x = ''
    m = 0
    for i in txt:
        if (i == '400'):
            x += ' '
        else:
            m = (int(i)**d) % n
            m += 65
            c = chr(m)
            x += c
    return x
   
    
   
#Message

message = input("Que voulez vous chiffrer ou déchiffrer? (Séparer les nombres avec ',' pour le déchiffrement): ")
print("Votre message est:",message)
 
# Fonction pour retrouver la clé secrète (d,n) 
# en connaissant seulement la clé publique (e,n)

def reconstruction_private_key(e, n):
    totient = (decomposition(n)[0] - 1) * (decomposition(n)[1] - 1)
    d = int(multiplicative_inverse(totient, e)[1])
    private = (d, n)
    return private



#Choix chiffrement ou déchiffrement

choix = input("Tapez '1' pour chiffrer ou '2' pour déchiffrer: ")

while (choix != '1' and choix != '2'):
    print("Vous avez entré une option non valide.")
    choix = input("Tapez '1' pour chiffrer ou '2' pour déchiffrer: ")
    
if(choix == '1'):
    msg_crypt = chiffrement(public , message)
    print("Votre message chiffré est:", msg_crypt)
    print("Merci d'avoir utilisé l'algorithme RSA!")
elif(choix == '2'):
    print("Votre message déchiffré (l'algorithme de déchiffrement utilise la clé secrète) est:", dechiffrement(private, message))
    print("Votre message déchiffré (l'algorithme de déchiffrement n'utilise que la clé publique) est:", dechiffrement(reconstruction_private_key(e, n), message))
    print("Merci d'avoir utilisé l'algorithme RSA!")



