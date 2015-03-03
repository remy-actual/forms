[![Build Status](https://travis-ci.org/asm-products/formspree.svg?branch=master)](https://travis-ci.org/asm-products/formspree)

Functional HTML forms. Hosted at [http://formspree.io](http://formspree.io).

Just send your form to our URL and we'll forward it to your email. No PHP, Javascript or sign up required — perfect for static sites!
Example:

    <form action="//formspree.io/you@email.com">
        <input type="text" name="name">
        <input type="email" name="_replyto">
        <input type="submit" value="Send">
    </form>

Setting it up is easy and free. Here's how:

You don't even have to register.

## 1. Setup the HTML form

Change your form's action-attribute to this and replace your@email.com with your own email.

## 2. Submit the form and confirm your email address

Go to your website and submit the form once. This will send you an email asking to confirm your email address, so that no one can start sending you spam from random websites.

## 3. All set, receive emails

From now on, when someone submits that form, we'll forward you the data as email.

=======
## Advanced features:

Form inputs can have specially named name-attributes, which alter functionality. They are all prefixed with an underscore.

### _replyto

This value is used for the email's Reply-To field. This way you can directly "Reply" to the email to respond to the person who originally submitted the form.

### _next

By default, after submitting a form the user is shown the Formspree "Thank You" page. You can provide an alternative URL for that page.

### _subject

This value is used for the email's subject, so that you can quickly reply to submissions without having to edit the subject line each time.

### _cc

This value is used for the email's CC Field. This lets you send a copy of each submission to another email address.

### _gotcha

Add this "honeypot" field to avoid spam by fooling scrapers. If a value is provided, the submission will be silently ignored. The input should be hidden with CSS.

### Using AJAX

You can use Formspree via AJAX. This even works cross-origin. The trick is to set the Accept header to application/json. If you're using jQuery this can be done like so:

    $.ajax({
        url: "//formspree.io/you@email.com", 
        method: "POST",
        data: {message: "hello!"},
        dataType: "json"
    });

--------


Running your own copy of Formspree 
----------------------------------

### Running on localhost

You'll need a [sendgrid](https://sendgrid.com/) account, postgresql, redis and python 2.7 and should install [pip](https://pip.pypa.io/en/latest/installing.html), and create a [virtual environment](http://docs.python-guide.org/en/latest/dev/virtualenvs/) for the server.

Once your environment is setup, create a postgresql database, clone the source and cd into the root of the Formspree repository. Then run:

    pip install -r requirements.txt

then create a `.env` file with your configuration like the following:

    API_ROOT='127.0.0.1:5000'
    CONTACT_EMAIL='support@example.com'
    DATABASE_URL='postgresql://<username>@127.0.0.1:5432/formspree'
    DEBUG='True'
    DEFAULT_SENDER='no-reply@localhost.com'
    LOG_LEVEL='debug'
    MONTHLY_SUBMISSIONS_LIMIT='100'
    NONCE_SECRET='y0ur_n0nc3_s3cr3t'
    HASHIDS_SALT='a salt'
    REDISTOGO_URL='127.0.0.1:6379'
    SECRET_KEY='y0ur_s3cr3t_k3y'
    SENDGRID_PASSWORD='<password>'
    SENDGRID_USERNAME='<username>'
    SERVICE_NAME='LocalFormspree'
    SERVICE_URL='http://127.0.0.1:5000'
    TEST_DATABASE_URL='sqlite://'

Make sure you have a postgresql database called `formspree` and create the necessary tables by running:

    python manage.py db upgrade

And you are ready to run the server:

    python manage.py runserver
    
### Running tests

    REDISTOGO_URL='0.0.0.0:6379' \
    TEST_DATABASE_URL=sqlite:// \
    NONCE_SECRET='y0ur_n0nc3_s3cr3t' \
    HASHIDS_SALT='a salt' \
    SECRET_KEY='y0ur_s3cr3t_k3y' \
    python -m unittest discover

### Running on heroku

You will need to install the [heroku toolbelt](https://toolbelt.heroku.com/).

Once your environment is setup, clone the source and cd into the root of the Formspree repository. Then run:

    heroku apps:create [your project name]

then

    git push heroku

Your new project will be running at [your project name].herokuapp.com.


### Dependencies

Formspree requires a Postgres database and uses SendGrid to send emails. If you're deploying to Heroku you can get a free Heroku Postgres database and a SendGrid account by running

    heroku addons:add heroku-postgresql:hobby-dev
    heroku addons:add sendgrid

### Configuring Formspree

Take a look at the `forms/settings.py` file for a list of environment variables that should be set in order for Forms to work correctly.



Contributing
----------------------------------

Formspree is being managed from Assembly. Check out the discussion and get involved at [assembly.com/formspree](http://www.assembly.com/formspree).
<a href="https://assembly.com/formspree/bounties?utm_campaign=assemblage&utm_source=formspree&utm_medium=repo_badge"><img src="http://badger.asm.co/formspree/badges/tasks.svg" height="24px" alt="Open Tasks" /></a>

