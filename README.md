# Pokédex MDS

Portail qui regroupe les Pokédex de fan sous une seule adresse :

- `/` : page d'accueil « Choisis ton Pokédex » (ce dépôt, site statique sans étape de construction) ;
- `/hisui/` : [Pokédex Hisui](https://github.com/Gagz71/pokedex-hisui) (Légendes Pokémon : Arceus) ;
- `/kanto/` : [Pokédex Kanto](https://github.com/Gagz71/pokedex-kanto) (Pokémon Let's Go, Pikachu !) ;
- `/galar/` : [Pokédex Galar](https://github.com/Gagz71/pokedex-galar) (Pokémon Épée).

Chaque module garde son propre dépôt et son propre déploiement Vercel ; `vercel.json` renvoie
`/hisui/…`, `/kanto/…` et `/galar/…` vers eux de façon transparente (même adresse pour le navigateur, donc une
seule connexion Supabase partagée entre les modules).

## Ajouter un module

1. Dans l'appli du module : `base: '/<chemin>/'` dans `vite.config.ts`, et un `vercel.json` qui
   redirige `/` vers `/<chemin>/` et réécrit `/<chemin>/:path+` vers `/:path+` (voir Hisui ou Kanto).
2. Ici : deux règles dans `vercel.json` (`/<chemin>/` et `/<chemin>/:path+` vers le déploiement du
   module) et une carte dans `index.html`.
3. Dans Supabase (Authentication > URL Configuration) : ajouter
   `https://pokedex-mds.vercel.app/<chemin>/` aux Redirect URLs.
