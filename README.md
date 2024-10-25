# MORPION
def grille_jeu():
    # Affiche la grille de jeu
    print(" +---+---+---+")
    print(f"| {grille[0]} | {grille[1]} | {grille[2]} |")
    print(" +---+---+---+")
    print(f"| {grille[3]} | {grille[4]} | {grille[5]} |")
    print(" +---+---+---+")
    print(f"| {grille[6]} | {grille[7]} | {grille[8]} |")
    print(" +---+---+---+")

def victoire(symbole):
    # Scénarios de victoire horizontale, verticale et diagonale
    combinaisons_gagnantes = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],  # lignes
        [0, 3, 6], [1, 4, 7], [2, 5, 8],  # colonnes
        [0, 4, 8], [2, 4, 6]              # diagonales
    ]
    for combinaison in combinaisons_gagnantes:
        if grille[combinaison[0]] == grille[combinaison[1]] == grille[combinaison[2]] == symbole:
            print(f"Joueur {symbole} tu as gagné!")
            return True
    return False

# Initialisation de la grille et des variables
grille = [" " for _ in range(9)]
symbole = "X"  # Commence avec le joueur X
fin = False

print("Nous allons jouer au morpion.")
print("Le premier à aligner 3 symboles identiques gagne!")

# Boucle principale du jeu
while not fin:
    grille_jeu()
    try:
        choix = int(input(f"Joueur {symbole}, choisissez une case (1-9) : ")) - 1
        if choix < 0 or choix > 8 or grille[choix] != " ":
            print("Case invalide, réessayez.")
            continue
    except ValueError:
        print("Entrée invalide, veuillez entrer un chiffre entre 1 et 9.")
        continue

    grille[choix] = symbole  # Placer le symbole
    if victoire(symbole):    # Vérifier victoire
        grille_jeu()
        break

    # Changer de joueur
    symbole = "O" if symbole == "X" else "X"

    # Vérifier le match nul
    if " " not in grille:
        print("Match nul, vous pouvez réessayer.")
        grille_jeu()
        break
