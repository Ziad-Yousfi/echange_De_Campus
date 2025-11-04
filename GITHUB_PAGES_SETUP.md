# 🚀 Configuration GitHub Pages - Guide

## ✅ Solution automatique (Déjà implémentée)

Le site a maintenant un **fallback automatique** : si `config.js` n'existe pas sur GitHub Pages, il utilisera la configuration directement dans `index.html`.

**Votre site devrait maintenant fonctionner sur GitHub Pages !** ✅

## 📝 Alternative : Créer config.js sur GitHub (Optionnel)

Si vous préférez garder les clés séparées, vous pouvez créer `config.js` directement sur GitHub :

### Méthode 1 : Via l'interface GitHub

1. Allez sur votre repository GitHub : `https://github.com/votre-nom/votre-repo`
2. Cliquez sur **"Add file"** → **"Create new file"**
3. Nommez le fichier : `config.js`
4. Copiez le contenu de votre `config.js` local
5. Cliquez sur **"Commit new file"**

⚠️ **Note** : Cela mettra vos clés API publiques sur GitHub. Pour un site public, c'est acceptable car l'API key Firebase est censée être publique.

### Méthode 2 : Via Git

Si vous voulez vraiment commiter `config.js` (non recommandé mais fonctionne) :

```bash
# Retirer config.js de .gitignore temporairement
git rm --cached .gitignore
# Ou modifier .gitignore pour ne plus exclure config.js

git add config.js
git commit -m "Ajouter config.js pour GitHub Pages"
git push
```

## 🔒 Sécurité

**Important** : L'API key Firebase est **publique par nature** et doit être visible côté client. C'est normal.

**Pour protéger votre projet** :
1. Dans Firebase Console → **Project Settings** → **API Restrictions**
2. Limitez votre API key aux domaines autorisés :
   - `votre-nom.github.io`
   - `localhost` (pour développement)
3. Activez les restrictions d'API

## ✅ Vérification

Après avoir mis à jour le code ou créé `config.js` :
1. Attendez quelques minutes (GitHub Pages met à jour le site)
2. Rechargez votre site : `https://ziad-yousfi.github.io`
3. Vérifiez la console du navigateur (F12) :
   - ✅ "Firebase initialisé avec succès"
   - ❌ Plus d'erreur "config.js non trouvé"

## 🎯 Résumé

**Option recommandée** : Utiliser le fallback automatique (déjà implémenté)
- ✅ Fonctionne immédiatement
- ✅ Pas besoin de créer config.js sur GitHub
- ✅ Les clés sont dans le code (normal pour Firebase)

**Alternative** : Créer config.js sur GitHub
- ✅ Garde les clés séparées
- ⚠️ Les clés seront publiques sur GitHub (mais c'est OK)

Votre site devrait maintenant fonctionner ! 🎉
