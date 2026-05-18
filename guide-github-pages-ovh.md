# 🚀 Guide — studiomaths.fr → GitHub Pages

**Objectif :** faire pointer `studiomaths.fr` (OVH) vers
`https://samir-chikhi.github.io/cours-particulier-NK/`

**Durée totale :** ~20 minutes de manipulation + 24h de propagation DNS max
(souvent moins de 2h)

---

## Vue d'ensemble du mécanisme

```
Visiteur tape studiomaths.fr
        ↓
  OVH DNS (votre config)
        ↓
  GitHub Pages (hébergement)
        ↓
  Affiche index.html du repo
```

---

## PARTIE 1 — GitHub (10 minutes)

### Étape 1 — Déposer le fichier CNAME dans le repo

Le fichier `CNAME` (sans extension) indique à GitHub quel domaine utiliser.

**Son contenu :** une seule ligne → `studiomaths.fr`

**Comment l'ajouter :**

1. Allez sur → https://github.com/samir-chikhi/cours-particulier-NK
2. Cliquez sur **"Add file"** → **"Create new file"**
3. Dans le champ nom, tapez exactement : `CNAME`  *(majuscules, sans extension)*
4. Dans le corps du fichier, tapez : `studiomaths.fr`
5. En bas → **"Commit changes"** → **"Commit directly to main"** → **"Commit"**

> ⚠️ Ce fichier doit être à la racine du repo, au même niveau que `index.html`.

---

### Étape 2 — Déposer/mettre à jour index.html et les logos

Si ce n'est pas déjà fait, uploadez dans le repo :

1. Cliquez sur **"Add file"** → **"Upload files"**
2. Glissez-déposez ces fichiers :
   - `index.html` *(le fichier mis à jour avec le SEO)*
   - `logo-studio-maths-icone.png`
   - `logo-studio-maths-horizontal.jpg`
3. Cliquez **"Commit changes"**

---

### Étape 3 — Activer GitHub Pages avec domaine personnalisé

1. Dans le repo → cliquez sur ⚙️ **"Settings"** (en haut à droite)
2. Dans le menu gauche → cliquez sur **"Pages"**
3. Section **"Build and deployment"** :
   - **Source** : `Deploy from a branch`
   - **Branch** : `main` · `/ (root)`
   - Cliquez **"Save"**
4. Section **"Custom domain"** :
   - Dans le champ, tapez : `studiomaths.fr`
   - Cliquez **"Save"**
5. ✅ GitHub affiche : *"Your site is ready to be published at https://studiomaths.fr"*
6. Cochez **"Enforce HTTPS"** (si la case est disponible — sinon revenir après la config DNS)

---

## PARTIE 2 — OVH DNS (10 minutes)

> 🔑 Connectez-vous sur https://www.ovhcloud.com/fr/ → Espace client

### Étape 4 — Accéder à la zone DNS du domaine

1. Menu gauche → **"Web Cloud"** → **"Noms de domaine"**
2. Cliquez sur **`studiomaths.fr`**
3. Onglet **"Zone DNS"**

---

### Étape 5 — Supprimer les anciennes entrées A et CNAME

Avant d'ajouter les nouvelles entrées, supprimez les enregistrements existants qui pourraient créer des conflits :

Cherchez et **supprimez** (icône corbeille) les entrées de type :
- `A` avec pour nom `@` ou vide (entrée racine)
- `A` avec pour nom `www`
- `CNAME` avec pour nom `www`

> ⚠️ Ne supprimez **pas** les entrées de type `MX` (emails) ni `TXT` (vérifications).

---

### Étape 6 — Ajouter les 4 entrées A (IPv4 GitHub Pages)

Cliquez sur **"Ajouter une entrée"** → choisissez **"A"**

Ajoutez ces 4 enregistrements **un par un** (ce sont les IPs officielles de GitHub Pages) :

| Type | Sous-domaine | Cible (IP) | TTL |
|------|-------------|------------|-----|
| A | *(laisser vide ou mettre @)* | `185.199.108.153` | 3600 |
| A | *(laisser vide ou mettre @)* | `185.199.109.153` | 3600 |
| A | *(laisser vide ou mettre @)* | `185.199.110.153` | 3600 |
| A | *(laisser vide ou mettre @)* | `185.199.111.153` | 3600 |

