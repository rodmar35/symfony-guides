# Console commands

You can see available commands:

```
./bin/console
```

### Create project

*Way 1*

- Install [Symfony client](https://symfony.com/download):

```
wget https://get.symfony.com/cli/installer -O - | bash
```

- Create new project:

```
symfony new mysite
```

*Way 2*

```
composer create-project symfony/skeleton mysite
```

### Add package

```
composer require symfony/dotenv
```

Add package to dev environment only

```
composer require maker --dev
```

### Remove package

```
composer remove symfony/dotenv
```

### Create controller

```
php bin/console make:controller
```

If you get the error *There are no commands defined in the "make" namespace.*, install package:

```
composer require maker --dev
```

File of controller `src/Controller/PartnerController.php`:

```php
class PartnerController extends AbstractController
{
    /**
     * @Route("/partners", name="partner")
     */
    public function index(EntityManagerInterface $em)
    {
        $repository = $em->getRepository(Partner::class);
        $partners = $repository->findAll();

        return $this->render('partners/index.html.twig', [
            'partners' => $partners,
        ]);
    }
}
```

Store the application templates in the `templates/` directory at the root of your project.

File of template `templates/partners/index.html.twig`:

```twig
{% extends 'base.html.twig' %}

{% block content %}
    <h1>Partners</h1>

    {% if partners %}
        <ul>
        {% for partner in partners %}
            <li>{{ partner.name }} - {{ partner.email }}</li>
        {% endfor %}
        </ul>
    {% else %}
        <p>No partners found</p>
    {% endif %}

{% endblock %}
```

### Create CRUD for entity

```
php bin/console make:crud
```
This command will create controller, form, templates for entity.

### Start development server

*Way 1:*
```
php -S 127.0.0.1:8000 -t public
```

*Way 2:*
```
./bin/console server:start
```
To make this work, don't forget to add: `composer require server`

### Show available routes
```
./bin/console debug:router
```

### Show available services that we can include in our app:

```
./bin/console debug:autowiring
```

If you want to search available services that match the given word *log*:

```
./bin/console debug:container log
```

If you also want to see private services:

```
./bin/console debug:container --show-private
```

### Show parameters values

```
./bin/console debug:container --parameters
```

*Useful parameters*:

- `kernel.debug` - it's `true` most of the time, but is `false` in the prod environment.


### Dump default config of the bundle

```
./bin/console config:dump TwigBundle
./bin/console config:dump knp_markdown
```

### Show current config for service

```
./bin/console debug:config framework
```

### Clear app's cache

```
./bin/console cache:pool:clear cache.app
```

Clear Symfony's internal cache that helps your app run:

```
./bin/console cache:clear
```

### Create cache files

```
./bin/console cache:warmup
```

This command will create all cache files that Symfony will ever need.

### Show environment variables

```
./bin/console about
```

### Show twig filters, functions

```
php bin/console debug:twig
```

### Generate User, UserRepository

```php
php bin/console make:user
```