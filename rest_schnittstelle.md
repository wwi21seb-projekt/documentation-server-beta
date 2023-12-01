
## User Story 1
Als Nutzender möchte ich wissen, wer diese Webseite betreibt (Impressum), um den Inhaber erreichen zu können

Nur Implementierung im Frontend

### möglicher Endpoint
**URL**: `api/impressum`\
**Methode**: GET\
**Response**:
- **200** OK
```json
{
    "contact": "Max Mustermann",
    "address": "Große Str. 2, 68163 Mannheim",
    "email": "max.mustermann@domain.com",
    "info": "Weitere rechtlich relevante Informationen"
}
```

## User Story 2
Als Nutzer möchte ich mich mit Email und Passwort registrieren können, um einen gesicherten Zugang zu meinem Account zu haben und konfigurieren zu können

### 1. Endpoint
**URL**: `api/user`\
**Methode**: POST\
**Request**:
```json
{
    "email": "max.mustermann@domain.com",
    "password": "password123",
    "username": "maxmusti"
}
```
**Response**:
- **201** CREATED
```json
{
    "id": "UUID",
    "email": "max.mustermann@domain.com",
    "username": "maxmusti"
}
```
**Fehlercodes**: 
- **400** Bad Request (falscher Body, ungültige Email-Adresse, etc.)
- **409** Conflict (bereits genutzte Email oder genutzter Nutzername)        
- **500** Internal Server Error

### 2. Endpoint
**URL**: `api/user/login`\
**Methode**: POST\
**Request**:
```json
{
    "email": "max.mustermann@domain.com",
    "password": "password123"
}
```
**Response**:
- **204** No Content
  
**Fehlercodes**: 
- **400** Bad Request
- **401** Unauthorized
- **403** Forbidden (Account gesperrt)      
- **500** Internal Server Error

### 3. Endpoint
**URL**: `api/user`\
**Methode**: PUT\
**Request**:
```json
{
    "id": "UUID",
    "email": "max.mustermann@domain.com",
    "old_password": "password123",
    "new_password": "newpassword",
    "username": "maxmusti"
}
```
**Response**:
- **200** OK
```json
{
    "id": "UUID",
    "email": "max.mustermann@domain.com",
    "username": "maxmusti"
}
```
**Fehlercodes**: 
- **400** Bad Request
- **401** Unauthorized
- **500** Internal Server Error

## User Story 3
Als Nutzer möchte ich Texte posten können, um meine Gedanken zu teilen

### 1. Endpoint
**URL**: `api/posting`\
**Methode**: POST\
**Request**:
```json
{
    "user_id": "UUID",
    "text": "Lorem ipsum..."
}
```
**Response**:
- **201** CREATED
```json
{
    "id": "UUID",
    "created_at": "2023-11-28T12:00:00"
    "user_id": "UUID",
    "text": "Lorem ipsum..."
}
```
**Fehlercodes**: 
- **400** Bad Request
- **401** Unauthorized
- **403** Forbidden (Account gesperrt)
- **500** Internal Server Error

## User Story 4
Als Nutzer möchte ich die Möglichkeit haben, Hashtags zu verwenden, um meine Beiträge zu kategorisieren und leichter auffindbar zu machen

### 1. Endpoint
**URL**: `api/posting/hashtag/{hashtag}?page={page}&limit={limit}`\
**Methode**: GET\
**Querystrings**:
- **page**: Aktuelle Seite (Pagination)
- **limit**: Anzahl der Elemente auf einer Seite (Pagination)
  
**Response**:
- **200** OK
```json
{
    [
        {
        "id": "UUID",
        "created_at": "2023-11-28T12:00:00",
        "user": {
            "user_id": "UUID",
            "username": "maxmusti",
        },
        "text": "Lorem ipsum...",
        "image": "image"
        },
        ...
    ]
}
```
**Fehlercodes**: 
- **204** No Content (keine Posts zum gesuchten Hashtag)
- **400** Bad Request
- **401** Unauthorized

## User Story 5
Als Nutzer möchte ich Fotos hochladen können, um ...

Endpoint von User Story 4 wird überarbeitet

### 1. Endpoint
**URL**: `api/posting`\
**Methode**: POST\
**Request**:
```json
{
    "user_id": "UUID",
    "text": "Lorem ipsum...",
    "image": "image"
}
```
**Response**:
- **201** CREATED
```json
{
    "id": "UUID",
    "created_at": "2023-11-28T12:00:00"
    "user_id": "UUID",
    "text": "Lorem ipsum...",
    "image": "image"
}
```
**Fehlercodes**: 
- **400** Bad Request
- **401** Unauthorized
- **403** Forbiden (Account gesperrt)
- **500** Internal Server Error

## User Story 6
Als Nutzer möchte ich Beiträge kategorisiert filtern können, um nach bestimmten Beiträgen zu suchen

### 1. Endpoint
**URL**: `api/posting/user/{user_id}?start_date={start_date}&end_date={end_date}&page={page}&limit={limit}`\
**Methode**: GET\
**Querystrings**:
- **start_date**: Frühstes Erstellungsdatum
- **end_date**: Spätestes Erstellungsdatum
- **page**: Aktuelle Seite (Pagination)
- **limit**: Anzahl der Elemente auf einer Seite 
  
