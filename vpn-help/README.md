# vpn-help

Les fiches d'aide listées dans l'écran VPN des réglages, sur iPhone et sur
Apple TV. L'app affiche une ligne par entrée : une pastille de couleur avec son
symbole, le titre, et le lien qui mène à la fiche publiée sur le site.

Le texte des fiches n'est pas ici, il est sur `swiptv.app`. Ce fichier ne porte
que ce qu'il faut pour les annoncer et y mener.

## Format

`v1.json` :

```json
{
  "version": 1,
  "updated": "2026-08-18",
  "articles": [ ... ]
}
```

`updated` n'est pas lu par l'app, il est là pour qu'on sache d'un coup d'œil
quand le fichier a bougé pour la dernière fois.

Chaque entrée de `articles` :

| Champ | Obligatoire | Ce que c'est |
|---|---|---|
| `id` | oui | Identifiant stable de la fiche. Sert à la distinguer des autres, ne pas le réutiliser pour un autre sujet. |
| `symbol` | oui | Nom d'un symbole SF Symbols, dessiné dans la pastille. |
| `tint` | oui | Couleur de la pastille, en hexadécimal `#RRGGBB`. |
| `url` | oui | La fiche sur le site. **Doit être en `https`.** |
| `title` | oui | Le titre, par langue. |
| `subtitle` | oui | Une phrase de description, par langue. Elle n'apparaît que sur l'Apple TV, sur l'écran qui montre le code à scanner. |

## Les langues

`title` et `subtitle` sont des dictionnaires dont les clés sont les quinze
langues de l'app :

```
en  nl  fr  de  it  es  tr  da  pl  pt  pt-BR  sv  ar  he  nb
```

L'app prend la langue choisie dans ses réglages, et retombe sur `en` si elle
manque. Donc `en` est la seule vraiment obligatoire : une nouvelle fiche peut
n'être écrite qu'en anglais au départ, les autres langues se complètent après
sans rien casser.

Les fiches elles-mêmes, sur le site, sont en anglais uniquement. Traduire les
titres reste utile : c'est ce qu'on lit dans la liste, et ça permet de choisir
la bonne fiche avant de la lire.

## Ce que l'app refuse

Le dépôt est public, donc l'app se méfie de ce qu'elle lit et écarte
silencieusement les entrées douteuses plutôt que d'afficher n'importe quoi :

- une `url` qui n'est pas en `https` : l'entrée est ignorée, une fiche qui ne
  mène nulle part n'a rien à faire dans la liste
- un `title` vide dans la langue choisie **et** en anglais : l'entrée est ignorée
- un `symbol` inconnu de l'appareil : la pastille retombe sur un symbole neutre,
  l'entrée reste affichée

Ce dernier cas mérite attention : les symboles SF ajoutés par Apple dans une
version récente d'iOS ou de tvOS n'existent pas sur les appareils plus anciens.
En choisir un tout neuf ne casse rien, mais il ne se dessinera pas partout. Les
symboles disponibles depuis iOS 17 et tvOS 17 sont sûrs.

## Ajouter, retirer, réordonner

L'ordre du tableau `articles` est l'ordre d'affichage. Il suit aujourd'hui
l'ordre des questions qu'on se pose : ce qu'est un VPN, ce qu'est un profil, où
en obtenir un, comment l'ajouter, ce que l'app collecte.

Retirer une entrée la fait disparaître de l'app, sans autre effet. Une seule
exception, et elle mérite d'être connue avant de toucher au fichier :

**`what-we-collect` est la seule entrée que l'app désigne par son nom.** Elle
sert deux fois : dans la liste d'aide comme les autres, et derrière le « en
savoir plus » de la déclaration de collecte de données, l'écran qui s'impose
avant que le VPN puisse être activé. Changer son titre, sa couleur ou son
adresse est sans danger, les deux endroits suivent. Mais **changer son `id` ou
retirer l'entrée fait disparaître ce lien-là**, et la déclaration se présente
alors sans « en savoir plus ». Elle reste complète et lisible, c'est prévu,
mais autant le faire exprès plutôt que par accident.
