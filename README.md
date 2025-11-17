Présentation

Ce mini-projet illustre une gestion simple d’un magasin en Java : on consulte les produits disponibles, on ajoute/supprime des produits dans un panier, puis on passe une commande pour un client. Le but est pédagogique : manipuler classes, objets, listes (ArrayList), et un petit menu texte.

Architecture et rôles des classes
Produit

Représente un article du magasin.

Attributs : id, nom, prix, quantite.

Méthodes clés :

afficherDetails() : affiche un résumé d’un produit.

Getters/Setters : accéder/modifier les champs.

Client

Représente un client qui passera une commande.

Attributs : id, nom, email.

Méthodes clés :

afficherDetails() (optionnelle) pour visualiser un client.

Getters/Setters.

Panier

Stocke les produits sélectionnés avant la commande.

Attribut : List<Produit> produits.

Méthodes clés :

ajouterProduit(Produit p) : ajoute un produit au panier.

supprimerProduitParId(int id) : supprime le premier produit ayant cet id.

afficherPanier() : liste les produits du panier et calcule le total.

calculerTotal() : somme de prix × quantite pour chaque produit.

getProduits() : renvoie la liste des produits du panier (utilisée par Commande).

Magasin

Stocke le catalogue des produits disponibles.

Attribut : List<Produit> produits.

Méthodes clés :

ajouterProduit(Produit p) : ajoute un article au catalogue.

afficherProduitsDisponibles() : affiche tous les produits.

trouverProduitParNom(String nom) : recherche simple par nom (insensible à la casse).

getProduits() : renvoie la liste du catalogue si besoin.

Commande

Représente un achat finalisé pour un client, à partir d’un panier.

Attributs : idCommande, client, List<Produit> produitsCommandes, total.

Construction :

Le constructeur reçoit idCommande, client, panier.

Il copie les produits du panier (new ArrayList<>(panier.getProduits())).

Il calcule le total via panier.calculerTotal().

Méthode clé :

afficherDetailsCommande() : récapitulatif de la commande (client, lignes, total).

Main (ou gestionmagasin.Main)

Point d’entrée avec un menu console pour tester l’application.

Initialise un Magasin avec quelques produits d’exemple.

Crée un Client et un Panier.

Affiche un menu boucle do...while avec Scanner :

Afficher les produits du magasin

Ajouter au panier (par nom)

Afficher le panier

Supprimer du panier (par id)

Passer commande (copie du panier dans une Commande et affichage du récapitulatif)

Quitter

Chaque choix déclenche la méthode correspondante (ex. magasin.afficherProduitsDisponibles(), panier.afficherPanier(), etc.).

Logique de fonctionnement

Catalogue
Le Magasin conserve la liste des produits disponibles. On peut les parcourir et en sélectionner un par son nom.

Panier
Quand l’utilisateur ajoute un produit, l’objet Produit est ajouté dans la liste du Panier.
Le panier calcule le total en additionnant prix × quantite de chaque produit présent.

Commande
Lorsqu’on “passe commande”, la Commande est créée à partir du Client et du Panier.
Les produits du panier sont copiés dans la commande, et le total est figé.
La méthode afficherDetailsCommande() affiche un récapitulatif complet.

Menu console
L’application boucle jusqu’à ce que l’utilisateur saisisse 0.
Les entrées clavier sont lues avec Scanner, et un switch oriente vers l’action choisie.

Exemple d’utilisation (scénario)

Lancer Main.

Choisir 1 pour voir les produits disponibles.

Choisir 2, saisir le nom d’un produit, il est ajouté au panier.

Choisir 3 pour afficher le panier et vérifier le total provisoire.

Éventuellement 4 pour retirer un article par son id.

Choisir 5 pour créer la commande et afficher le récapitulatif.

Choisir 0 pour quitter.

Hypothèses et limites 

Les produits sont ajoutés “tels quels” dans le panier (pas de gestion avancée des stocks ni de fusions d’articles identiques).

La recherche par nom est simple et retourne le premier match exact (insensible à la casse).

Les contrôles d’erreurs sont basiques (par exemple, pas de validation d’email côté Client).

Les données sont en mémoire uniquement (pas de base de données, pas de persistance).

Pistes d’amélioration

Gérer les quantités au niveau du panier (incrémenter la quantité si le même produit est ajouté plusieurs fois).

Mettre en place une vraie gestion de stock côté Magasin.

Ajouter la persistance (fichiers, base de données) et des tests unitaires.
