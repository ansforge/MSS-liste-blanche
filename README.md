# Projet : Liste Blanche MSSanté 

Ce dépôt GitHub contient une liste blanche de ressources validées pour l'écosystème MSSanté ainsi qu'un mécanisme automatisé de vérification d'intégrité pour garantir que la liste n'a pas été compromise.

## Contenu

*   `listeblanchemssante.xml` : Le fichier principal contenant la liste blanche des ressources (domaines, adresses IP, etc.) autorisées dans le contexte MSSanté. Ce fichier est mis à jour régulièrement.
*   `checksum` : Un fichier texte contenant la somme de contrôle (checksum) du fichier `listeblanchemssante.xml`. Ce checksum est automatiquement recalculé à chaque mise à jour du fichier principal et permet de vérifier son intégrité.

## Objectif

L'objectif est de :

*   Assurer la transparence et la vérifiabilité de cette liste.
*   Détecter rapidement toute modification non autorisée du fichier `listeblanchemssante.xml`.

## Utilisation du checksum

1.  **Récupérer la liste blanche :** Téléchargez le fichier `listeblanchemssante.xml` depuis ce dépôt.

2.  **Vérifier l'intégrité :**
    *   Téléchargez le fichier `checksum`.
    *   Calculez le checksum du fichier `listeblanchemssante.xml` en utilisant l'algorithme SHA-256.
    *   Comparez le checksum calculé avec la valeur contenue dans le fichier `checksum`. Si les deux valeurs correspondent, le fichier `listeblanchemssante.xml` est intact.

    Exemple en ligne de commande (Linux/macOS) avec SHA-256 :

    ```bash
    shasum -a 256 listeblanchemssante.xml
    cat checksum
    ```

    Si les deux résultats sont identiques, vous pouvez utiliser le fichier `listeblanchemssante.xml` en toute confiance.

## Mécanisme d'Intégrité

À chaque *push* sur la branche `main` (ou la branche principale de ce dépôt), un workflow GitHub Actions est déclenché. Ce workflow effectue les opérations suivantes :

1.  Calcule le checksum (SHA-256) du fichier `listeblanchemssante.xml`.
2.  Écrit ce checksum dans le fichier `checksum`.
3.  Commit et push le fichier `checksum` mis à jour vers le dépôt.

Ce processus automatisé garantit que le fichier `checksum` est toujours synchronisé avec la dernière version du fichier `listeblanchemssante.xml`.


