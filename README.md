1. Gestion des Sessions Utilisateurs
Problématique : Stocker et gérer les informations de session des utilisateurs.

Tâches :

Créez une clé de session pour un utilisateur avec son ID, contenant ses informations de connexion (nom, email, date de connexion).

sh
Copy code
HMSET session:user:1001 name "John Doe" email "john@example.com" date "2024-07-06"
Mettez à jour l'email de l'utilisateur.

sh
Copy code
HSET session:user:1001 email "john.doe@example.com"
Récupérez toutes les informations de la session pour cet utilisateur.

sh
Copy code
HGETALL session:user:1001
2. Stockage de Messages
Problématique : Stocker et récupérer les messages envoyés par les utilisateurs.

Tâches :

Utilisez une liste pour stocker les messages envoyés par un utilisateur.

sh
Copy code
RPUSH messages:user:1001 "Hello, how are you?"
Ajoutez un autre message à la liste.

sh
Copy code
RPUSH messages:user:1001 "I am doing well, thank you!"
Récupérez les 3 derniers messages pour cet utilisateur.

sh
Copy code
LRANGE messages:user:1001 -3 -1
3. Gestion de Listes de Tâches
Problématique : Gérer les listes de tâches des utilisateurs.

Tâches :

Créez une liste pour stocker les tâches d'un utilisateur.

sh
Copy code
RPUSH tasks:user:1001 "Buy groceries" "Complete assignment" "Read a book"
Ajoutez plusieurs tâches à la liste.

sh
Copy code
RPUSH tasks:user:1001 "Go for a walk"
Marquez une tâche comme complétée (retirez-la de la liste).

sh
Copy code
LREM tasks:user:1001 1 "Complete assignment"
Récupérez toutes les tâches restantes pour cet utilisateur.

sh
Copy code
LRANGE tasks:user:1001 0 -1
4. Classement des Utilisateurs
Problématique : Gérer un classement des utilisateurs basé sur un score.

Tâches :

Utilisez un ensemble trié (sorted set) pour stocker les scores des utilisateurs.

sh
Copy code
ZADD user:ranking 1000 "user1" 2000 "user2" 1500 "user3"
Ajoutez des scores pour plusieurs utilisateurs.

sh
Copy code
ZADD user:ranking 1200 "user4"
Récupérez le classement des utilisateurs par score.

sh
Copy code
ZREVRANGE user:ranking 0 -1 WITHSCORES
Récupérez la position d'un utilisateur spécifique dans le classement.

sh
Copy code
ZREVRANK user:ranking "user3"
5. Suivi des Présences
Problématique : Suivre quels utilisateurs sont actuellement en ligne.

Tâches :

Utilisez un ensemble pour stocker les ID des utilisateurs actuellement en ligne.

sh
Copy code
SADD online:users 1001
Ajoutez un utilisateur à l'ensemble lorsqu'il se connecte.

sh
Copy code
SADD online:users 1002
Retirez un utilisateur de l'ensemble lorsqu'il se déconnecte.

sh
Copy code
SREM online:users 1001
Récupérez la liste des utilisateurs actuellement en ligne.

sh
Copy code
SMEMBERS online:users
6. Utilisation des Données Géospatiales
Problématique : Permettre aux utilisateurs de partager leur position géographique et de rechercher d'autres utilisateurs à proximité.

Tâches :

Utilisez des données géospatiales pour stocker la position des utilisateurs.

sh
Copy code
GEOADD user:locations 13.361389 38.115556 "user1"
Ajoutez des positions pour plusieurs utilisateurs.

sh
Copy code
GEOADD user:locations 13.583333 37.316667 "user2" 13.583333 38.316667 "user3"
Recherchez les utilisateurs dans un rayon de 50 km autour d'une position donnée.

sh
Copy code
GEORADIUS user:locations 13.361389 38.115556 50 km
