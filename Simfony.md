you can pass variables to througt the url using this sintax
```php
#[Route('movies/{varName}',name:'movies',defaults:[varName => <defaulfValue>])]

pubblic function myFun($varName){
#rest of the code
}

```
you can access the variable, by specifyng a parameter in the function that this route points to, with the same name as the one we set between the brackets.

## 2
you can set a base.html.twig and you can extend it in blocks

in the child html we put this
```twig
{% extends "base.html.twig" %}

{% block <nomeBlocco> %}
{% endblock %}
```
## 3
you can define global variables in the twig.yaml

after default_path but not outside the parent, define "global:"
to define a variable
```yaml

varName:value
```

## 4
```sh
simfony console list doctrine
```

## 5
with simfony make:entity you can create a table in the database and a class

using "manyToOne" or "manyToMany" etc, will prompt you to link this field to another entity, then you will have the possibility to link to the othier side.

## Authentication

secutity-bundle required
simfony console make:registration-form
simfony console make:auth


# db
```php
$manager -> persist($entity)
```
serve per aggiungere l'entità alla lista di oggetti da modificare sul database.

```php
$manager->flush()
```
scrive i dati sul db

under the flush
```php
$this->addReference(<identifier>, $entity)
```

to add references to an object inside another object
```php
$entity->addOtherEntity($this->getReference(<otherEntityIdentifier>))
```

## repository
you can pass a repository as a parameter for function.

# refactoring
