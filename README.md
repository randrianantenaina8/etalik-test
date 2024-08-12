# Etalik - test

The project run with Symfony 7.1.3  with the following requirement : 

- php v8.3 or higher
- Mariadb v10

### - Clone the project
git clone https://github.com/randrianantenaina8/etalik-test.git




### - install the vendor libraries
get into your project root directory and execute the following command :
Run composer install to download the suitable vendors.  


```shell
$ composer install
```

### - Update the database schema
mettre à jour le fichier .env pour que le mot de passe mysql et la version de mariadb sur la ligne 31 DATABASE_URL="mysql://root:root@localhost:3306/roger_etalik?serverVersion=mariadb-10.5.19" soit compatible avec votre environnement

```shell
php bin/console doctrine:database:create
php bin/console make:migration
php bin/console doctrine:migrations:migrate
```

## Demarrer le serveur symfony
```shell
symfony serve
```

### - Test  application on browser
- Test on http://127.0.0.1:8000

- La page d'accueil ramène vers la page de création de produit
- la validation de cette page redirige vers la page liste des produits
- Sur la page liste des produits il y a des liens qui mène vers la page de création de produit ou la page fiche produit ou la page d'édition de produit
- La page d'édition de produit permet de modifier un produit ou de supprimer un produit et c contient un lien qui qui mène vers la page liste des produits

