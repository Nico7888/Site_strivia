# Site vitrine Strivia (Hugo)

Site marketing statique construit avec [Hugo](https://gohugo.io), inspiré du langage visuel de [fullenrich.com](https://fullenrich.com) (hero avec fond vagues, bandeau social proof, cartes produit flottantes, sections chiffres-clés, bloc sécurité/RGPD) et adapté à l'identité et au contenu Strivia (brief marketing fourni).

## Lancer le site en local

```bash
# Installer Hugo (extended) si besoin — ex. Ubuntu/Debian :
sudo apt-get install hugo

cd website
hugo server -D
# → http://localhost:1313
```

## Build de production

```bash
cd website
hugo --gc --minify
# Le site statique est généré dans website/public/
```

## Structure

```
website/
  hugo.toml              # config, menu, params globaux (email, CTA…)
  content/
    _index.md            # TOUT le contenu texte de la home (hero, méthode,
                          # process, sécurité, témoignages…) est dans le
                          # front matter — modifiable sans toucher au HTML
    blog/                # cas d'usage (1 fichier .md = 1 étude de cas)
    contact.md
    mentions-legales.md
    politique-de-confidentialite.md
  layouts/                # templates Hugo (aucun thème externe)
  static/
    css/main.css          # design system complet (couleurs, composants)
    js/main.js             # menu mobile
    images/                # favicon + logo recréés en SVG (voir note ci-dessous)
```

## À compléter avant mise en ligne

- **Logo** — `layouts/partials/logo.html` contient une recréation SVG du logo
  (carré dégradé bleu + wordmark) faite à partir de la capture fournie, faute
  de pouvoir récupérer le fichier vectoriel original. Remplacez ce SVG par
  votre fichier logo réel (export SVG depuis Figma/Illustrator) pour un rendu
  pixel-perfect.
- **Témoignages** — la section `#temoignages` sur la home contient des
  emplacements clairement marqués `[à compléter]` : à remplacer par de vrais
  témoignages clients (nom, poste, entreprise) avant publication.
- **Mentions légales / Politique de confidentialité** — contiennent des
  champs entre crochets (SIRET, hébergeur, DPO, durées de conservation…) à
  compléter avec les informations juridiques réelles de Strivia.
- **Logos "Ils nous font confiance"** — la bande social proof utilise des
  tags sectoriels génériques (SaaS B2B, Cybersécurité…) plutôt que des logos
  clients réels. Dès que vous avez l'accord de vos clients pour afficher leur
  logo, remplacez `proof.sectors` (dans `content/_index.md`) par de vrais
  logos dans `.proof__tag`.
- **Prise de RDV** — la page `/contact/` est un texte simple (mailto). Vous
  pouvez y intégrer un widget Calendly / HubSpot Meetings à la place.

## Déploiement

Le site est 100% statique (`website/public/` après build) : déployable tel
quel sur Vercel, Netlify, Cloudflare Pages… en pointant la commande de build
sur `hugo --gc --minify` (root directory : `website`).