> Ces IPs appartiennent à GitHub — elles ne changent pas.

---

### Étape 7 — Ajouter l'entrée CNAME pour www

Cliquez sur **"Ajouter une entrée"** → choisissez **"CNAME"**

| Type | Sous-domaine | Cible | TTL |
|------|-------------|-------|-----|
| CNAME | `www` | `samir-chikhi.github.io.` | 3600 |

> ⚠️ N'oubliez pas le **point final** après `.io` dans le champ cible.

---

### Étape 8 — Confirmer et attendre la propagation

1. Cliquez **"Valider"** pour chaque entrée
2. OVH vous demandera de confirmer → validez
3. ⏳ Attendez **1 à 24h** (généralement 1 à 2h)

---

## PARTIE 3 — Vérifications

### Vérifier la propagation DNS (depuis votre navigateur)

Tapez dans la barre d'adresse :
```
https://studiomaths.fr
```

Si le site s'affiche → ✅ tout fonctionne.

### Outil de vérification DNS (si vous voulez contrôler)

Allez sur → https://dnschecker.org
- Entrez `studiomaths.fr`
- Vérifiez que les 4 IPs GitHub apparaissent en vert partout dans le monde

### Activer HTTPS sur GitHub (si pas encore fait)

1. Retournez dans Settings → Pages
2. Si la case **"Enforce HTTPS"** est maintenant disponible → cochez-la
3. ✅ Votre site sera accessible en `https://studiomaths.fr`

---

## PARTIE 4 — Google Search Console

Pour que Google indexe `studiomaths.fr` (et non l'ancienne URL GitHub) :

1. Allez sur → https://search.google.com/search-console
2. **"Ajouter une propriété"** → **"Préfixe d'URL"**
3. Entrez : `https://studiomaths.fr/`
4. Méthode de vérification recommandée : **"Balise HTML"**
5. Copiez la balise fournie par Google :
   ```html
   <meta name="google-site-verification" content="VOTRE_CODE_ICI">
   ```
6. Ajoutez-la dans `index.html` juste après la ligne `<meta name="theme-color"...>`
7. Uploadez le `index.html` mis à jour sur GitHub
8. Revenez sur Search Console → **"Vérifier"**
9. Une fois vérifié → menu gauche → **"URL Inspection"** → entrez `https://studiomaths.fr/` → **"Demander l'indexation"**

---

## Récapitulatif — Checklist

**GitHub :**
- [ ] Fichier `CNAME` créé à la racine du repo avec `studiomaths.fr`
- [ ] `index.html` mis à jour uploadé
- [ ] Logos uploadés (`logo-studio-maths-icone.png`, `logo-studio-maths-horizontal.jpg`)
- [ ] GitHub Pages activé (Settings → Pages → branch main)
- [ ] Domaine personnalisé renseigné dans GitHub Pages
- [ ] "Enforce HTTPS" coché

**OVH :**
- [ ] Anciennes entrées A et CNAME supprimées
- [ ] 4 entrées A ajoutées (IPs GitHub)
- [ ] Entrée CNAME www ajoutée
- [ ] Propagation DNS attendue (1 à 24h)

**Vérification :**
- [ ] `https://studiomaths.fr` affiche le site
- [ ] `https://www.studiomaths.fr` redirige aussi
- [ ] Google Search Console configuré et indexation demandée

---

## ❓ Problèmes fréquents

| Problème | Cause probable | Solution |
|----------|---------------|----------|
| Page 404 GitHub | `index.html` pas à la racine du repo | Vérifier dans GitHub que le fichier est au niveau racine |
| "Domain already taken" dans GitHub Pages | Un autre repo utilise ce domaine | Supprimer le CNAME de l'autre repo d'abord |
| Site OVH par défaut visible | Propagation DNS pas terminée | Attendre 2h et vider le cache navigateur |
| HTTPS non disponible | DNS pas encore propagé | Revenir après propagation et cocher "Enforce HTTPS" |
| Logos absents | Fichiers PNG/JPG non uploadés sur GitHub | Vérifier que les 3 fichiers sont dans le repo |

---

*Guide rédigé pour Studio Maths · studiomaths.fr · Mai 2026*
