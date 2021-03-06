EntityGenerator
===============

EntityGenerator transform Physical Data Model (optimized for MySql) from PowerAMC software to Doctrine's entities directly usable with Symfony 2.
EntityGenerator provide relations between entities with annotation.

For now, only manyToMany relations who own more than two relations dosen't work good.


How it work (quickly)
-----------
This project use Silex, the PHP micro-framework based on the Symfony2 Components.

From the MPD backup file of PowerDesigner (this is a flat XML), the EntityGenerator extract informations about tables models and her relations.
Is extract from tables models :
- table code (a unique identifier of the table name), comment
- columns name (a unique identifier of column name), type, length and comment

After extraction, EntityGenerator create entities files who for each parameters has his annotation for use with Doctrine 2.
And for each entity an EntityRepository is create.
With this entities files we can easily create database with Doctrine's commands lines.


EntityGenerator is only usable with commands lines.

If your MPD has ManyToMany relations who own more than two relations, EntityGenerator will tell you what relations will not be created.

Remember to check if the schema is correct with :
`php app/console doctrine:schema:validate`

[-> How it works in detail](src/Cnerta/EntityGeneratorBundle/Resources/doc/index.md)

What is ignored during transformation
-------------------------------------
- trigger
- view
- enum type (not yet implemented in Doctrine)


Install
-------
- Clone from here
- Install dependency with ```composer install``



Commands lines
--------------
Usage: `php console.php entity:generator --file="~/model.MPD" --namespace="a/name/space" --output="~/project/"`
- `--file` is the path of the PowerAMC PDM backup
- `--namespace` is the namespace for entities (use slash "/" instead of backslash "\\")
- `--output` is the path for the output folder


Change :
* [2013-10-02] :
    - add transformation for ternary entity who have one or more attributes
    - set null a parameter in the setter method if the attribute can be null
    - add a "BaseTest.mpd" file for test (src/Cnerta/EntityGeneratorBundle/Resources/doc)
* [2013-01-16] when a getter return an array, he is suffix with "List"
* [2012-05-22] chaining possibility on set methods
