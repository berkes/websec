!SLIDE bullets incremental
# Oplossingen #

* Implementeer GET/POST/PUT/PATCH/DELETE correct.
* Secret Token
* Same origin polcy middels Cookie-to-Header token

!SLIDE code

    @@@ruby
    def token
      env['rack.session'][key] ||= SecureRandom.base64(32)
    end

    def tag
      %Q(<input type="hidden" name="csrftoken" value="{token}" />)
    end

    def call(env)
      raise InvalidCsrfToken unless env.params[:csrftoken] == token
    end

!SLIDE code

Set-Cookie: Csrf-token=i8XNjC4b8KVok4uw5RftR38Wgp2BFwql; expires=Thu, 23-Jul-2015 10:25:33 GMT; Max-Age=31449600; Path=/

    @@@javascript
    var xhr = new XMLHttpRequest();
    xhr.open("POST", "http://example.com/transfer/", true);
    xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
    xhr.setRequestHeader("X-Csrf-Token", "i8XNjC4b8KVok4uw5RftR38Wgp2BFwql");
    xhr.send("amount=42&to=1337");

!SLIDE code
    @@@html
    <meta content="intwIVdk5ItyCj+ZdiQpTGBv2UBk4RQ5PwjkslscXig=" name="csrf-token" />

Uitleesbaar met:

    @@@javascript
    document.getElementsByTagName('meta').item(property='csrf-token');

!SLIDE bullets incremental
# Extra Oplossingen #

* Implementeer fail2ban voor patterns in url.
* CAPTCHAs
* 2factor

!SLIDE bullets incremental
# Geen oplossingen #
* referer checking
* POST gebruiken

!SLIDE bullets incremental
# Oplossingen Architectuur #
* Zorg voor XSRF afhandeling in middleware.
* (Zo laag mogelijk in de stack)
* Handel "params" generiek af, of ze nu geparste JSON of form-encoded
  oid zijn.
* Zorg voor goede salt in de randomgenerator (en zorg dat mensen deze
  veranderen)
* Niet limiteren tot formulieren. Binnen een sessie is veel soorten
  interactie mogelijk.
* Bied makkelijke helpers voor hidden forms, meta-tags en js-helpers.
