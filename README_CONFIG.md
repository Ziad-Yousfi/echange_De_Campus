# 🔐 Configuration Firebase - Instructions

## Comment cacher votre API key sur GitHub

### ✅ Solution mise en place

1. **Fichier `config.js`** : Contient vos vraies clés (ne sera PAS commité sur GitHub)
2. **Fichier `config.example.js`** : Template vide (sera commité comme exemple)
3. **Fichier `.gitignore`** : Exclut `config.js` du repository

### 📋 Étapes pour utiliser cette solution

1. **Le fichier `config.js` existe déjà** avec vos clés actuelles
2. **Commitez sur GitHub** :
   ```bash
   git add .gitignore config.example.js index.html
   git commit -m "Cacher API key Firebase"
   git push
   ```
3. **Sur votre serveur/local** : Assurez-vous que `config.js` existe avec vos vraies clés

### ⚠️ IMPORTANT - À comprendre

**L'API key Firebase sera toujours visible côté client** car elle doit être dans le JavaScript qui s'exécute dans le navigateur. Cacher l'API key du repository GitHub :

- ✅ Protège votre clé des bots qui scanent GitHub
- ✅ Empêche les autres développeurs de voir votre clé dans le repo
- ❌ N'empêche PAS les utilisateurs finaux de voir la clé dans le code source du navigateur

### 🔒 Vraie sécurité : Règles Firestore

La **vraie sécurité** vient des **Règles Firestore** dans la console Firebase :

1. Allez sur https://console.firebase.google.com
2. Sélectionnez votre projet
3. Firestore Database → Règles
4. Configurez les règles pour limiter l'accès

### 🛡️ Protection supplémentaire (optionnel)

Dans Firebase Console → Project Settings → General :
- Configurez les **restrictions d'API key** pour limiter les domaines autorisés
- Ajoutez votre domaine GitHub Pages dans les restrictions

### 📝 Pour les autres développeurs

Si quelqu'un clone votre repo :
1. Copiez `config.example.js` en `config.js`
2. Remplissez avec vos propres clés Firebase
3. Le fichier `config.js` ne sera pas commité grâce à `.gitignore`
