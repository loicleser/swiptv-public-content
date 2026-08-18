# swiptv-public-content

Les contenus de l'app Swiptv qui vieillissent tout seuls, sortis du binaire pour
pouvoir être corrigés sans passer par une version App Store.

Un lien d'aide qui déménage, un article à ajouter ou à retirer, un titre à
reformuler : ça se fait ici, et l'app le voit à la prochaine ouverture de
l'écran concerné. Attendre une revue Apple pour corriger une adresse serait
absurde, et laisser un lien mort en attendant l'est encore plus.

## Organisation

Un dossier par besoin, un fichier par version de format.

| Dossier | Ce qu'il contient | Lu par |
|---|---|---|
| `vpn-help/` | Les fiches d'aide listées dans l'écran VPN des réglages | iPhone et Apple TV, depuis la v3.6 |

Chaque dossier a son propre `README.md` qui décrit son format champ par champ.

L'app lit les fichiers directement, sans intermédiaire :

```
https://raw.githubusercontent.com/loicleser/swiptv-public-content/main/vpn-help/v1.json
```

## Les deux règles

**1. On ne change jamais la forme d'un fichier déjà publié.**

C'est la règle qui compte le plus, parce qu'une version de l'app vit pour
toujours : un iPhone resté en 3.6 lira `v1.json` dans cinq ans, avec le code de
lecture de 2026. Renommer une clé ou rendre un champ obligatoire casserait
l'écran chez tous ceux qui n'ont pas mis à jour, et ils ne le signaleront pas,
ils verront juste une aide vide.

Donc : corriger une URL, changer un titre, ajouter ou retirer une entrée, tout
ça se fait librement dans `v1.json`. Mais le jour où la **structure** doit
bouger, on crée `v2.json` à côté et on laisse `v1.json` vivre sa vie pour les
anciennes versions.

**2. Ce qui est ici est public et sert de source unique.**

Pas de copie du même contenu dans l'app. L'app n'embarque rien et ne garde rien
en cache : ce qui s'affiche est ce que contient ce dépôt à cet instant. La
contrepartie est assumée : sans connexion, la section concernée n'affiche rien
et le dit.

## Modifier un contenu

Tout se fait depuis l'interface web de GitHub, sans rien installer :

1. Ouvrir le fichier, cliquer sur le crayon.
2. Modifier, commiter sur `main`.
3. Vérifier que le JSON est valide, GitHub le signale à l'affichage.

Le changement est visible par l'app dans la minute. Il n'y a rien à déployer et
personne à prévenir.