**Response**:
- **200** OK
```json
{
    [
        {
        "id": "UUID",
        "created_at": "2023-11-28T12:00:00",
        "user": {
            "user_id": "UUID",
            "username": "maxmusti",
        },
        "text": "Lorem ipsum...",
        "image": "image"
        },
        ...
    ]
}
```

### 2. Endpoint
**URL**: `api/posting/text/?search_string={search_string}&start_date={start_date}&end_date={end_date}&page={page}&limit={limit}`\
**Methode**: GET\
**Querystrings**:
- **search_string**: Text, nach dem in den Posts gesucht wird
- **start_date**: Frühstes Erstellungsdatum
- **end_date**: Spätestes Erstellungsdatum
- **page**: Aktuelle Seite (Pagination)
- **limit**: Anzahl der Elemente auf einer Seite 
  
**Response**:
- **200** OK
```json
{
    [
        {
        "id": "UUID",
        "created_at": "2023-11-28T12:00:00",
        "user": {
            "user_id": "UUID",
            "username": "maxmusti",
        },
        "text": "Lorem ipsum...",
        "image": "image"
        },
        ...
    ]
}
```
**Fehlercodes**: 
- **204** No Content (keine Posts zum gesuchten Hashtag)
- **400** Bad Request
- **401** Unauthorized

## User Story 7
Als Nutzer möchte ich Posts löschen können, um meine Veröffentlichungen rückgängig zu machen

### 1. Endpoint
**URL**: `api/posting/{id}`\
**Methode**: DELETE
  
**Response**:
- **204** No Content
  
**Fehlercodes**: 
- **401** Unauthorized
- **403** Forbidden (Post eines anderen Nutzers)
- **404** Not Found

## User Story 8
Als Nutzer möchte ich die Möglichkeit haben, andere Nutzer zu suchen und ihre persönlichen Nachrichten-Feeds anzeigen zu können und zu abonnieren

### 1. Endpoint
**URL**: `api/user?search_string={search_string}&page={page}&limit={limit}`\
**Methode**: GET\
**Querystrings**:
- **search_string**: Text, nach dem Benutzernamen gesucht wird
- **page**: Aktuelle Seite (Pagination)
- **limit**: Anzahl der Elemente auf einer Seite (Pagination)
  
**Response**:
- **200** OK
```json
{
    {
        "user_id": "UUID",
        "username": "maxmusti",
    },
    ...
}
```
**Fehlercodes**: 
- **204** No Content (keine Posts zum gesuchten Nutzernamen)
- **400** Bad Request
- **401** Unauthorized

### 2. Endpoint
**URL**: `api/user/{user_id}?page={page}&limit={limit}`\
**Methode**: GET\
**Querystrings**:
- **page**: Aktuelle Seite (Pagination)
- **limit**: Anzahl der Posts auf einer Seite (Pagination)
  
**Response**:
- **200** OK
```json
{
    "user_id": "UUID",
    "username": "maxmusti",
    "is_following": True, 
    "postings": [
        {
            "id": "UUID",
            "created_at": "2023-11-28T12:00:00"
            "text": "Lorem ipsum...",
            "image": "image"
        },
        ...
    ]
}   
```
**Fehlercodes**:
- **400** Bad Request
- **404** Not Found
- **401** Unauthorized

### 3. Endpoint
**URL**: `api/follow/{user_id}`
**Methode**: POST

**Response**:
- **200** OK
```json
{
    "follow_id": "UUID",
    "following_user_id": "UUID",
    "followed_user_id": "UUID",
}
```
**Fehlercodes**:
- **400** Bad Request
- **401** Unauthorized
- **404** Not Found

### 4. Endpoint
**URL**: `api/follow/{id}`\
**Methode**: DELETE
  
**Response**:
- **204** No Content
  
**Fehlercodes**: 
- **401** Unauthorized
- **403** Forbidden (Follow eines anderen Nutzers)
- **404** Not Found

## User Story 9
Als Nutzer möchte ich einen Feed haben, um neue Beiträge meiner Freunde sehen zu können

### 2. Endpoint
**URL**: `api/posting/feed/?page={page}&limit={limit}`\
**Methode**: GET
- **page**: Aktuelle Seite (Pagination)
- **limit**: Anzahl der Elemente auf einer Seite 
  
**Response**:
- **200** OK
```json
{
    [
        {
        "id": "UUID",
        "created_at": "2023-11-28T12:00:00",
        "user": {
            "user_id": "UUID",
            "username": "maxmusti",
        },
        "text": "Lorem ipsum...",
        "image": "image"
        },
        ...
    ]
}
```
**Fehlercodes**: 
- **204** No Content (keine Posts zum gesuchten Hashtag)
- **400** Bad Request
- **401** Unauthorized

## User Story 10
Als Nutzer möchte ich die Option haben, Nutzerprofile einzusehen und grundlegende Informationen über sie zu erhalten

siehe oben...