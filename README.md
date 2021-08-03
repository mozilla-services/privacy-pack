# privacy-pack
Mozilla privacy products under a single pack.

## Development
### Requirements
* python 3.7 (suggest using
  [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv))

### Install and Run the Site Locally
1. Clone and change to the directory:

    ```sh
    git clone https://github.com/mozilla-services/privacy-pack.git
    cd privacy-pack
    ```

2. Create and activate a virtual environment:

    ```sh
    pyenv virtualenv 3.7 privacy-pack
    pyenv activate privacy-pack
    ```

3. Install Python requirements:

    ```sh
    pip install -r requirements.txt
    ```

4. Copy `.env` file for
   [`decouple`](https://pypi.org/project/python-decouple/) config:

    ```sh
    cp .env-dist .env
    ```

5. Add a `SECRET_KEY` value to `.env`:

    ```ini
    SECRET_KEY=secret-key-should-be-different-for-every-install
    ```

6. Migrate DB:

    ```sh
    python manage.py migrate
    ```

7. Create superuser:

    ```sh
    python manage.py createsuperuser
    ```

8. Run it:

    ```sh
    python manage.py runserver
    ```

Next you'll need to enable Firefox Accounts auth ...

#### Enable Firefox Accounts Auth
To enable Firefox Accounts authentication on your local server, you can use the
"private-relay (local)" OAuth app on oauth-stable.dev.lcip.org.

To do so:

1. Set `ADMIN_ENABLED=True` in your `.env` file

2. Go to [the django admin page to change the default
   site](http://127.0.0.1:8000/admin/sites/site/1/change/).

3. Change `example.com` to `127.0.0.1:8000` and click Save.

4. [Go to the django-allauth social app admin
page](http://127.0.0.1:8000/admin/socialaccount/socialapp/), sign in with the
superuser account you created above, and add a social app for Firefox Accounts:

   * Provider: Firefox Accounts
   * Name: oauth-stable.dev.lcip.org
   * Client id: 9ebfe2c2f9ea3c58
   * Secret key: ping say-yawn for this
   * Sites: 127.0.0.1:8000 -> Chosen sites

Now you can sign into [http://127.0.0.1:8000/](http://127.0.0.1:8000/) with an
FxA. Remember: you'll need to use an account on oauth-stable.dev.lcip.org, not
the production accounts.firefox.com. For more instruction on setting up
django-allauth check this [document](https://dev.to/gajesh/the-complete-django-allauth-guide-la3).
