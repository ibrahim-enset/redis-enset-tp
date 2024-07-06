# 1. Gestion des Sessions Utilisateurs
## 1:

     HSET session:123 user_id 123 name "John Doe" email "john.doe@example.com" login_date "2024-07-06"

## 2:

    HSET session:user:1001 email "john.doe@example.com"

## 3 :

    HGETALL session:user:1001


# 2. Stockage de Messages
## 1:

    RPUSH messages:user:1001 "Hello, how are you?"

## 2:

    RPUSH messages:user:1001 "I am doing well, thank you!"

## 3:

    LRANGE messages:user:1001 -3 -1

#  3. Gestion de Listes de Tâches
## 1:

    RPUSH tasks:user:1001 "Buy groceries" "Complete assignment" "Read a book"

## 2:

    RPUSH tasks:user:1001 "Go for a walk"
    
## 4:

    LREM tasks:user:1001 1 "Complete assignment"
    
## 5:

    LRANGE tasks:user:1001 0 -1
    
# 4. Classement des Utilisateurs
## 1:

    ZADD user:ranking 1000 "user1" 2000 "user2" 1500 "user3"

## 2:

    ZADD user:ranking 1200 "user4"


## 3:

    ZREVRANGE user:ranking 0 -1 WITHSCORES
## 4:

    ZREVRANK user:ranking "user3"

# 5. Suivi des Présences

## 1:

    SADD online:users 1001
## 2:

    SADD online:users 1002
    
## 3:

    SREM online:users 1001

## 4:

    SMEMBERS online:users

#  6. Utilisation des Données Géospatiales

## 1:

    GEOADD user:locations 13.361389 38.115556 "user1"
    
## 2:

    GEOADD user:locations 13.583333 37.316667 "user2" 13.583333 38.316667 "user3"

## 3:

    GEORADIUS user:locations 13.361389 38.115556 50 km
