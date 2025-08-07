# Development tools
This chapter covers all the different development tools you need for Drupal install and development. Everything from system 
platforms like Docker and DDEv, IDE's and versioning control.

## Docker
Using Docker containers while developing has several compelling advantages. First and foremost it allows for environment 
consistency and therefor eliminates the biggest excuse used in development: "It works on my machine!" Instead it ensures
that your development environment is exactly the same as the staging/production environment.

It also allows isolation between projects, allowing you to use different dependencies, PHP/Node/Python/Database versions etc,
eliminating risk of conflicts with global packages or system-level software.

It's relatively quick to setup for the first time, but you will need some knowledge of Docker to do so. There might also
be someone at your company or in your project that has already done so, leaving you to only need to run `docker compose up` 
to run the containers and start. 

Docker containers work very well with modern tools like VS Code Dev Containers, GitHub Codespaces and CI tools plus it 
supports volume mounts, network configurations, debugging and more.

## DDEV
DDEV is an open-source tool that simplifies the local web developing by using Docker containers. It's very popular 
with PHP-based development like Drupal, WordPress, TYPO3, Laravel and Symfony, but it also works well for general
web development.

DDEV automates Docker container setup for web development projects and provides a standardized environment for PHP,
web server, database and other dependencies. It's really easy to spin up, tear down and switch between projects. You can
be working in multiple different Drupal projects at once, each with their own configurations and still have no conflicts
between them. It handles HTTPS, custom domains, email capture, Xdebug and so much more.

The key features are:
* Cross-project consistency, allowing to run multiple projects locally with the same tools and setup.
* Out-of-the-box LAMP/LEMP setup and built-in support for Apache/Nginx, MariaDB/PosteSQL and PHP 7.x and 8.x
* Docker-powered so your system stays clean
* Per-project config. All settings live in the `.ddev/config.yml` in each project folder
* HTTPS and custom domains, allowing you to have your live domain's url with `.ddev.site` ending to your URL. And it has SSL!
* Very easy setup! `ddev config`, `ddev start` and you are ready.
 
Some basic DDEV commands:
``` 
ddev config         # Initialize DDEV for your project
ddev start          # Starts the environment
ddev ssh            # Enters the web container
ddev stop           # Stops the project environment
ddev delete         # Removes the environment and the containers
```
### Why use DDEV rather than raw Docker/Docker compose
With DDEV you get Automatic setup, Built-in HTTPS/dev domains, can easily switch between PHP versions, have clean CLI commands
and it provides integrated dev tools.

If you choose raw Docker on the other hand, all config becomes manual, it requires separate NGINX config, the PHP versions
are tied to the container image and you need to add your own Xdebug, Mailhog and other dependencies manually.

That being said, we're not saying DDEV is better. After all is DDEV based on Docker so in the end you are having the "same"
system. The difference is where you want to focus your time, either more at developing or sharing the time for configuration.

## Lando
Lando is (also) an open-source local development tool built on Docker. It's designed to simplify the setup and management
of development environments, especially for web applications like Drupal, WordPress, Laravel and more.

The key features are:
* Docker powered. Everything runs in isolated containers, keeping your host system clean.
* Per-project config. Uses a `.lando.yml` file to define services, tooling and dependencies.
* Prebuilt "recipes" allows quickly spin up of environments for Drupal, WordPress, Laravel, Node.js and more.
* Built-in dev services. Easily include databases, caches, mailhog, PHP versions and more.
* HTTPS and custom domains, allowing you to have local URLS with endings like `.lndo.site`.
* Dev tooling automatically includes CLI tools like `drush`, `wp-cli`, `composer` and `npm`.
* Hosting integrations supports push/pull with Pantheon, Acquia, Platform.sh and more.
* Extending with custom Docker images and services if needed.

## DDEV vs. Lando vs. Raw Docker

