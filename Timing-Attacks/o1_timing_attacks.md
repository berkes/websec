!SLIDE title
# Timing Attacks #
(extra tijd)

!SLIDE code

    @@@ruby
    def password_digest(password)
      Bcrypt.create(password + SECRET)
    end

    def validate_login
      user = User.find_by(name: params[:username])
      if user
        raise InvalidLogin if user.password == password_digest
      end
    end

!SLIDE code

    @@@ruby
    def prevent_access_with_404
      if current_user.can_read_project?(params[:id])
        render Project.find(params[:id])
      else
        render_404
      end
    end

!SLIDE bullets incremental
# Oplossingen #

    @@@ruby
    def validate_login
      user = User.find_by(
        name: params[:username]
        password_digest: params[:password])
      raise InvalidLogin unless user
    end

!SLIDE bullets incremental
# Oplossingen #

* Randomness
* Pas op met performance optimalisatie.
* Heroden de executiepaden waar informatie kan lekken.
