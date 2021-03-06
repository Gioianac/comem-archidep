# Configure a PHP application through environment variables

This guide describes how to improve the configuration step of the [previous exercise](git-clone-deployment.md)
by using environment variables instead of hardcoding configuration values.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Setup](#setup)
- [Update the configuration](#update-the-configuration)
- [Pull the latest version from the server](#pull-the-latest-version-from-the-server)
- [Run the PHP development server](#run-the-php-development-server)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->




## Setup

Make sure you have done the [previous exercise](git-clone-deployment.md)
and the [Git collaboration](https://github.com/MediaComem/comem-archidep-php-todo-exercise) exercise first.

Stop your `php -S` command if it is still running.





## Update the configuration

**In your local repository (NOT on the server):**
modify the first few lines of `index.php` to take configuration values from the environment if available.

For example, instead of:

```php
define('BASE_URL', '/');
```

Use this:

```php
define('BASE_URL', getenv('TODOLIST_BASE_URL') ?: '/');
```

With this code, the `BASE_URL` variable will be equal to the value of the `TODOLIST_BASE_URL` environment variable if it has been set,
or it will default to `/` if the environment variable is not available.

Do **not** set a default value for the password,
as it is a bad practice to hardcode sensitive values.

The full configuration section should look like this:

```php
define('BASE_URL', getenv('TODOLIST_BASE_URL') ?: '/');
define('DB_USER', getenv('TODOLIST_DB_USER') ?: 'todolist');
define('DB_PASS', getenv('TODOLIST_DB_PASS'));
define('DB_NAME', getenv('TODOLIST_DB_NAME') ?: 'todolist');
define('DB_HOST', getenv('TODOLIST_DB_HOST') ?: '127.0.0.1');
define('DB_PORT', getenv('TODOLIST_DB_PORT') ?: '3306');
```

**Commit and push your changes** to the remote repository on GitHub.





## Pull the latest version from the server

**Connect to your server** and go into the cloned repository (from the previous exercise):

```bash
$> cd ~/todolist-repo
```

Discard the changes you made manually for the previous exercise:

```bash
$> git checkout index.php
```

Pull the latest version from GitHub:

```bash
$> git pull origin master
```




## Run the PHP development server

Still in the cloned repository, run a PHP development server on port 3000.

This time, add an environment variable to define the password when running it:

```bash
$> TODOLIST_DB_PASS="chAngeMeN0w!" php -S 0.0.0.0:3000
```

You should be able to access the application in a browser at the correct IP address and port (e.g. `1.1.1.1:3000`).





## End result

![Diagram](configuration-through-environment.png)

> [PDF version](configuration-through-environment.pdf).





[cyberduck]: https://cyberduck.io
[php-todolist]: https://github.com/MediaComem/comem-archidep-php-todo-exercise
