# credits

La liste de l'écran « Crédits » des réglages : les projets et les services sur
lesquels Swiptv s'appuie, rangés par groupes. Chaque ligne ouvre la page du
projet ; sur Apple TV, faute de navigateur, l'app affiche un code que le
téléphone lit d'un coup d'appareil photo.

## Format

`v1.json` :

```json
{
  "version": 1,
  "updated": "2026-10-07",
  "sections": [
    {
      "id": "services",
      "title": { "en": "Services", "fr": "Services" },
      "entries": [
        {
          "id": "tmdb",
          "name": "TMDB",
          "url": "https://www.themoviedb.org",
          "description": { "en": "This product uses the TMDB API but is not endorsed or certified by TMDB." }
        },
        { "id": "trakt", "name": "Trakt", "url": "https://trakt.tv" }
      ]
    }
  ]
}
```

`updated` n'est pas lu par l'app, il est là pour qu'on sache d'un coup d'œil
quand le fichier a bougé pour la dernière fois.

Les groupes et les lignes s'affichent **dans l'ordre du fichier**.

Chaque groupe de `sections` :

| Champ | Obligatoire | Ce que c'est |
|---|---|---|
| `id` | oui | Identifiant du groupe. L'app ne le cherche pas par son nom : il sert à s'y retrouver. |
| `title` | oui | Le titre du groupe, par code de langue (`fr`, `en`, `pt-BR`…). L'anglais sert quand la langue de l'app manque, il doit donc être là. |
| `entries` | oui | Les lignes du groupe. |

Chaque ligne de `entries` :

| Champ | Obligatoire | Ce que c'est |
|---|---|---|
| `id` | oui | Identifiant de la ligne, unique dans le fichier. |
| `name` | oui | Le nom affiché, tel quel dans toutes les langues (c'est un nom propre). |
| `url` | oui | La page ouverte au tap. **Doit être en `https`.** |
| `description` | non | Une phrase sous le nom, par code de langue, l'anglais à défaut. Sert aux mentions qu'un service exige (celle de TMDB, par exemple). Sans elle, l'app affiche l'adresse du site sous le nom. |

## Ce que l'app refuse

- Une ligne sans `id`, sans `name` ou sans adresse `https` est écartée, sans
  emporter les autres.
- Un groupe sans titre anglais, ou sans aucune ligne valable, est écarté.

## TMDB

Les conditions d'utilisation de l'API TMDB demandent cette phrase, telle
quelle, dans l'écran des crédits : *« This product uses the TMDB API but is not
endorsed or certified by TMDB. »* Elle n'est donc donnée qu'en anglais, pour
garder la formulation exacte. Ne pas retirer la ligne TMDB tant que l'app
utilise leur API.
