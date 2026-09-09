# legal

Les adresses des pages légales vers lesquelles l'app renvoie depuis l'écran
d'abonnement : la politique de confidentialité et les conditions d'utilisation.
Apple impose ces deux liens sur un écran d'abonnement.

Le texte de ces pages n'est pas ici. La confidentialité est publiée sur
`swiptv.app`, les conditions d'utilisation pointent sur l'EULA standard d'Apple.
Ce fichier ne porte que les adresses, pour qu'elles se corrigent en ligne sans
nouvelle version App Store.

Dans l'app, iPhone et iPad ouvrent le lien directement ; l'Apple TV, faute de
navigateur, affiche un code que le téléphone lit d'un coup d'appareil photo.

## Format

`v1.json` :

```json
{
  "version": 1,
  "updated": "2026-09-09",
  "entries": [
    { "id": "privacy", "url": "https://www.swiptv.app/privacy-policy" },
    { "id": "terms",   "url": "https://www.apple.com/legal/internet-services/itunes/dev/stdeula/" }
  ]
}
```

`updated` n'est pas lu par l'app, il est là pour qu'on sache d'un coup d'œil
quand le fichier a bougé pour la dernière fois.

Chaque entrée de `entries` :

| Champ | Obligatoire | Ce que c'est |
|---|---|---|
| `id` | oui | Identifiant de la page. L'app cherche `privacy` et `terms` par ce nom : ne pas les renommer. |
| `url` | oui | La page sur le web. **Doit être en `https`.** |

## Ce que l'app refuse

Le dépôt est public, donc l'app se méfie de ce qu'elle lit : une `url` absente
ou qui n'est pas en `https` fait écarter l'entrée concernée, sans emporter les
autres. Sans réseau, l'app n'a aucune adresse à ouvrir et le dit à l'écran
plutôt que de laisser un lien qui ne mène nulle part.
