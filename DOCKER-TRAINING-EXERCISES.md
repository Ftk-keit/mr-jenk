# 🐳 EXERCICES PRATIQUES DOCKER
## Formation Interactive - Projet mr-jenk

> **Instructions :** Complétez chaque exercice dans l'ordre. Copiez-collez vos commandes et résultats dans ce fichier. Je vérifierai vos réponses !

---

## 📋 NIVEAU 1 : COMMANDES DE BASE

### ✏️ Exercice 1.1 : Inspection des containers
**Tâche :** Listez tous vos containers en cours d'exécution avec SEULEMENT les colonnes : Nom, Status, Ports

**Votre commande :**
```bash
# Écrivez votre commande ici :
docker ps --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"

```

**Résultat attendu :** Tableau avec 10 containers

---

### ✏️ Exercice 1.2 : Logs en temps réel
**Tâche :** Affichez les 50 dernières lignes de logs du service `user-service` et suivez les nouveaux logs en temps réel (mode tail -f)

**Votre commande :**
```bash
# Écrivez votre commande ici :
docker logs -f --tail 50 mr-jenk-user-service

```

**Question bonus :** Comment arrêter le suivi des logs sans tuer le container ?
**Réponse :** on peut le faire par controle C ou mettre un timeout

---

### ✏️ Exercice 1.3 : Entrer dans un container
**Tâche :** Entrez dans le container MongoDB et listez le contenu du dossier `/data/db`

**Vos commandes :**
```bash
# Commande 1 - Entrer dans MongoDB :
docker exec -it mr-jenk-mongo-database sh

# Commande 2 - Lister /data/db (depuis l'intérieur du container) :
ls /data/db

# Commande 3 - Sortir du container :
exit

```

---

### ✏️ Exercice 1.4 : Stats de consommation
**Tâche :** Affichez la consommation CPU et RAM de tous vos containers, triés par consommation RAM (du plus gourmand au moins)

**Votre commande :**
```bash
# Écrivez votre commande ici :
docker stats --no-stream --format "table {{.Name}}\t{{.CPUPerc}}\t{{.MemUsage}}" | sort -n -k3 -r
```

**Question :** Quel est le container le plus gourmand en RAM ?
**Réponse :** c'est mr-jenk-kafka2-1

---

## 🌐 NIVEAU 2 : RÉSEAUX DOCKER

### ✏️ Exercice 2.1 : Inspection du réseau
**Tâche :** Affichez tous les containers connectés au réseau `mr-jenk_buy01-network` avec leurs adresses IP

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

**Question :** Quelle est l'adresse IP de `eureka-server` ?
**Réponse :**

---

### ✏️ Exercice 2.2 : Test de connectivité interne
**Tâche :** Depuis le container `api-gateway`, faites un `curl` vers `user-service` sur le port 8081 pour vérifier la santé du service

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

**Résultat attendu :** `{"status":"UP"}` ou similaire

---

### ✏️ Exercice 2.3 : Test de connectivité externe
**Tâche :** Depuis votre PC (hôte), essayez d'accéder directement au port 8081 (user-service) avec curl

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

**Question :** Pourquoi ça ne fonctionne pas ?
**Réponse :**

---

### ✏️ Exercice 2.4 : DNS Docker
**Tâche :** Depuis le container `user-service`, utilisez `ping` ou `nslookup` pour résoudre le nom `mongodb` en adresse IP

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

**Question :** Le nom `mongodb` se résout-il automatiquement ? Pourquoi ?
**Réponse :**

---

## 💾 NIVEAU 3 : VOLUMES ET PERSISTANCE

### ✏️ Exercice 3.1 : Liste des volumes
**Tâche :** Listez tous les volumes Docker de votre système

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

**Question :** Combien de volumes sont utilisés par le projet `mr-jenk` ?
**Réponse :**

---

### ✏️ Exercice 3.2 : Inspection d'un volume
**Tâche :** Affichez les détails du volume `mr-jenk_mongodb_data` (chemin de montage, taille, driver)

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

**Question :** Où est stocké physiquement ce volume sur votre disque ?
**Réponse :**

