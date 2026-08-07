# Portfolio académique — Design

Date : 2026-08-08 (révisé après réception de la maquette réelle)

## Contexte

Portfolio personnel pour un profil de chercheur PhD (Lyu Chang), destiné à être
hébergé gratuitement via GitHub Pages, sur un repo public déjà créé :
`https://github.com/LyuChang-AI/portfolio`.

Note d'ownership : ce projet est développé par un tiers (développeur) pour le
compte du propriétaire du profil (Lyu Chang / compte GitHub `LyuChang-AI`). Le
repo appartient à `LyuChang-AI` dès le départ — le développeur travaillera via
un accès collaborateur (write) sur ce repo, pas via un transfert de repo après
coup.

## Révision importante

La conception initiale envisageait un site multi-pages (Accueil, Publications,
Projets, CV, Contact). L'utilisateur a fourni une **maquette HTML déjà
finalisée et fonctionnelle** (`~/Downloads/index.html`) représentant une page
unique de type "carte académique" (proche d'un link-in-bio), avec contenu réel
(vrai nom, vraie bio, vrais liens, vraie photo). L'utilisateur a confirmé :
**cette maquette constitue tout le site — pas de sous-pages.**

En conséquence :
- La structure multi-pages est abandonnée au profit d'une page unique.
- Le style est déjà écrit à la main (CSS custom avec variables), donc
  **pas de Tailwind** — on réutilise directement le CSS existant plutôt que de
  le réimplémenter dans un autre système, la maquette étant déjà complète et
  soignée.
- La palette et la typographie ne sont plus "à définir" : elles viennent de la
  maquette (voir Design system ci-dessous).

## Objectif

Une page vitrine unique, sobre et soignée, présentant le profil de recherche :
identité, liens de contact, résumé de recherche, formation, superviseurs,
activité académique récente.

## Stack technique

- **Statique pur, une seule page** (`index.html`). Pas de générateur de site,
  pas de framework JS, pas de Tailwind.
- CSS custom en `<style>` inline dans la page (tel que dans la maquette
  d'origine) — pas de fichier `style.css` séparé : la page est
  auto-suffisante, cohérent avec l'esprit "zéro build, zéro complexité" pour
  une page unique.
- **Aucun JavaScript nécessaire** (pas de nav, pas de menu mobile — c'est une
  seule page sans navigation interne). Les seules animations sont en CSS pur
  (`@media (prefers-reduced-motion:no-preference)`), déjà présentes dans la
  maquette.
- Polices Google Fonts : Space Grotesk (titres), Inter (corps de texte),
  JetBrains Mono (labels/méta), chargées comme dans la maquette.

## Amélioration technique ciblée

La maquette source embarque la photo de profil en **base64 inline** dans le
HTML (~60 Ko), ce qui alourdit la page et la rend illisible/difficile à
éditer. Amélioration retenue pour l'implémentation : extraire cette image en
fichier réel `assets/img/avatar.jpg`, référencé par un `src` classique. Gain :
page HTML lisible, image mise en cache par le navigateur, poids de page
réduit. Reste du CSS/HTML repris tel quel.

## Structure de fichiers

```
portfolio/
├── index.html           (page unique, reprise de la maquette + avatar externalisé)
├── assets/
│   └── img/
│       └── avatar.jpg   (photo extraite du base64 de la maquette)
├── 404.html              (page d'erreur GitHub Pages — optionnel, faible effort)
└── README.md
```

## Contenu de la page (déjà rédigé dans la maquette, à reprendre tel quel)

- **Hero** : nom (Lyu Chang), avatar, rôle ("Auditing large language models
  for digital gender-based violence"), affiliation (Programa de Doctorat en
  Física · Universitat de Barcelona), projet en cours (COVIMADI).
- **Find me** : liens directs — email universitaire, email personnel,
  LinkedIn, arXiv, ORCID. Tient lieu de section Contact.
- **Research** : paragraphe "about" décrivant l'axe de recherche.
- **Education** : MSc (Trinity College Dublin & UCD) et BA (Northeastern
  University, China).
- **Supervisors** : Sònia Estradé Albiol, Núria Vergés Bosch.
- **Recent academic activity** : liste de conférences/venues récentes (ESA
  Conference, FES 2026, Historical Materialism, Gender & Science Seminar).
- **Footer** : "Universitat de Barcelona".

Pas de section CV (pas de PDF disponible) ni de liste de publications
formelle avec DOI pour cette v1 — décision explicite de l'utilisateur. Ajout
possible plus tard comme entrée supplémentaire dans "Find me" (CV) ou section
dédiée (publications), sans changement d'architecture nécessaire.

## Design system (extrait de la maquette — définitif, pas à re-décider)

- **Couleurs** : fond `--paper:#f4f5f7` avec dégradé radial subtil en haut à
  droite, cartes `--card:#ffffff`, texte `--ink:#16171c`,
  `--ink-soft:#565b67`, `--ink-faint:#8b909c`, accent `--accent:#7a2c56`
  (bordeaux/prune profond), fond d'accent `--accent-tint:#f3e7ee`, lignes
  `--line:#e5e6eb` / `--line-strong:#d3d5dd`. Rayon de bordure `14px`.
- **Typographie** : Space Grotesk (titres/labels forts), Inter (corps de
  texte), JetBrains Mono (labels en petites capitales/métadonnées).
- **Layout** : carte centrée, `max-width:480px`, beaucoup d'espace blanc,
  microanimations d'apparition au chargement (fade + translateY), respect de
  `prefers-reduced-motion`.

## Déploiement

- Repo GitHub : `LyuChang-AI/portfolio` (déjà créé, vide).
- Accès : le développeur doit disposer d'un accès collaborateur (write) sur
  ce repo pour pousser depuis sa machine — le propriétaire (`LyuChang-AI`)
  crée le repo et invite le développeur en collaborateur ; aucun partage
  d'identifiants entre comptes.
- Hébergement : **GitHub Pages, "Deploy from a branch"** — branche `main`,
  dossier `/ (root)`. Pas de GitHub Actions/pipeline CI.
- URL finale : `lyuchang-ai.github.io/portfolio`.

## Vérification

- Test manuel responsive (mobile + desktop) dans le navigateur.
- Vérification que tous les liens externes (email, LinkedIn, arXiv, ORCID)
  sont valides et pointent vers les bonnes destinations.
- Vérification que l'avatar s'affiche correctement après extraction du
  base64 vers un fichier image.
- Vérification visuelle sur l'URL GitHub Pages réelle après déploiement.

## Hors scope (v1)

- Site multi-pages (abandonné — page unique confirmée par l'utilisateur).
- CMS ou build tool (Tailwind, générateur de site).
- Section CV / PDF téléchargeable (pas de fichier disponible).
- Liste formelle de publications avec DOI.
- Formulaire de contact (liens directs uniquement).
- Sections enseignement et blog/actualités.
- Nom de domaine personnalisé.
- Multilingue.
- Favicon personnalisé (favicon par défaut du navigateur pour cette v1).
