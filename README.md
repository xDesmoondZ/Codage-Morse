
code_dict =  {'....-': '4', '.....': '5',
    '-...': 'B', '-..-': 'X', '.-.': 'R',
     '.--': 'W', '..---': '2', '.-': 'A', '..': 'I', '..-.': 'F',
     '.': 'E', '.-..': 'L', '...': 'S', '..-': 'U', '.----': '1', '-.-': 'K', '-..': 'D', '-....': '6','---': 'O', '.--.': 'P','--': 'M', '-.': 'N',
     '....': 'H', '.----.': "'", '...-': 'V', '--...': '7', '-.-.-.': ';',
     '-....-': '-', '..--.-': '_', '-.--.-': ')', '-.-.--': '!', '--.': 'G',
     '--.-': 'Q', '--..': 'Z', '-..-.': '/', '.-.-.': '+', '-.-.': 'C', '---...': ':',
     '-.--': 'Y', '-': 'T', '.--.-.': '@', '...-..-': '$', '.---': 'J', '-----': '0',
     '----.': '9', '.-..-.': '"', '-.--.': '(', '---..': '8', '...--': '3'
     }

def menu():
    print ("---------------------------------------------------------------------------------------------")
    
    print ("[1]. Codage morse")
     
    print ("[2]. Nombre premiers")

    print ("[3]. Validation de la base d'un nombre et sa conversion en décimal")

    print ("[4]. Quitter")

    print ("---------------------------------------------------------------------------------------------")
    
    choix =(input("saissisez votre choix"))
    return(choix)

### end def menu




def decodeMorse(morseCode):
    results = []
    wrong = []
    
    for item in morseCode.split(' '):
        results.append(code_dict.get(item, '?'))
        
        if item not in code_dict:
            wrong.append(item)
          
        
            
    return "" .join(results), (wrong)


def premiers(n, p=[2,3,5]):
    """Retourne la liste des nombres premiers <= n (méthode=division)"""
    k = p[-1]+2
    if n < k:
        return [x for x in p if x<=n]
    while k <= n:
        i = 0
        while i < len(p):
            if p[i]*p[i] > k:
                p.append(k)
                break
            if (k % p[i]) == 0:
                break
            i += 1
        k += 2
    return p
 

def base_to_decimal(number, base):
    if base == "2":
        nombre_convertie = int(number , 2)
    elif base == "8":
        nombre_convertie = int(number, 8) 
    elif base == "16":
        nombre_convertie = int(number, 16)

    print(number,"dans la base",base_name,"est égale à", nombre_convertie," dans la base décimal")    
    
    return nombre_convertie
    

def valide_nbr_base(number, base):

    if base == "2":
        chaara = "01"
    elif base == "8":
        chaara = "01234567"
    elif base == "10":
        chaara = "0123456789"
    elif base == "16":
        chaara = "0123456789ABCDEF"
        
    for char in number:
        if char not in chaara:            
            return False

    return True





option = ""
while option != "4":
    
    option = menu()
    
    if option == "1":

        morseCode = input(("donnez votre code morse"))

        results, wrong = decodeMorse(morseCode)
        print("Le décodage de votre message est comme suit:")
        print (results)
        if not wrong == []:
            print("Les codes morses invalides sont comme suit:")
            print (wrong)
    
    
        
    elif option =="2":
        
        n = ((input(("Veuillez entrer la limite supérieure de recherche des nombres premiers"))))

        while True:
            try:
                int(n)
            except ValueError:
        
        
                n = (input(("==> Erreur de saisie, taper un entier, réessayer")))
            else:
                # pas d'erreur; stopper la boucle
                break    
        

    
        n = int(n)    
        while n <= 2:
            n = int(input(("==> Taper un entier >=  2 réessayer ")))
        
        print ("Il y'a",len(premiers(n)),"nombres premiers qui sont:")

        print ( "==>", premiers(n))# affiche [2,3,5,7,11,13,17,19,23,29,31,37,41,43,47,53,59,61,67,71,73,79,83,89,97] pour n = 100 par exemple


    elif option =="3":
        # ---------------------------------------------------------------

        while True:
        # avoir le nombre
            number = input("donne un entier strictement positif à convertir: ")

        
            # le verifier
            correct = valide_nbr_base(number, "10")

    
    
            # quitter la boucle ou afficher erreur
            if correct:
                break
    
    
            else:
                print("==> Erreur de saisie, donne un entier strictement positif")



        while True:
   
            base = input("Choix de la base 2 [binaire], 8 [octal] 16[Héxadécimal] : 8 ")

            if base == "2":
                base_name = "Binaire"     
        
            elif base == "8":
                base_name = "Octoal"
            elif base == "16":
                base_name = "Hexadecimal"
            else:
                print("==> Input error, type 2, 8 or 16, retry")
                continue # return to `while`

            # verifier
            correct = valide_nbr_base(number, base)

            # quitter la boucle ou afficher erreur
            if correct:
                break
            else:
                print("==> Erreur:", number, "est un nombre non valide dans la base",base_name)

        # ---

        print() # ligne vide

        # ---

        result = base_to_decimal(number, base)
        print(result)

        
    elif option =="4":
        print ("vous pouvez quitter le menu")

    
