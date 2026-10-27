# Design — Activités Côte d'Opale & Baie de Somme

Date : 2026-10-27  
Fichier cible : `content/voyages/europe/cote-dopale-baie-de-somme/index.fr.md`

## Objectif

Enrichir le carnet en construction avec des infos pratiques (activités, villages, randonnées), en distinguant clairement **Côte d'Opale** et **Baie de Somme** dans le sommaire.

## Structure de la page (H2)

1. **Comment venir** — conserver les liens existants (2 Caps, bus)
2. **Côte d'Opale** — avant Baie de Somme
3. **Baie de Somme** — bloc principal (inclut Mers-les-Bains et Le Tréport)
4. **Restaurants** — inchangé
5. **Infos pratiques** — inchangé
6. **À planifier** — inchangé

Sections H2 actuelles à supprimer (contenu utile redistribué) :

- Randonnées & visites guidées
- Autour du Tréport, Mers-les-Bains et Ault
- À voir

TOC déjà active (`showTableOfContents: true`). Ajouter le front matter `markup.tableOfContents` avec `endLevel: 3` (comme Paris) pour afficher les H3 sous Baie de Somme.

## Côte d'Opale

Section courte, prête à enrichir plus tard.

- Lien randonnée Caps Blanc-Nez ↔ Gris-Nez (existant)
- Pas de nouveau contenu long pour cette itération

## Baie de Somme

Sous-sections (H3), style fiches type page Paris (titre fort + puces factuelles) ; tableaux Markdown pour les randonnées. Pas d'emojis dans les titres. Niveaux de rando en texte : Facile / Moyen.

### Activités

Intégrer les infos concrètes (parcours, tarifs, prestataires, contraintes) :

| Activité | Points à garder |
| --- | --- |
| Traversée guidée de la baie | Crotoy → Saint-Valery ~7 km / 3h ; guide obligatoire ; 17 € / 6 € ; Rando Baie de Somme ; réservation ; retour voiture ou train vapeur |
| Observation des phoques — Hourdel | Gratuit ; créneau marée ; distance 300 m ; phare, blockhaus, sauterelliers ; postes été 25 mai – 17 août |
| Vélo (Vélomaritime / EV4) | Location Noyelles / Cayeux ; 2 itinéraires (~16 km, ~15 km) + liens Vélomaritime / Baiecyclette |
| Train à vapeur CFBS | Depuis 1887 ; 27 km ; 4 gares ; dîner wagon XIXe ; cfbs.eu |
| Parc du Marquenterre | Espèces ; sentiers 3,5 / 5,5 km ; jumelles 6 € ; tarifs ; lien site |
| Pirogue Va'a | ~3h ; Hourdel / phoques ; Va'a en Baie — Saint-Valery |
| Char à voile | Quend / Fort-Mahon ; 2h30–3h ; dès 7 ans ; ~45 € ; Ozone / Eolia |

### Villages & sites

- Saint-Valery-sur-Somme (médiéval, Courtgain, Chapelle des Marins, Tours Guillaume, calvaire)
- Le Crotoy (village coloré, belvédère Manessier)
- Cayeux-sur-Mer (chemin de planches 2 km, 400 cabines)
- Cimetière chinois de Nolette (Noyelles) — mémorial WWI
- Jardins de Valloires (Argoules) — tarifs + lien existant

### Mers-les-Bains

Rattaché à la Baie de Somme (choix validé).

- Villas Belle Époque (~600 façades, esplanade, secteur sauvegardé, 30–45 min)
- Notre-Dame de la Falaise
- Plage (galets/sable, sports nautiques)
- Marché lun/jeu matin
- Bois de Cise (classé, Art Nouveau, gratuit, ~90 m, GR120 ~45 min)

Liens Destination Le Tréport–Mers à réinjecter ici ou sous Tréport.

### Randonnées

Intro : GR21 comme colonne vertébrale.

Trois tableaux :

1. Au départ de Mers-les-Bains (5 entrées)
2. Au départ d'Eu (4 entrées)
3. Autres à proximité (5 entrées)

Colonnes : Randonnée · Distance · Durée · Niveau (si fourni) · Points d'intérêt ; pour le 3e tableau : + Départ.

### Le Tréport

- Funiculaire (gratuit, 100 m, 2 min)
- Falaises (106 m, GR21, danger effondrements)
- Quartier des Cordiers
- Église Saint-Jacques
- Port et halle aux poissons
- Kahl-Burg (visite guidée saisonnière)

## Format & style

- Markdown Hugo existant, français uniquement (`index.fr.md`)
- Gras pour faits clés (tarifs, durées, contraintes)
- Liens utiles existants réinjectés au bon endroit géographique
- Intro « Page en préparation… » : conserver telle quelle (pas de rewrite narratif)

## Hors scope

- Page anglaise (`index.en.md`)
- Enrichissement détaillé Côte d'Opale au-delà des liens Caps
- Images / feature image
- Nouveaux composants front (tout en Markdown)

## Critères de succès

- Au sommaire : Côte d'Opale apparaît avant Baie de Somme
- Mers et Tréport sont sous Baie de Somme, pas en H2 séparés
- Infos pratiques (tarifs, horaires marée, réservations) présentes sans spam emoji
- Anciennes sections redondantes retirées, meilleurs liens conservés
