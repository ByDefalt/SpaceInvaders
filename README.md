# Space Invaders en python

### Installation des dépendances :

- **Tkinter**  
  - ```bash
    pip install tk
    ```

- **Random**  
  - *(Aucune installation requise, fait partie de la bibliothèque standard de Python)*

- **Winsound**  
  - *(Aucune installation requise, fait partie de la bibliothèque standard sur Windows ne fonctionne que sur Windows)*

- **Json**  
  - *(Aucune installation requise, fait partie de la bibliothèque standard de Python)*

### Capture d'écran : 

<img src="markdown_doc/space_invaders.png" alt="Capture d'écran du jeu" width="500"/>

###### Musique secrète quand la touche k est presser


### Acquis :

- **Création d'objet, d'instance et de méthode**

     ```python
    class SpaceInvaders(object):
    def __init__(self):
        self.root = tk.Tk()
        self.root.title("Space Invaders")#crée le titre
        self.frame = tk.Frame(self.root) #crée une fenêtre 
        self.frame.pack()
        self.game = Game(self.frame) #crée un element de type Game

    def keymanagementRL(self):#permet de gerer les deplacement de droite a gauche
        for key in self.keys: #key sont les clés du dictionnaire keys key=["space", "Right", "Left"]
            if self.keys[key]:#les cles ont pour valeur True or False
                if key == "Right":
                    self.game.defender.move_in(self.game.defender.move_delta)#lance la fonction move_in
                elif key == "Left":
                    self.game.defender.move_in(-self.game.defender.move_delta)#lance la fonction move_in
        self.root.after(15, self.keymanagementRL)#repete la fonction apres 15ms
    ...
    ...
    ...
     ```

- **Utilisation du Json :**
    ```python
    def inscripscores(self):#sert a inscrire le score
        self.resultats2 = self.resultats.fromFile("data/scores.json") #crée un tableaux de dictionnaire a partir de scores.json
        self.resultats2.ajout(self.scores) #ajoute scores au tableaux
        self.resultats2.toFile("data/scores.json") #met le tableaux dans le fichier scores.json
        self.affichescores() #lance affichescores

    ```

- **Optimisation du comportement pour plus de fluidité :**
    ```python
    def keymanagementRL(self):#permet de gerer les deplacement de droite a gauche
        for key in self.keys: #key sont les clés du dictionnaire keys key=["space", "Right", "Left"]
            if self.keys[key]:#les cles ont pour valeur True or False
                if key == "Right":
                    self.game.defender.move_in(self.game.defender.move_delta)#lance la fonction move_in
                elif key == "Left":
                    self.game.defender.move_in(-self.game.defender.move_delta)#lance la fonction move_in
        self.root.after(15, self.keymanagementRL)#repete la fonction apres 15ms

    def keymanagementSP(self):#permet de gerer les tirs
        for key in self.keys:#key sont les clés du dictionnaire keys key=["space", "Right", "Left"]
            if self.keys[key]:#les cles ont pour valeurs True or False
                if key == "space":
                    self.game.defender.fire()#lance la fonction fire de defender
        self.root.after(120, self.keymanagementSP)#repete la fonction apres 120ms contrairement a keymanagementRL afin de ne pas tiré tout les balle d'un seule cout

    def press(self, event):
        self.keys[event.keysym] = True #met la valeur True dans la key qui est l'event

    def release(self, event):
        self.keys[event.keysym] = False #met la valeur False dans la key qui est l'event

    def keymanagement(self): #sert a bind les touches

        self.drn = ["space", "Right", "Left"]
        self.keys = dict.fromkeys(self.drn, False)#creé un dictionaire de clé tableaux avec comme valeurs False

        for key in self.keys:
            self.root.bind("<KeyPress-%s>" % key, self.press)#bind les clés du dictionaire en press pour lancer la fonction press
            self.root.bind("<KeyRelease-%s>" % key, self.release)#bind les clés du dictionaire en release pour lancer la fonction release
                                                                #effectue pour chaque clés

        self.keymanagementRL()#appel keymanagementRL
        self.keymanagementSP()#appel keymanagementSP
    ```
