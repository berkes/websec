!SLIDE bullets incremental
# Oplossingen #

* ORM
* Prepared Statements
* Escapen
* Permissions op Database

!SLIDE bullets incremental
# Oplossingen #
## ORM, database abstractielaag ##

    @@@ruby
    user = User.find(1337)
    user.update_attributes(email: email)

    Account.where('name LIKE ?', pattern)

!SLIDE bullets incremental
# Oplossingen #
## Prepared Statement ##

    @@@sql
    PREPARE user (int) AS
      SELECT * FROM users WHERE id = $1);

    EXECUTE user(1);

!SLIDE bullets incremental
# Oplossingen #
## Escapen ##
* Gebruik een ORM of Datbase-abstractielaag.
* Vervang bijvoorbeeld `'` met `\'`. *en meer*

!SLIDE bullets incremental
# Oplossingen #
## Permissies op Database ##

* CMS met user `drupal_cms` heeft schrijfrechten.
* frontend met user `drupal_frontend` heeft read-only rechten.

!SLIDE bullets incremental
# Oplossingen Architectuur #
* Zorg voor een goed, veelgebruikt ORM.
* Druk dit zo laag mogelijk de stack in.
* Maak het moeilijk om fout te doen en makkelijk om goed te doen.
* Zorg voor één, voorspelbare plek.
