<p align="center">
    <img height="80" src="https://cdn.rawgit.com/ElemeFE/element/dev/element_logo.svg" alt="Element UI">
    <img width="88" height="80" src="https://vuejs.org/images/logo.png" alt="Vue.js">
    <img width="300" src="https://laravel.com/assets/img/components/logo-laravel.svg" alt="Laravel">
</p>

## Laravel + Vue + ElementUI 2.x

- UI based on [ElementUI](http://element.eleme.io/).
- Login using [Sanctum](https://laravel.com/docs/9.x/sanctum) with [Axios](https://github.com/mzabriskie/axios)
- JS routing with [Ziggy](https://github.com/tighten/ziggy).
- Modular system implemented. See [description](./docs/modules.md).
- [FontAwesome](http://fontawesome.io/icons/) and [ElementUI](https://element.eleme.io/2.15/#/en-US/component/icon) icons

## Table of Contents

<a href="#start">**BEFORE YOU START**</a>

- <a href="#installation">Install and Configure The Project</a>
    * <a href="#docker">Docker</a>
    * <a href="#local">Direct Installation</a>
    * <a href="#useful-commands">Useful Commands</a>

- <a href="#ide-settings">Set Up Your IDE</a>
    * <a href="#webpack">Webpack</a>
    * <a href="#js-code-style">Javascript Code Style</a>
        - <a href="#eslint">ESLint options</a>
    * <a href="#php-code-style">PHP Code Style</a>
        - <a href="#phpcs">PHP_CodeSniffer</a>
        - <a href="#phpstan">PHPStan</a>
        - <a href="#php-inspections">PHP Inspections</a>


<a href="#work-essentials">**ALL YOU NEED FOR WORK**</a>

- <a href="#structure">Project Structure and Routes</a>
    * <a href="#add-module">Add New Module</a>

- <a href="#git">Task Management and Version Control</a>
    * <a href="#branches">GIT Branches</a>
    * <a href="#commits">GIT Commits</a>
    * <a href="#task-finished">When You Finished The Task</a>

- <a href="#features">Project Features</a>
    * <a href="#server-const">Server Constants for Frontend</a>
    * <a href="#errors">Errors Handling</a>
    * <a href="#tests">Tests</a>
    * <a href="#websockets">Websockets</a>
    * <a href="#export-import">Export/Import</a>
    * <a href="#elasticsearch">Elasticsearch</a>

- <a href="#style-guide">UI Style Guide</a>

<a href="#additional-info">**ADDITIONAL INFORMATION**</a>

- <a href="#integrations">Optional Modules and Integrations</a>
    * [Firebase](docs/integrations.md#firebase)



<span id="start"></span>
# BEFORE YOU START
***

<span id="installation"></span>
## Install And Configure The Project

<span id="docker"></span>
### Docker
If you prefer to use **Docker** follow the [Docker Setup manual](./docs/docker.md)

<span id="local"></span>
### Direct Installation
- `composer install`
- `yarn install`
- `cp .env.example .env`
- Add your **DB credentials** and **APP_URL*** in `.env`
- `php artisan key:generate`
- `php artisan migrate --seed`
- `php artisan storage:link` to create storage symlink in public folder (delete **public/storage** if has error, and re-run)
- `php artisan ziggy:generate "resources/assets/js/includes/ziggy.js"` to generate routes file
- Compile JS assets - run *one* of the following commands:
  - `yarn dev` to compile JS assets
  - `yarn watch` to run watcher to compile JS in real time
  - `yarn hot` run JS hot reload modules. For SSL need to set `HMR_SSL_CERT_PATH=` and `HMR_SSL_KEY_PATH=` keys in `.env`
    file.
- `*`Make sure your local web server is running and a new website is configured. Open with **APP_URL** in browser.
- Login with `super-admin@app.com` and password `password`

`*` To use built-in laravel Development Server run `php artisan serve` and open the given link in browser (usually http://127.0.0.1:8000). Note, that the `APP_URL` param in your `.env` should be exactly like this given link, including port number. If not, change it, then generate routes and re-compile js assets.

<span id="useful-commands"></span>
### Useful Commands
- `php artisan ide-helper:models -n` - creates and updates models meta file for [ide-helper](https://github.com/barryvdh/laravel-ide-helper#automatic-PHPDocs-for-models).
- `php artisan permissions:update` - updates role permissions (**app/Modules/Laratrust/config/permissions.php** to config).
- `php artisan make:module` - creates a new module (module name and params will be asked in process).



<span id="ide-settings"></span>
## Set Up Your IDE

You should configure your IDE to help you follow our code style rules.
The following settings are given for **PHPStorm**.

<span id="webpack"></span>
### Webpack

The Webpack configuration file `webpack.config.js` is in the root of the project.
Make sure that IDE is able to see and recognise it:

`Settings` -> `Languages & Frameworks` -> `JavaScript` -> `Webpack`

<span id="js-code-style"></span>
### Javascript Code Style

`Settings` -> `Editor` -> `Code Style` -> `JavaScript`

Click on `Set from...` and select `TypeScript`

Make sure that you have these options:

* On tab **Tabs and Indents**
  - Use tab character: `false`
  - Smart tabs: `false`
  - Tab size: `4`
  - Indent: `4`
  - Continuation Indent: `4`
  - Keep indents on empty lines: `false`
  - Indent chained methods: `true`
  - Indent all chained calls in a group: `true`


* On tab **Wrapping and Braces**
  - `Hard wrap at` = `180`

<span id="eslint"></span>
#### ESLint options

Options are defined in `.eslintrc.js` file.
If your IDE doesn't see that settings file, you should point on it manually.

For example, go to `Settings` -> `Languages & Frameworks` -> `JavaScript` -> `Code Quality Tools` -> `ESLint`

- Set `Manual ESLint configuration` to `true`
- Set `ESLint package` path as `{your_project}/node_modules/eslint`
- Set `Configuration file` path as `{your_project}/.eslintrc.js`

Now all code style issues in .js and .vue files will be highlighted.
To fix ESLint problems in a whole file, select `Fix ESLint problems` in the file's context menu.

<span id="php-code-style"></span>
### PHP Code Style

`Settings` -> `Editor` -> `Code Style` -> `PHP`

Click on `Set from...` and select `PSR1/PSR2`

Make sure that you have these options:

* On tab **Tabs and Indents**
  - Use tab character: `false`
  - Smart tabs: `false`
  - Tab size: `4`
  - Indent: `4`
  - Continuation Indent: `4`
  - Keep indents on empty lines: `false`
  - Indent code in PHP tags: `false`


* On tab **Wrapping and Braces**
  - `Hard wrap at` = `200`

<span id="phpcs"></span>
#### PHP_CodeSniffer
[Configure PHP_CodeSniffer as a PhpStorm inspection](./docs/php_cs.md)

<span id="phpstan"></span>
#### PHPStan
[Configure PHPStan as a PhpStorm inspection](./docs/phpstan.md)

<span id="php-inspections"></span>
#### PHP Inspections
Go to `Settings` -> `Plugins` -> `Marketplace` tab.

Find and install [**Php Inspections (EA Extended)**](https://plugins.jetbrains.com/plugin/7622-php-inspections-ea-extended-) plugin.



<span id="work-essentials"></span>
# ALL YOU NEED FOR WORK
***
This section contains important information for everyday work. Please, study it carefully and completely.

<span id="structure"></span>
## Project Structure and Routes
The project has a **modular system** implemented on base of Laravel framework.
It means that:

* All regular Laravel files like Models, Controllers, migrations, etc. is located in separate folders inside `app/Modules`.
* All module-related Vue files is located inside `resources/Modules` (common js and vue files are still in
  `resources/assets/js`).
* API routes for ajax requests are in `Modules/{ModuleName}/Http/Routes/api.php`.

<span id="add-module"></span>
#### Add New Module
To add **scaffolding for a new Module** run `php artisan make:module` command (module name and params will
be requested in process).

For more details of Modular structure see [documentation](./docs/modules.md).



<span id="git"></span>
## Task Management and Version Control

<span id="branches"></span>
### GIT Branches

Main CRM is called **Momentum**. It can be found in `master-v2` branch.

There are other several projects (in branches) based on the Momentum CRM, e.g.: niagara, resume4mat, springboard etc.
These projects usually have 2 major branches: `production-{project-name}` and `staging-{project-name}`. Example: `production-niagara` and `staging-niagara`. Some new projects only have staging branch in the beginning.

**When starting a new task, checkout a new branch from:**

  * Production branch of your project - for launched projects.
  * Staging branch - for projects that are not in production yet (confirm with your Team Lead!)

**Branch naming template:** `{project-name}/{feature|bugfix}/{task number}-{kebab-case-task-name}`.

*NOTE: for main CRM's tasks use project name `core-v2`*

Examples:

- `niagara/feature/NS-73-core-module-updates`
- `core-v2/bugfix/MS-4-fix-some-issue`

<span id="commits"></span>
### GIT Commits:
*****
All developers should follow smart commit [rules](https://confluence.atlassian.com/fisheye/using-smart-commits-960155400.html).

**Commit message template:** `{task number} {Performed changes description}`.

Common commit message example:
```
SD-90 Auth Page fixing
SD-90 Login Page fixing: added new validation rule
```
All committed changes should be reflected in a commit messages.

<span id="task-finished"></span>
### When You Finished The Task
1. Check on your local PC that it's really works.
2. Create a Pull Request (PR) to the staging branch of your project. Get at least 2 approvals before merge!
3. Ask the Team Lead to push to the staging server.
4. Test it manually on the staging server.
5. Make a new comment in this task in Jira, and include the following info:
   - on which server the changes are available,
   - **video** evidence of how it works.
6. Move task to the **UAT** section in Jira.
7. After receiving an approval to move to production, repeat steps 2-5 for production branch and server.
(Although, additional PR may not be needed - confirm with your Team Lead).

#### To Make a Video
Use Chrome extensions for screencast, for example: [https://www.screencastify.com](https://www.screencastify.com).
After task is complete and deployed, developer has to test it manually on staging/production,
and add a link with video file in the task.



<span id="features"></span>
## Project Features

<span id="server-const"></span>
### Server Constants for Frontend
You have access to backend constants in JS code.
Type `window.Laravel` in JS console to check the list of all exported variables.

The constants must be located in the relevant folder inside the module:

- Create `SomeConstants.php` in `{Module}/Constants` directory.
- You can add an unlimited number of module constants classes. The ending of the filename must be `Constants.php`.

**Examples:**

* `app/Modules/Users/Constants/RouteConstants.php` call in JS as `Laravel.Users.Routes`
* `app/Modules/Emails/Constants/StatusConstants.php` call as `Laravel.Emails.Statuses`
* Public const `INDEX` in `app/Modules/Users/Constants/RouteConstants.php` call as `Laravel.Users.Routes.INDEX`


<span id="errors"></span>
### Errors Handling
Validation and api requests errors in Vue should be handled with `this.$errors` plugin. It is installed as a global
property and available in any component (does not need to be imported).

For more info and usage examples see [Errors handling documentation](./docs/errors.md)


<span id="tests"></span>
### Tests
All developers should cover their implemented features with tests.
Follow the [guide](./docs/tests.md) to set up testing environment and create tests.


<span id="websockets"></span>
### Websockets
The project has notification system based on WebSockets technology.

Make sure you have these settings in `.env`:
```dotenv
BROADCAST_DRIVER=pusher

PUSHER_APP_ID=${APP_NAME}_pusher_id
PUSHER_APP_KEY=${APP_NAME}_pusher_key
PUSHER_APP_SECRET=${APP_NAME}_pusher_secret
PUSHER_APP_CLUSTER=mt1
PUSHER_PORT=6001
PUSHER_SCHEME=http
PUSHER_APP_ENCRYPTION=false

MIX_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
MIX_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"
```

Run `php artisan websockets:serve`

See **Laravel Broadcasting** [documentation](https://laravel.com/docs/broadcasting) for usage examples.


<span id="export-import"></span>
### Export/Import

This feature allows to import entities to DB from a file or download them as .xls.
Originally, it is implemented for User model, see the example on the **Admin -> Import/Export** page.
To add any other model to this feature, follow the steps :

1. In ImportExport module add new model's details to `Constants/FieldConstants.php`.
2. Add `Http/Requests/{Model}/ExportRequest` class which extends `BaseExportRequest` .
3. Add `Http/Controllers/{Model}ImportExportController` class which extends `BaseImportExportController`
4. Add routes and update permissions.
5. In Vue update data `items` in `ImportExport/includes/EntityRadio.vue`, then update `getSubmitAction` methods
   in `Import.vue` and `Export.vue` files.


<span id="elasticsearch"></span>
### Elasticsearch

See [documentation](./app/Modules/ElasticSearch/docs/elastic.md)



<span id="style-guide"></span>

## UI Style Guide

Please follow [this style guide](https://ui-style-guide.aws.hicalibertest.com.au/) when working on new layout.
It contains the most common UI rules to maintain a consistent system style.



<span id="additional-info"></span>
# ADDITIONAL INFORMATION
***

<span id="integrations"></span>
## Optional Modules and Integrations
Different projects may include optional modules and features that require additional setup.
If you need any of these features, follow corresponding [documentation](docs/integrations.md).

### [Xero](docs/integrations.md#xero)

### [Amazon Connect](docs/integrations.md#amazon-connect)

### [Stripe](docs/integrations.md#stripe)

### [G-Suite](docs/integrations.md#g-suite)

### [Firebase](docs/integrations.md#firebase)

### [Twilio](docs/integrations.md#twilio)

## REX middleware

### Add new agency for REX sync

1. On the Agencies page add a new agency.

2. Go to "Inactive" tab, find the agency and enable the sync ("Sync On" switch).

3. Update events section, select single/dual sync in a dropdown and toggle Create/Update switches.
   Now webhook-sync is working.

4. If you need to sync entities that already exist execute `php artisan rex:agency-sync` command.

5. On the Data page in the `Recent` tab.
   Change the filter by type, select the `System` item.
   On this page you will see the start and end of the sync.

6. Checking the amount of synchronization of models
    1. Log in [rexsoftware](https://app.rexsoftware.com/) to the synced account
    2. Go to the tabs Contacts, Property, Listings, Contracts (Other lists -> Contracts) in the right corner the quantity is indicated.
    3. ``
       SELECT
       type,
       count(id) as "Count Models",
       CASE
       WHEN type = 1 THEN 'PROPERTY'
       WHEN type = 2 THEN 'CONTACT'
       WHEN type = 3 THEN 'LISTING'
       WHEN type = 9 THEN 'CONTRACT'
       WHEN type = 5 THEN 'KEY_REGISTER'
       WHEN type = 6 THEN 'NOTE'
       WHEN type = 7 THEN 'KEY_REGISTER_HISTORY'
       WHEN type = 8 THEN 'BUILDING'
       WHEN type = 9 THEN 'CONTRACT'
       WHEN type = 10 THEN 'ADMIN_VALUE_LIST'
       WHEN type = 11 THEN 'LISTING_STATE'
       WHEN type = 12 THEN 'FEEDBACK'
       end
       as model
       FROM rex_models
       WHERE account_id=ID_ACCOUNT
       GROUP BY type;
       ``
    4. Compare quantity

### Sync command
If you need to manually start sync process for an agency then run `php artisan rex:agency-sync` command and follow the prompts.
