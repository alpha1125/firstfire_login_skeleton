# FirstFire Consulting LTD - Login

## What does this do
- using symfony as a framework, allow for the following USER features
  - sign up w/Email
  - sign in
  - sign out
  - reset/forget password, by sending user an email.
- Use Bootstrap 5.3.1 (as of 2023-07-31)
- Uses EasyAdmin controller, to manage:
  - USER entries


TODOs:
- EasyAdmin::UserCrudController
  - Extend to manage roles
    - SuperUser can add/remove admins
    - invite new user. Trigger a new user's email invite.
    - RESET password from ADMIN, will get user to reset email.

## Requirements:
- Mysql
- PHP 8.2
- Symfony 6.4-dev


## SETUP:

### Initial:
* DB setup, MYSQL required.
```bash
$> php bin/console doctrine:migration:migrate
$> php bin/console doctrine:fixtures:load
```


### Running:

#### Async workers, needs to be running in the background.
* Manual:
```bash
$> php bin/console messenger:consume async
```

* Cronjob:
```cronexp
# every minute -- cron will not start a new instance until this one closes
# OR alt. see: https://symfony.com/doc/current/messenger.html#supervisor-configuration
* * * * * php bin/console messenger:consume async

# Remove expired password requests
@daily php bin/console reset-password:remove-expired
```

