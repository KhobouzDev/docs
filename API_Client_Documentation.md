
# 📘 API Client Documentation

## 🔑 Authentification
Toutes les requêtes doivent inclure une clé API valide dans l’en-tête :

```
X-API-KEY: YOUR_SECRET_KEY
```

> ⚠️ Remplacer `YOUR_SECRET_KEY` par la clé envoyer via whatsapp.

---

## 1️⃣ Vérifier l’existence d’un client

### **Endpoint**
```
GET /api/client/exist
```

### **Description**
Vérifie si un client existe dans la base de données à partir de son identifiant.

### **Paramètres**

| Nom         | Type   | Obligatoire | Description |
|--------------|--------|-------------|--------------|
| client_id    | int    | ✅ Oui       | Identifiant du client à vérifier |

### **Exemple de requête (AJAX / jQuery)**
```js
$.ajax({
  url: 'https://365965.center/epiltech/web/api/client/exist',
  type: 'GET',
  data: { client_id: 671214076 },
  headers: { 'X-API-KEY': 'YOUR_SECRET_KEY' },
  success: function(response) {
    if (response.exists) {
      console.log("✅ Client existe !");
    } else {
      console.log("❌ Client introuvable.");
    }
  }
});
```

### **Réponse**
```json
{
  "success": true,
  "exists": true,
  "client_id": 671214076
}
```

#### Codes de retour possibles :
| Code | Signification |
|------|----------------|
| 200  | Succès |
| 400  | Paramètre manquant |
| 401  | Accès non autorisé |

---

## 2️⃣ Récupérer le chiffre d’affaires total des clients

### **Endpoint**
```
GET /api/clients/ca-total
```

### **Description**
Retourne le chiffre d’affaires total par client, avec possibilité de filtrer par client id et/ou date de début.

### **Paramètres**

| Nom         | Type   | Obligatoire | Description |
|--------------|--------|-------------|--------------|
| client_id    | int    | ❌ Non       | ID du client spécifique |
| date_start   | date (YYYY-MM-DD) | ❌ Non | Date de début pour filtrer les paiements |

### **Exemple de requête (AJAX / jQuery)**
```js
$.ajax({
  url: 'https://365965.center/epiltech/web/api/clients/ca-total',
  type: 'GET',
  data: {
    client_id: 671214076,
    date_start: '2025-01-01'
  },
  headers: { 'X-API-KEY': 'YOUR_SECRET_KEY' },
  success: function(response) {
    if (response.success) {
      console.log("Résultats :", response.clients);
    } else {
      console.warn(response.message);
    }
  }
});
```

### **Réponse**
```json
{
    "success": true,
    "clients": [
        {
            "client_id": "671214076",
            "nom": "OUM****K",
            "prenom": "K***a",
            "dateCreationClient": "2025-03-14 13:45:57",
            "DDP": "2025-10-01 12:16:07",
            "CA": "8000"
        }
    ]
}
```

#### Codes de retour possibles :
| Code | Signification |
|------|----------------|
| 200  | Succès |
| 400  | Paramètre invalide |
| 401  | Accès non autorisé |

---

## ⚙️ Notes techniques
- Les routes sont sécurisées par clé API (`X-API-KEY`).  
- Les requêtes doivent être de type **GET** (lecture seule).  
- Le backend retourne des objets JSON structurés.  
- Les dates sont au format `YYYY-MM-DD`.