| Feature                       | **DDEV**                                                    | **Lando**                                                  | **Raw Docker**                                          |
| ----------------------------- | ----------------------------------------------------------- | ---------------------------------------------------------- | ------------------------------------------------------- |
| **Foundation**              | Docker                                                      | Docker                                                     | Docker                                                  |
| **Setup Complexity**       | Low – CLI-based config (`ddev config`, `.ddev/config.yaml`) | Medium – YAML config file (`.lando.yml`)                   | High – manual Dockerfile, `docker-compose.yml`, scripts |
| **Ease of Use**            | Very easy, minimal config, optimized for CMSs               | Easy but more flexible/customizable                        | Difficult – requires deep Docker knowledge              |
| **Built-in Services**      | PHP, DBs, Redis, Mailhog, NGINX, HTTPS                      | PHP, DBs, Redis, Mailhog, Apache/NGINX, HTTPS              | Only what you explicitly define                         |
| **Local URLs**             | `https://<project>.ddev.site` with HTTPS out-of-the-box     | `http://<project>.lndo.site`, HTTPS optional               | Manual ports and hostname setup                         |
| **Xdebug / Mailhog**       | Built-in, toggle with CLI                                   | Built-in, included in recipes                              | Manual setup required                                   |
| **Tooling Support**        | Composer, Xdebug, mkcert, VS Code DevContainers, etc.       | Composer, Drush, WP-CLI, npm, platform integrations        | Add tools manually or via custom Dockerfiles            |
| **Customizability**       | Moderate – via hooks or Docker overrides                    | High – supports custom Docker images and services          | Unlimited – you control everything                      |
| **Developer Experience** | Streamlined, especially for CMS workflows                   | Flexible and developer-friendly, better for platform teams | Powerful but verbose and error-prone                    |
| **Docs & Community**       | Strong documentation, active open-source community          | Strong docs, backed by Pantheon community                  | General Docker docs, no project-specific support        |
| **Hosting Integration**    | No direct integrations                                      | Supports Pantheon, Acquia, Platform.sh                     | None                                                    |
| **Multi-project Handling** | Excellent, automatic DNS and isolation                      | Excellent, automatic proxying and service separation       | Manual – separate networks, containers, and DNS         |
| **Drupal/WordPress Ready** | Yes — primary use case                                      | Yes — with official "recipes"                              | Only if you build the stack manually                    |

# IDE's 
An IDE (Integrated Development Environment) is a software application that provides developers with a complete set of tools 
for writing, testing and debugging code, all in one place.

The key features of an IDE includes:
* A code editor, smart text editor with syntax highlighting, autocomplete and code formatting.
* Debugger connection to help you step through code, inspect variables and fix bugs efficiently.
* Build tools help you compile and run the code with the results being directly displayed within the IDE.
* Integration with testing tools to run unit tests and view results directly in the IDE.
* Code navigation allows you to jump to definitions, find references and refactor with ease.
* Very customizable for specific languages, frameworks or workflows.

Everyone has an opinion on what's the "best" IDE! For Drupal/PHP development most people use either Visual Studio Code or 
PHPStorm although some people who love their configuration files use `vim` as their development tool. 

Whatever you choose, using and IDE will boost your productivity with combining multiple tools in one application, helps 
prevent bugs with smart code assistance and speeds up development with integrated workflows and automation. 

For an example, this book is written partly in PHP Storm, using Markdown as the formatting language. The Drupalviking recommends
PHPStorm for development, but that's mostly because he doesn't want to spend time learning other systems :-) 

# Versioning software
The last tool a developer has in his or hers toolkit is a versioning control software (VCS) to store their code and 
keep it consistent.

If you use a versioning control system you can track every change made to your code and roll back if needed. You can even 
roll back to the initial commit you did, even if you now have 15-20 years of commit history! VCS allows you to work with 
teams without overwriting each other's work, it uses branches to test features or fixes without affecting the main code base.
You can tag and release stable version of your code, it documents who changed what, when and why, it can offer off-site
backups so that your code is safe even if your computer crashes or is stolen and finally it integrates with CI/CD tools, 
offers code review and issue tracking.

If you decide to skip VCS on the other hand, you cannot easily revert to previous working state (undo only has so much 
buffer), collaborators can overwrite each other's work unknowingly, there is no clean way to test new ideas without affecting
production code. On top of that, manual tracking of file changes is very unreliable and very prone to mistakes and errors.
Finally, you have no backup (until you manually backup your computer)! If local files are lost or corrupted, your work is 
gone forever!

## Which one to use?
The most popular VSC for Drupal development is Git. By far. Drupal.org uses Git under the hood and is hosted on Git Lab,
which is one of three most common hosting platforms for Drupal. The others are GitHub and BitBucket. 

[NOTE]
Remember not to confuse the two. Git is the software, the VCS. GitLab and GitHub are platforms to host code on, but they
both use "Git" as the software.

Other VCS's include SVN (Subversion), which is very rare today and mostly legacy, and Mercurial (hg) which is practically 
nonexistent in modern Drupal workflows.

The last one to mention briefly is Azure Repos, which is a Microsoft solution. Azure is sometimes used within 
companies that relate heavily on Microsoft products as is within the Azure DevOps suite. It also uses Git, supports Team 
Foundation Version Controlling. Azure is not just for code hosting, it's part of a full DevOps pipeline. But like we said,
it's more often used when the companies have more than web development to manage and would like to keep everything in the
same place.

This book is maintained by using Git and it's hosted on GitLab for editors to collaborate on.

# Conclusion
We've mentioned a lot of tools you can use when developing for Drupal. Drupalviking developes using Macbook Pro, DDEV,
PHPStorm and Git+GitLab. That does not mean that's the best, these are just the tool he uses. Feel free to explore all the 
possibilities for your development work! The processes described in this book are mainly using these technologies, but because
it's written collaboratively and it's a live document, as other writers come to the project, we will offer explanations using
different technologies.