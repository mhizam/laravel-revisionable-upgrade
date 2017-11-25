# Laravel revisionable upgrade

Upgrade for the venturecraft revisionable package, add many useful methods. 
[Venturecraft Revisionable](https://github.com/VentureCraft/revisionable)

# Laravel versions

| Laravel Version | Package Tag | Supported | Development Branch
|-----------------|-------------|-----------| -----------|
| 5.2.x | 1.2.x | yes | 1.2
| <5.2 | - | no |

*versions for higher laravel versions comming soon

# How to use

1.Install package with composer
```
composer require fico7489/laravel-revisionable-upgrade:"*"
```
2.Use Fico7489\Laravel\RevisionableUpgrade\Traits\RevisionableUpgradeTrait trait in your base model or only in particular models. Model which use RevisionableUpgradeTrait must also use RevisionableTrait;

```
...
use Venturecraft\Revisionable\RevisionableTrait;
use Fico7489\Laravel\RevisionableUpgrade\Traits\RevisionableUpgradeTrait;

abstract class BaseModel extends Model
{
    use RevisionableTrait;
    use RevisionableUpgradeTrait;
    
    //enable this if you want use methods that gets information about creating
    protected $revisionCreationsEnabled = true;
...
```

and that's it, you are ready to go.

# Why to use

Yeah, revisionable package has userResponsible () method, but that is not enough and we can use saved revisions for much more useful stuff. We can find out who created and deleted model, who edited model, when the model was edited and much more. See below for more information.

# New methods

* **userCreated()**
Returns user which created this model
* **userDeleted()**
Returns user which deleted this model
* **userUpdated($key = null, $newValue = null, $oldValue = null)**
Returns user which updated this model (last user if there are more)


*  **revisionCreated()**
Returns revision for model created
*  **revisionDeleted()**
Returns revision for model deleted
* **revisionUpdated($key = null, $newValue = null, $oldValue = null)**
Returns revision for model updated (last revision if there are more)


* **dateUpdated($key = null, $newValue = null, $oldValue = null)**
Returns date for model updated (last revision if there are more)
* **revisionsUpdated($key = null, $newValue = null, $oldValue = null)**
Returns revisions for model updated
* **usersUpdated($key = null, $newValue = null, $oldValue = null)**
Returns users for model updated

Clarification for methods with **usersUpdated($key = null, $newValue = null, $oldValue = null)**

* All options are optional
* If you provide $key method will only look for changes on that key/field
* If you provide $newValue method will only look for changes where key/field is changed to this value
* If you provide $oldValue method will only look for changes where key/field is changed from this value

We don't need to create and delete methods for **dates** because information about this is stored in created_at and deleted_at.
We don't need to create and delete methods for **revisions** and **users** because only model can be created or deleted once.
Methods which returns **user** and **users** are using model from **auth.model** configuration.


# Why this package is usefull ?
You don't need to add foreign keys (e.g. author_id, created_user_id etc.) to your tables to connect users that edited, deleted or updated this model. You even don't need to use any package beacause if you are already using venturecraft revisionable all information that you need are already stored in revisions table.

# Improtant notes
Models where you want use this package must use created_at timestamp

If you want fetch users that have deleted models you must enable $revisionCreationsEnabled
```
protected $revisionCreationsEnabled = true;
```
[See more](https://github.com/VentureCraft/revisionable)

# Tests

All methods are covered with tests. If you run tests clone this package run "composer install" and just run : 

```
"vendor/bin/phpunit" tests
```

License
----

MIT


**Free Software, Hell Yeah!**