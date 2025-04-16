# Drupal Dev Days 2025 - Introduction to Migration

In this session we write a migration to import/update articles with related tags and image into Drupal. The articles content is made available via a JSON file, which is a commonly used data format for exchanging content between systems.

## Drupal setup

The Drupal setup used in this session was an 'out-of-the-box' [Drupal 11 core](https://new.drupal.org/download) install with contribute module [`migrate_plus`](https://www.drupal.org/project/migrate_plus) and [`migrate_tools`](https://www.drupal.org/project/migrate_tools) installed and enabled.

The `migrate_tools` module gives you a 'Migrations' admin page that is available via 'Manage' > 'Structure' > 'Migrations'. In there the migrations you add via config will be detected and can be runned, rollbacked, stoped and reset.

The `migrate_plus` module extends the Drupal migrate functionality with the `url` source plugin that makes migrating JSON content available.

## Entity types

For the `json_articles`, `json_article_image_urls` and `json_article_image_objects` migrations:
* we use the `node:article` bundle with `field_tags` and `field_image` that is available in Drupal by default.
* the tags are migrated to the vocabulary `tags` and referenced in the `field_tags` field of the article.
* the images are migrated to file entities and referenced in the `field_image` field of the article.

For the `json_countries` migration an extra taxonomy vocabulary `countries` has to be created. No extra fields are required there.


## A no-PHP-code session

In this session we do not write any PHP code. All was done via YAML config files that were added to the `config/sync` folder (by default that one exists in the `sites/default/files` folder) and imported in the Drupal data via `drush cim` (config import).

We only use the plugins that are in Drupal core and available via the contributed module `migrate_plus`.

## To get started

### The YAMLS

The **YAML files** in this repo (`config` folder) hold the configurations for the migrations.

Copy them to your `config/sync` folder (by default in the `sites/default/files` folder and import them. You can import them via the Drupal UI or via the `drush cim' command. 

TIP: If your `config/sync` folder is still empty that means your current configuration is not yet exported and available as YAMLs. Before copying the migration YAMLs to the config sync folder export the current configuration first via the Drupal UI or via the `drush cex` command.

### The JSONs

In this repo there are a few **JSON files** ('json` folder) file that holds the content to be migrated.

Copy thos files to the `/sites/default/files/json` folder to make them available for the migration, for example as `public://json/articles.json`.
