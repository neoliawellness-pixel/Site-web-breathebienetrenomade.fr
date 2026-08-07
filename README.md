# BREATHE — Bien-être Nomade

Site vitrine de BREATHE, massages à domicile, en entreprise et en van aménagé
à Ouistreham, Caen et dans tout le Calvados.

**En ligne :** https://www.breathebienetrenomade.fr

---

## Mise en ligne avec Vercel

1. Pousser **tout le contenu de ce dossier** à la racine d'un dépôt GitHub
   (le dossier `images/` doit bien apparaître dans le dépôt, avec ses 30 fichiers).
2. Sur vercel.com : **Add New → Project → Import** le dépôt.
3. Framework Preset : **Other**. Aucune commande de build, aucun dossier de sortie.
4. **Deploy**.
5. **Settings → Domains** : ajouter `www.breathebienetrenomade.fr`
   et `breathebienetrenomade.fr` (Vercel redirige automatiquement vers le www).

### Configuration DNS chez Ionos

Dans **Domaines & SSL → breathebienetrenomade.fr → DNS** :

| Type  | Nom  | Valeur                 |
|-------|------|------------------------|
| CNAME | www  | `cname.vercel-dns.com` |
| A     | @    | 76.76.21.21            |

Vercel affiche les valeurs exactes à l'écran : recopier celles-ci en priorité.
Le certificat HTTPS est généré automatiquement en quelques minutes.

Le fichier `vercel.json` applique les en-têtes de sécurité, le cache longue durée
sur les images et les redirections. Il est lu automatiquement à chaque déploiement.

-------|------|---------------------------|
| CNAME | www  | `<utilisateur>.github.io` |
| A     | @    | 185.199.108.153           |
| A     | @    | 185.199.109.153           |
| A     | @    | 185.199.110.153           |
| A     | @    | 185.199.111.153           |

Remplacer `<utilisateur>` par le nom du compte GitHub.
Compter jusqu'à 24 h de propagation, puis quelques minutes de plus
pour que le certificat HTTPS soit délivré.

---

## Modifier le site

Tout se trouve dans `index.html`. Le bloc de configuration est en bas du fichier :

```js
const WA            = "33615400972";        // WhatsApp (format international, sans +)
const EMPLACEMENT   = { lieu, ville, dates, note };   // à mettre à jour chaque semaine
const FACEBOOK_URL  = "...";
const INSTAGRAM_URL = "...";
const CALENDLY      = [ ... ];              // un lien Calendly par prestation
```

Après modification : commit + push. Le site se met à jour tout seul en 1 à 2 minutes.

---

## Structure

```
index.html                    page unique
404.html                      page d'erreur
CNAME                         domaine personnalisé
.nojekyll                     désactive le moteur Jekyll de GitHub
robots.txt / sitemap.xml      indexation Google
manifest.webmanifest          installation sur mobile
browserconfig.xml             tuiles Windows
favicon*.png / .ico           icônes du site
og-*.jpg                      aperçu lors des partages
images/                       photos en JPEG + WebP
```

---

## À faire avant / après la mise en ligne

- [ ] Remplacer les témoignages de la section **Avis** par de vrais retours clients
      (ils sont balisés en données structurées : des avis fictifs exposent à une
      pénalité manuelle de Google).
- [ ] Vérifier les identifiants Instagram et Facebook.
- [ ] Renommer les événements Calendly (`signature-1h`, `amma-assis-20min`),
      leurs adresses actuelles ne correspondent pas aux prestations.
- [ ] Déclarer le site sur **Google Search Console** et soumettre `sitemap.xml`.
- [ ] Créer une fiche **Google Business Profile** à Ouistreham.

---

## Notes techniques

- Aucune dépendance, aucun build : HTML, CSS et JS natifs.
- Images en WebP avec repli JPEG, `loading="lazy"` et dimensions déclarées (pas de décalage de mise en page).
- Polices chargées de façon non bloquante, image d'accueil préchargée.
- Données structurées Schema.org : `LocalBusiness`, `MassageTherapist`, `FAQPage`,
  `BreadcrumbList`, `WebSite`, `OfferCatalog`.
- Accessibilité : lien d'évitement, repères ARIA, contrastes conformes WCAG AA,
  navigation clavier complète, `prefers-reduced-motion` respecté.
- L'agenda Calendly n'est chargé qu'au moment où l'onglet est ouvert.
