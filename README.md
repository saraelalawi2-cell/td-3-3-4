#include <stdio.h>
#include <stdlib.h>
#include <time.h>

/* Structure d'un noeud */
typedef struct Noeud {
    int valeur;
    struct Noeud* suivant;
} Noeud;

/* Fonction qui supprime le noeud de valeur minimale */
Noeud* supprimerMin(Noeud *tete) {

   // si la liste est vide
    if(tete == NULL) {
        return NULL;
    }

  Noeud *courant = tete;
    Noeud *precedent = NULL;

  Noeud *minNode = tete;       // noeud contenant le minimum
    Noeud *minPrec = NULL;       // précédent du minimum

  // parcours pour trouver le minimum
    while(courant != NULL) {

  if(courant->valeur < minNode->valeur) {
            minNode = courant;
            minPrec = precedent;
        }

   precedent = courant;
        courant = courant->suivant;
    }

// suppression du minimum
    if(minPrec == NULL) {
        // le minimum est en tête
        tete = tete->suivant;
    } else {
        // relier le précédent au suivant du minimum
        minPrec->suivant = minNode->suivant;
    }

free(minNode);   // libérer mémoire
  return tete;     // retourner la nouvelle tête
}

int main() {

Noeud *tete = NULL;
    Noeud *nouveau, *courant;
    int i;

srand(time(NULL));

 // création de 100 noeuds
    for(i = 0; i < 100; i++) {

  nouveau = (Noeud*) malloc(sizeof(Noeud));

  if(nouveau == NULL) {
            printf("Erreur d'allocation\n");
            return 1;
        }

  nouveau->valeur = rand() % 100;

  nouveau->suivant = tete;
        tete = nouveau;
    }
  // affichage avant suppression
    printf("Liste avant suppression du minimum :\n");
    courant = tete;
    while(courant != NULL) {
        printf("%d -> ", courant->valeur);
        courant = courant->suivant;
    }
    printf("NULL\n");

   // suppression du minimum
    tete = supprimerMin(tete);

  // affichage après suppression
    printf("\nListe apres suppression du minimum :\n");
    courant = tete;
    while(courant != NULL) {
        printf("%d -> ", courant->valeur);
        courant = courant->suivant;
    }
    printf("NULL\n");

  // libération mémoire restante
    courant = tete;
    while(courant != NULL) {
        Noeud *temp = courant;
        courant = courant->suivant;
        free(temp);
    }
return 0;
}
