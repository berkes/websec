!SLIDE bullets incremental
# Oplossingen #

* Escapen en sanitizen
* In rendering laag
* HTTP-only cookies
* Spagetti vermijden

!SLIDE bullets incremental
# Oplossingen #
 * `htmlspecialchars($email)`

!SLIDE code
    @@@php
    <?php print htmlspecialchars($email) ?>

    @@@php
    $message = "Please check <i>{$email}</i>";
    print htmlspecialchars($message);
    #=> Please check &lt;i&gt;example@example.com&lt;/i&gt;

!SLIDE bullets incremental
# Oplossingen #
* HTML-builders (HAML, SLIM, Markdown)
* Parse ook attributen
* Parse vooral ook data-attributen
* JSON-builders (NIET: `json_encode`)
* Javascript templates (coffee)
* CSS templates (LESS)

!SLIDE bullets incremental
# Oplossingen Architectuur #
* Laat rendering engine standaard escapen.
* Stuur de escape-status van variabelen mee.
* Maak onmogelijk om `print`, `echo` e.d aan te roepen.
* Maak het makkelijk om het goed te doen en moeilijk om het fout te
  doen.

!SLIDE code

Bad:

    @@@PHP
    <?php print $insecure; ?>

Good:

    @@@PHP
    <?php r($insecure); ?>
    <?php r($was_it_already_sanitized); ?>

!SLIDE code
Bad:

    @@@PHP
    $username = current_user()->name;
    $message = t('Successfully logged in %user', $username);

    <?php print check_plain($username); ?>
    <?php print $message; ?>

Good:

    @@@PHP
    <?php print check_plain($username); ?>
    <?php print check_plain($message); ?>

!SLIDE code
Beter:

    @@@PHP
    <?php r($username); ?>
    <?php r($message); ?>

!SLIDE code

   @@@PHP
   class View {
      function r($renderable) {
        if (!$renderable->is_sanitized()) {
          Sanitizer->sanitize($renderable);
        }
        print $renderable->content;
      }
    }