---

### ✏️ Exercice 3.3 : Test de persistance
**Tâche :** 
1. Arrêtez le container MongoDB
2. Redémarrez-le
3. Vérifiez que les données sont toujours là

**Vos commandes :**
```bash
# 1. Arrêter MongoDB :


# 2. Vérifier que c'est arrêté :


# 3. Redémarrer MongoDB :


# 4. Vérifier que les données persistent (taille de /data/db) :


```

**Question :** Les données ont-elles été conservées ?
**Réponse :**

---

### ✏️ Exercice 3.4 : Création d'un volume
**Tâche :** Créez un nouveau volume nommé `test-backup` et inspectez-le

**Vos commandes :**
```bash
# 1. Créer le volume :


# 2. Vérifier qu'il existe :


# 3. Supprimer le volume (nettoyage) :


```

---

## 🏗️ NIVEAU 4 : DOCKER COMPOSE

### ✏️ Exercice 4.1 : Restart d'un service
**Tâche :** Redémarrez UNIQUEMENT le service `eureka-server` avec Docker Compose (pas `docker restart`)

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

---

### ✏️ Exercice 4.2 : Logs de plusieurs services
**Tâche :** Affichez les logs de `eureka-server` ET `api-gateway` en même temps avec Docker Compose

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

---

### ✏️ Exercice 4.3 : Scaling (si applicable)
**Tâche :** Essayez de scaler le service `user-service` à 2 instances

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

**Question :** Est-ce que ça fonctionne ? Pourquoi ou pourquoi pas ?
**Réponse :**

---

### ✏️ Exercice 4.4 : Rebuild d'un service
**Tâche :** Rebuild UNIQUEMENT l'image du service `product-service` (sans toucher aux autres)

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

---

## 🔒 NIVEAU 5 : SÉCURITÉ ET CONFIGURATION

### ✏️ Exercice 5.1 : Vérification des permissions
**Tâche :** Vérifiez les permissions du fichier `.env`

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

**Question :** Les permissions sont-elles sécurisées (600 ou 400) ?
**Réponse :**

---

### ✏️ Exercice 5.2 : Variables d'environnement
**Tâche :** Affichez toutes les variables d'environnement du container `user-service` et comptez-les

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

**Question :** Combien de variables d'environnement sont définies ?
**Réponse :**

---

### ✏️ Exercice 5.3 : Healthcheck status
**Tâche :** Affichez le statut de santé (health status) de tous vos containers

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

**Question :** Combien de containers ont un healthcheck configuré ?
**Réponse :**

---

### ✏️ Exercice 5.4 : Restart policy
**Tâche :** Vérifiez la politique de restart de chaque container

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

**Question :** Quelle politique est utilisée pour `eureka-server` ?
**Réponse :**

---

## 🚀 NIVEAU 6 : OPTIMISATION ET BUILD

### ✏️ Exercice 6.1 : Taille des images
**Tâche :** Listez toutes vos images Docker avec leur taille, triées de la plus grosse à la plus petite

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

**Question :** Quelle est l'image la plus volumineuse ?
**Réponse :**

---

### ✏️ Exercice 6.2 : Analyse des layers
**Tâche :** Affichez l'historique des layers de l'image `mr-jenk-eureka-server`

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

**Question :** Combien de layers compose cette image ?
**Réponse :**

---

### ✏️ Exercice 6.3 : Nettoyage système
**Tâche :** Listez tout ce qui peut être nettoyé (images inutilisées, containers arrêtés, volumes orphelins) SANS rien supprimer

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

**Question :** Combien d'espace disque pourrait être libéré ?
**Réponse :**

---

### ✏️ Exercice 6.4 : Build avec cache
**Tâche :** Rebuild l'image `eureka-server` et observez quelles layers utilisent le cache

**Votre commande :**
```bash
# Écrivez votre commande ici :


```

**Question :** Combien de layers ont utilisé le cache (---> Using cache) ?
**Réponse :**

---

## 🎯 NIVEAU 7 : SCÉNARIOS RÉELS

