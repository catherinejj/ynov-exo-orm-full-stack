# Gestion des Migrations avec Entity Framework dans un Projet .NET

## Objectif
Cet exercice a pour but de vous familiariser avec la gestion des migrations dans un projet .NET utilisant Entity Framework Core.

## Prérequis
- .NET SDK installé
- Entity Framework Core installé dans le projet
- Une base de données configurée

## Étapes à Suivre

### 1. Création d'une Migration Vide
Nous commençons par créer une migration vide nommée `Empty` :
```bash
 dotnet ef migrations add Empty
```
Cette migration ne contient aucun changement structurel, mais elle servira de point de retour ultérieur.

### 2. Création d'une Migration pour Ajouter des Tables
Nous créons ensuite une nouvelle migration pour ajouter des tables, par exemple `Users` et `Products` :
```bash
 dotnet ef migrations add AddUsersAndProducts
```
Cette migration générera automatiquement le code nécessaire pour modifier la base de données en fonction des modifications apportées au modèle.

### 3. Application des Migrations
Nous appliquons les migrations à la base de données :
```bash
 dotnet ef database update
```
Cela mettra à jour la base de données en appliquant toutes les migrations disponibles.

### 4. Suppression de la Dernière Migration
Nous devons maintenant annuler la dernière migration avant qu'elle ne soit appliquée.
```bash
 dotnet ef migrations remove
```
Cette commande supprimera la dernière migration (dans ce cas, `AddUsersAndProducts`), mais uniquement si elle n'a pas encore été appliquée à la base de données.

### 5. Retour à la Migration Vide
Nous revenons à l'état de la base de données correspondant à la migration `Empty` :
```bash
 dotnet ef database update Empty
```
Cela restaure la base de données à son état initial.

### 6. Suppression de la Migration `AddUsersAndProducts`
Enfin, nous supprimons complètement la migration `AddUsersAndProducts` si elle est toujours présente dans le dossier `Migrations` :
```bash
 rm -rf Migrations/AddUsersAndProducts*
```

## Vérification
- Assurez-vous que la migration `AddUsersAndProducts` a bien été supprimée.
- Vérifiez que la base de données est revenue à l'état de la migration `Empty`.
- Confirmez que le dossier `Migrations` ne contient plus de traces de la migration supprimée.

## Résumé
- Création d'une migration vide (`Empty`)
- Ajout d'une migration avec des modifications (`AddUsersAndProducts`)
- Application des migrations
- Suppression de la dernière migration avant son application
- Retour à la migration vide
- Suppression définitive de `AddUsersAndProducts`

## Notes
Si la migration `AddUsersAndProducts` a déjà été appliquée, il faudra d'abord rétrograder la base de données avec :
```bash
 dotnet ef database update Empty
```
avant de pouvoir la supprimer avec `dotnet ef migrations remove`.
