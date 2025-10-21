# 📘 API Client Documentation

## 🔑 Authentification

Toutes les requêtes doivent inclure une clé API valide dans l’en-tête :

```
X-API-KEY: YOUR_SECRET_KEY
```

> ⚠️ Remplacer `YOUR_SECRET_KEY` par la clé envoyée via WhatsApp.

---

## 1️⃣ Vérifier l’existence d’un client

### **Endpoint**

```
GET /api/client/exist
```

### **Description**

Vérifie si un client existe dans la base de données à partir de son identifiant.

### **Paramètres**

| Nom        | Type | Obligatoire | Description                      |
| ---------- | ---- | ----------- | -------------------------------- |
| client\_id | int  | ✅ Oui       | Identifiant du client à vérifier |

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

| Code | Signification      |
| ---- | ------------------ |
| 200  | Succès             |
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

| Nom         | Type              | Obligatoire | Description                              |
| ----------- | ----------------- | ----------- | ---------------------------------------- |
| client\_id  | int               | ❌ Non       | ID du client spécifique                  |
| date\_start | date (YYYY-MM-DD) | ❌ Non       | Date de début pour filtrer les paiements |

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
            "nom": "OU****K",
            "prenom": "K*****a",
            "dateCreationClient": "2025-03-14 13:45:57",
            "DDP": "2025-10-01 12:16:07",
            "CA": "8000",
            "mg": "MG12",
            "rh": "Erh733 ILHAM ECHIHI",
            "YmD": "Y2509"
        }
    ]
}
```

#### Codes de retour possibles :

| Code | Signification      |
| ---- | ------------------ |
| 200  | Succès             |
| 400  | Paramètre invalide |
| 401  | Accès non autorisé |

---

## 3️⃣ Récupérer le chiffre d’affaires détaillé par client (nouveau format)

### **Endpoint**

```
GET /api/clients/ca-details
```

### **Description**

Retourne le chiffre d’affaires détaillé par client avec filtres dynamiques : date de début, date de fin, client id, nom, prénom, ville, centre (mg), responsable (rh), montant min/max.

### **Paramètres**

| Nom          | Type              | Obligatoire | Description                                             |
| ------------ | ----------------- | ----------- | ------------------------------------------------------- |
| client\_id   | int               | ❌ Non       | ID du client spécifique                                 |
| date\_start  | date (YYYY-MM-DD) | ❌ Non       | Date de début pour filtrer les paiements                |
| date\_end    | date (YYYY-MM-DD) | ❌ Non       | Date de fin pour filtrer les paiements                  |
| nom          | string            | ❌ Non       | Filtre par nom (partiel)                                |
| prenom       | string            | ❌ Non       | Filtre par prénom (partiel)                             |
| city         | string            | ❌ Non       | Filtre par ville du centre (partiel)                    |
| mg           | string            | ❌ Non       | Filtre par les 4 premiers caractères du titre du centre |
| rh           | string            | ❌ Non       | Filtre par responsable (Nom Prénom)                     |
| min\_tt\_mnt | float             | ❌ Non       | Montant minimum total des paiements                     |
| max\_tt\_mnt | float             | ❌ Non       | Montant maximum total des paiements                     |

### **Exemple de requête (AJAX / jQuery)**

```js
$.ajax({
  url: 'https://365965.center/epiltech/web/api/clients/ca-details',
  type: 'GET',
  data: {
    client_id: 671214076,
    date_start: '2025-01-01',
    date_end: '2025-10-21',
    city: 'Agadir'
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
            "nom": "OU****K",
            "prenom": "K*****a",
            "dateCreationClient": "2025-03-14 13:45:57",
            "date_naissance": "1998-01-22 00:00:00",
            "DPmt": "2025-03-14 13:45:57",
            "esp": "0",
            "cb": "0",
            "chq": "0",
            "tt_mnt": "0",
            "mg": "MG12",
            "rh": "Erh636 Mounia BENMEZINE",
            "Ymd": "Y2412",
            "city": "Agadir",
            "TDYNSh": "4",
            "TDYINST": "0"
        }
    ]
}
```

#### Codes de retour possibles :

| Code | Signification      |
| ---- | ------------------ |
| 200  | Succès             |
| 400  | Paramètre invalide |
| 401  | Accès non autorisé |

---

## ⚙️ Notes techniques

- Les routes sont sécurisées par clé API (`X-API-KEY`).
- Les requêtes doivent être de type **GET** (lecture seule).
- Le backend retourne des objets JSON structurés.
- Les dates sont au format `YYYY-MM-DD`.
- Les montants (`esp`, `cb`, `chq`, `tt_mnt`) incluent tous les modes de paiement, y compris les paiements échelonnés.
- `TDYNSh` et `TDYINST` indiquent respectivement le nombre de "No Show" et d'instances maximales par client.