### ✏️ Exercice 7.1 : Simulation de crash
**Tâche :** 
1. Tuez brutalement le processus Java dans le container `product-service`
2. Observez si le container redémarre automatiquement
3. Vérifiez les logs pour voir ce qui s'est passé

**Vos commandes :**
```bash
# 1. Tuer le processus Java :


# 2. Observer le restart (immédiatement après) :


# 3. Vérifier les logs :


```

**Question :** Le container a-t-il redémarré automatiquement ? Combien de temps ça a pris ?
**Réponse :**

---

### ✏️ Exercice 7.2 : Backup MongoDB
**Tâche :** Créez un backup de MongoDB dans le dossier `./backups` de votre projet

**Vos commandes :**
```bash
# 1. Créer le dossier backups :


# 2. Faire le backup MongoDB :


# 3. Vérifier que le backup existe :


```

---

### ✏️ Exercice 7.3 : Mise à jour Rolling
**Tâche :** Simulez une mise à jour du service `user-service` :
1. Arrêtez le service
2. Rebuild l'image
3. Redémarrez le service

**Vos commandes :**
```bash
# 1. Arrêter user-service :


# 2. Rebuild l'image :


# 3. Redémarrer le service :


```

**Question :** Combien de temps le service a été indisponible ?
**Réponse :**

---

### ✏️ Exercice 7.4 : Debug d'un service qui ne répond pas
**Tâche :** Si `api-gateway` ne répond pas, quelle série de commandes utiliseriez-vous pour diagnostiquer ?

**Votre checklist de debug :**
```bash
# 1. Vérifier si le container tourne :


# 2. Vérifier les logs récents :


# 3. Vérifier la santé du service :


# 4. Vérifier la connectivité réseau vers eureka :


# 5. Vérifier les variables d'environnement :


# 6. Vérifier les ressources (CPU/RAM) :


```

---

## 🏆 DÉFI FINAL : Projet Mini

### ✏️ Exercice BONUS : Ajout d'un nouveau service
**Tâche :** Ajoutez un service Redis cache à votre docker-compose.yml

**Spécifications :**
- Image : `redis:7-alpine`
- Container name : `mr-jenk-redis`
- Port : 6379 (non exposé à l'extérieur)
- Réseau : `buy01-network`
- Volume : `redis_data:/data`
- Restart : `unless-stopped`
- Healthcheck : `redis-cli ping`

**Votre configuration (ajout dans docker-compose.yml) :**
```yaml
# Écrivez votre configuration ici :




```

**Commandes pour tester :**
```bash
# 1. Démarrer le nouveau service :


# 2. Vérifier qu'il tourne :


# 3. Tester depuis un autre container :


# 4. Nettoyer (supprimer le service) :


```

---

## 📊 RÉSUMÉ DE VOS RÉSULTATS

**Niveau 1 (Base) :** __ / 4 exercices complétés
**Niveau 2 (Réseaux) :** __ / 4 exercices complétés
**Niveau 3 (Volumes) :** __ / 4 exercices complétés
**Niveau 4 (Compose) :** __ / 4 exercices complétés
**Niveau 5 (Sécurité) :** __ / 4 exercices complétés
**Niveau 6 (Optimisation) :** __ / 4 exercices complétés
**Niveau 7 (Scénarios) :** __ / 4 exercices complétés
**Défi Final :** __ / 1 complété

**SCORE TOTAL : __ / 29**

---

## 🎓 Barème d'évaluation

- **0-10** : Débutant - Continuez à pratiquer les bases
- **11-15** : Intermédiaire - Bonne compréhension des concepts
- **16-20** : Avancé - Vous maîtrisez Docker Compose
- **21-25** : Expert - Prêt pour la production
- **26-29** : Maître Docker - Vous pouvez enseigner aux autres ! 🏆

---

## 📝 Notes et Questions

**Vos questions pendant les exercices :**




**Difficultés rencontrées :**




**Ce que vous avez appris :**




---

> **Prochaine étape :** Une fois terminé, envoyez-moi ce fichier et je vous donnerai des feedbacks détaillés sur chaque exercice ! 🚀
