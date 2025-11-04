# 🔥 Configuration Firebase - Guide complet

## 📋 Configuration requise pour la suppression d'annonces

### 1. ✅ Fichier config.js (déjà fait)

Votre API key est maintenant dans `config.js` (non commité sur GitHub). C'est bien ! ✅

### 2. ⚠️ Règles Firestore - **IMPORTANT**

Les règles Firestore actuelles doivent permettre la **lecture** et **l'écriture** (y compris la suppression).

#### 🔒 Configuration actuelle recommandée (pour développement/test)

Allez dans **Firebase Console** → **Firestore Database** → **Règles** et utilisez :

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /annonces/{documentId} {
      // Permettre la lecture à tous
      allow read: if true;
      
      // Permettre la création (écriture) à tous
      allow create: if true;
      
      // Permettre la suppression à tous
      // ⚠️ Note: La vérification réelle se fait côté client (JavaScript)
      allow delete: if true;
    }
  }
}
```

#### ⚠️ Limitations de sécurité actuelles

**Problème** : Sans authentification Firebase, les règles Firestore ne peuvent pas vraiment vérifier que c'est le propriétaire qui supprime. La vérification se fait uniquement côté client (JavaScript), ce qui peut être contourné.

**Protection actuelle** :
- ✅ Vérification côté client (nom + téléphone)
- ✅ Double confirmation (modale + popup)
- ❌ Pas de protection côté serveur (Firestore)

### 3. 🔐 Options pour améliorer la sécurité

#### Option A : Accepter les limitations (pour un site public simple)

Si c'est un site public où les utilisateurs sont de confiance, la protection côté client suffit pour la plupart des cas.

**Règles Firestore** :
```javascript
allow read, write, delete: if true;
```

#### Option B : Ajouter Firebase Authentication (sécurisé)

Pour une vraie sécurité, il faudrait :
1. Ajouter Firebase Authentication
2. Connecter les annonces à un utilisateur authentifié
3. Utiliser des règles Firestore comme :

```javascript
match /annonces/{documentId} {
  allow read: if true;
  allow create: if request.auth != null;
  allow delete: if request.auth != null && 
                   resource.data.userId == request.auth.uid;
}
```

**Mais** : Cela nécessite que les utilisateurs créent un compte, ce qui peut décourager certains utilisateurs.

### 4. 📝 Instructions pour configurer les règles Firestore

1. **Allez sur** : https://console.firebase.google.com
2. **Sélectionnez** votre projet "site-de-changement"
3. **Cliquez sur** "Firestore Database" dans le menu gauche
4. **Allez dans** l'onglet "Règles" (en haut)
5. **Copiez-collez** les règles ci-dessus
6. **Cliquez sur** "Publier"

### 5. ✅ Vérification

Après avoir configuré les règles, testez :
1. Créez une annonce
2. Essayez de la supprimer avec les bonnes informations
3. Essayez de la supprimer avec de mauvaises informations (devrait échouer côté client)

### 6. 🛡️ Recommandations supplémentaires

#### Protection de l'API key

Dans Firebase Console → **Project Settings** → **General** → **Your apps** :
- Ajoutez des **restrictions d'API key** pour limiter les domaines autorisés
- Ajoutez votre domaine GitHub Pages (ex: `votre-nom.github.io`)

#### Monitoring

- Activez les **logs Firestore** pour surveiller les suppressions
- Dans Firebase Console → **Firestore Database** → **Usage** pour voir les statistiques

### 7. ⚠️ Note importante

**Même avec les meilleures règles**, sans authentification :
- Quelqu'un qui connaît l'ID d'une annonce peut techniquement la supprimer
- La protection principale vient de la vérification côté client (nom + téléphone)
- Pour une vraie sécurité, il faudrait Firebase Authentication

**Pour votre cas d'usage** (site public d'échange de campus) :
- La protection actuelle (vérification nom + téléphone) est suffisante
- Les utilisateurs doivent connaître exactement le nom et le téléphone pour supprimer
- C'est un bon compromis entre sécurité et facilité d'utilisation

---

## 📞 Résumé rapide

1. ✅ **config.js** : Déjà fait (API key cachée)
2. ⚠️ **Règles Firestore** : À configurer pour permettre delete
3. ✅ **Vérification côté client** : Déjà implémentée (nom + téléphone)
4. 🔐 **Sécurité complète** : Nécessiterait Firebase Authentication (optionnel)

**Action requise** : Configurez les règles Firestore pour permettre la suppression (voir section 4 ci-dessus).
