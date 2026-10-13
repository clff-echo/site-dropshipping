# ALMA — Le quotidien, en mieux.

Boutique généraliste de démonstration : Maison, Tech et Nomade.
Le site tient dans **un seul fichier `index.html`**, avec styles, animations,
JavaScript, illustrations SVG, police intégrée et backend Python extractible.

**Aucune vente réelle :** produits et prix fictifs, aucun paiement ni expédition.

## Découvrir le site

Téléchargez le dépôt et ouvrez `index.html` dans un navigateur récent.
Le catalogue, les filtres et le panier fonctionnent sans installation.
L’enregistrement des demandes et commandes de test nécessite le serveur ci-dessous.

- Six produits, recherche, filtres et tri.
- Panier persistant, fiches produit et interface responsive.
- Animations respectant `prefers-reduced-motion`.
- Charte graphique et deux logos SVG téléchargeables depuis le pied de page.
- Cahier des charges intégré : **210 exigences**, dont 170 réalisées,
  4 restant à vérifier et 36 prérequis de production.

## Lancer le backend local

Python **3.12 ou ultérieur**, sans dépendance externe.
Depuis le dossier contenant `index.html` :

```sh
python3 -c 'from pathlib import Path; s=Path("index.html").read_text(); exec(s.split("<script id=\"backend-source\" type=\"text/plain\">")[1].split("</script>")[0])'
```

Le terminal affiche l’adresse locale du serveur sur le port 8000.
Le serveur écoute uniquement sur `127.0.0.1` et n’est pas destiné à la production.
`ALMA_PORT` permet de changer le port ; `ALMA_DATA_DIR` permet de changer le
répertoire de données (par défaut `~/.local/share/alma-demo`).
Vous pouvez aussi extraire `alma-server.py` depuis le Guide technique du site,
le placer à côté de `index.html`, puis le lancer depuis ce dossier.

### API de démonstration

| Méthode | Route | Fonction |
| --- | --- | --- |
| GET | `/api/health` | Santé et mode de démonstration |
| GET | `/api/products` | Catalogue |
| POST | `/api/contact` | Enregistrer une demande locale |
| POST | `/api/orders` | Enregistrer une commande de test |

Écritures JSON avec origine locale autorisée. Validation côté serveur,
recalcul des prix, idempotence des commandes, limitation des requêtes et stockage
SQLite. Les messages ne sont pas envoyés par e-mail. Utilisez des coordonnées
fictives. Les données de plus de sept jours sont purgées au démarrage et à l’écriture.

## Personnalisation

Les couleurs se trouvent dans `:root`, le catalogue partagé dans `catalog-data`,
les exigences dans `requirements-data` et le serveur dans `backend-source`.
Les cartes statiques du catalogue doivent rester cohérentes avec `catalog-data`
si vous changez les produits. Les illustrations sont des symboles SVG intégrés.

## Validation

46 contrôles automatisés ont réussi pendant la création : filtres, panier,
contact, commandes, validation API, idempotence, cinq largeurs de 320 à 1440 px,
zoom 200 %, contenu sans JavaScript et réduction des animations.
Ces contrôles ponctuels ne constituent pas une CI livrée ni un audit de production.
La recette sur téléphone physique, lecteurs d’écran, Safari/Firefox et les
mesures Lighthouse sur hébergement réel restent à effectuer.

## Avant toute commercialisation

Sélectionner et contrôler les fournisseurs, remplacer les données fictives,
valider les produits, renseigner l’identité du vendeur et les conditions légales,
brancher paiements et expéditions, puis déployer un backend de production sécurisé.
Le `noindex` est volontaire tant que le contenu est fictif.
Le domaine canonique, les métadonnées de partage et l’indexation sont à configurer
sur le domaine final. Le nom ALMA n’a pas fait l’objet d’une recherche de marque.

GitHub Pages peut héberger l’interface statique ; il ne peut pas exécuter ce
backend Python. Publier ce dépôt ne déploie pas automatiquement le site.

## Licence et contributions

Code et créations originales sous [licence MIT](LICENSE) : utilisation,
modification et redistribution autorisées en conservant la licence.
La police Open Sans conserve sa licence Apache 2.0 ; voir
[THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

Les contributions sont bienvenues par issue ou pull request. Ne publiez jamais
de données clients, clés API ou fichiers de base de données.
