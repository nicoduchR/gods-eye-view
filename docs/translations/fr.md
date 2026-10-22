# French (`fr`)

Catalog: `src/i18n/locales/fr.json`. General rules: [TRANSLATORS.md](../TRANSLATORS.md).

## Style

- Use neutral French and address the user with « vous »: « Ajoutez », « Activez », « Réessayez ». Action labels use the infinitive: « Enregistrer », « Fermer le panneau ».
- Use sentence case and retain accents in uppercase labels: « EN DIRECT », « PÉRIMÉ ». Keep chips short; use « PRÉC. », « SUIV. », « VIT. », « DIST. » when needed.
- Use curly apostrophes and French quotation marks. Keep placeholders, keyboard keys (Space, Esc, Enter, Shift), provider names and protocol identifiers intact.
- Keep operational HUD codes (HDG, BRG, CRS, FOV, ALT, FT, KTS) and music genre names recognizable. Translate their explanations. Compass west is « O », so NW becomes « NO ».
- Preserve attribution, feed content, callsigns, user-authored text and machine values. Place presets may use conventional French names, such as « Londres » and « Dubaï ».
- Dates and numbers use the existing locale-aware formatters: « 15 janvier 2026 », « 1 234,5 ». Retain UTC wherever the source specifies it.
- Units remain unchanged in value: km, m, km/h, m/s, kn, ft, h, min, s, MW and hPa. Do not convert feet to metres or dollars to euros. Leave a space before a unit or percent sign. Currency magnitudes are « k$ », « M$ » and « Md$ ».
- Use « il y a » for elapsed time, but do not add it around a placeholder that already contains a relative-time label.

## Plurals

`Intl.PluralRules('fr')` requires three cardinal forms:

| Form    | Counts                                 | Example                |
| ------- | -------------------------------------- | ---------------------- |
| `one`   | 0, 1 and nonnegative fractions below 2 | 0 caméra, 1 caméra     |
| `many`  | exact nonzero multiples of one million | 1 000 000 caméras      |
| `other` | remaining counts                       | 2 caméras, 2,5 caméras |

The count is shown as digits, so `many` uses the same wording as `other`.
Roundabout exit ordinals are feminine: « 1re sortie », « 2e sortie », « 21e sortie ».
Choose ordinal categories using the active locale, not English suffix rules.

## Glossary

| English                           | Français                                                 |
| --------------------------------- | -------------------------------------------------------- |
| layer / data layer                | couche / couche de données                               |
| feed / source / provider          | flux / source / fournisseur                              |
| LIVE / SIMULATED                  | EN DIRECT / SIMULÉ                                       |
| stale / degraded / unavailable    | périmé / dégradé / indisponible                          |
| Provider Settings / API key       | paramètres des fournisseurs / clé API                    |
| enable / disable                  | activer / désactiver                                     |
| globe / basemap / map stack       | globe / fond de carte / ensemble cartographique          |
| aircraft / flight / vessel        | aéronef / vol / navire                                   |
| contact / tracking                | contact / suivi                                          |
| satellite / launch / payload      | satellite / lancement / charge utile                     |
| scene / shot / scene recipe       | scène / plan / recette de scène                          |
| heading / altitude / ground speed | cap / altitude / vitesse au sol                          |
| earthquake / active fire          | séisme / incendie actif                                  |
| street-level imagery              | imagerie au niveau de la rue                             |
| ALPR                              | LAPI (lecture automatisée des plaques d’immatriculation) |
| AQHI                              | CAS (cote air santé, Canada)                             |
| detection overlay                 | surcouche de détection                                   |
| cockpit / HUD                     | cockpit / HUD                                            |
| NOT AN ALL-CLEAR                  | NE GARANTIT PAS L’ABSENCE DE DANGER                      |

Shared French/English words, codes and proper names are explicitly reviewed in
`src/i18n/same-as-english.json`; they are not missing translations.
