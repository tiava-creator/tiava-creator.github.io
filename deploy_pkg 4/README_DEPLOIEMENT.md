# Déploiement du site OASIS-M sur tiava-creator.github.io

## Contenu de ce paquet

- Racine (`/`) : site français (source de référence), 9 pages.
- `/en/` : site anglais (miroir GOAP/UNSW), 9 pages.

Les deux sont des builds statiques Observable Framework indépendants, avec des chemins relatifs — aucune configuration serveur particulière n'est nécessaire, ça fonctionne avec n'importe quel hébergeur de fichiers statiques.

Contenu vérifié avant livraison : 18 pages (9 FR + 9 EN) testées en local, toutes en HTTP 200, chiffres identiques entre les deux langues (dont la double référence biomasse 1150/600 kg/ha ajoutée le 2026-08-09).

## Publication sur GitHub Pages

Le dépôt `tiava-creator.github.io` étant un dépôt "site utilisateur", tout ce qui est poussé sur sa branche par défaut (`main` ou `master` selon ta configuration) est servi directement à `https://tiava-creator.github.io/` — pas besoin d'activer Pages séparément si c'est déjà configuré.

### Si tu pars d'un dépôt vide ou que tu remplaces tout le contenu

```bash
git clone https://github.com/tiava-creator/tiava-creator.github.io.git
cd tiava-creator.github.io

# Vide le contenu existant si tu remplaces entièrement le site
# (attention si le dépôt contient déjà autre chose que tu veux garder)
rm -rf ./*

# Copie le contenu de ce paquet (adapte le chemin source)
cp -r /chemin/vers/deploy_pkg/* .

git add -A
git commit -m "Site OASIS-M : comptes SEEA EA récifs coralliens SW Madagascar (FR + EN)"
git push origin main
```

### Si tu veux ajouter ce site dans un sous-dossier d'un dépôt existant avec d'autre contenu

Copie simplement les dossiers (racine de ce paquet + `en/`) à l'endroit souhaité dans ton dépôt, en gardant leur structure interne intacte (ne pas renommer ou déplacer les fichiers à l'intérieur de `_observablehq/`, `_npm/`, `_file/` — les chemins relatifs en dépendent).

## Vérification après publication

Une fois poussé, GitHub Pages prend en général 1 à 2 minutes pour se mettre à jour. Vérifie :
- `https://tiava-creator.github.io/` → page d'accueil FR
- `https://tiava-creator.github.io/en/` → page d'accueil EN

## Point ouvert, pas bloquant

Il n'y a pas encore de lien croisé FR↔EN sur le site lui-même (le visiteur doit connaître l'URL `/en/` pour trouver la version anglaise). Si utile, je peux ajouter un petit lien de bascule de langue dans l'en-tête des deux versions — dis-le-moi et je le fais avant la prochaine régénération.

## Régénération future

Pour toute mise à jour de contenu, repartir des sources (`src/` pour le FR, `src-en/` pour l'EN) et utiliser la skill `goap-site-en`, pas ce paquet buildé — ce dossier est un instantané figé au 2026-08-09.
