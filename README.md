# Drupal Dev Days 2025 - Introduction to Migration

In this session we write a migration to import/update articles with related tags and image into Drupal. The articles content is made available via a JSON file, which is a commonly used data format for exchanging content between systems.

## Drupal setup

The Drupal setup used in this session was a 'out-of-the-box' Drupal 11 install with contribute module `migrate_plus' and 'migrate_tools` installed and enabled.

The migrate_tools module gives you a 'Migrations' menu admin page that is available via 'Manage' > 'Structure' > 'Migrations'. In there the migrations you add via config will be detected and can be run, rollback, stop and reset.

## Entity types

For the `json_articles`, `json_article_image_urls` and `json_article_image_objects`:
* we use the `node:article` bundle that is available in Drupal by default.
* the tags are migrated to the vocabulary 'tags' and referenced in the `field_tags` of the article.
* the images are migrated to file entities and referenced in the `field_image' of the article.

For the `json_countries` migration we we created an extra taxonomy vocabulary `countries`. No extra fields are required there.


## A no-code PHP session

I did not write any rule of PHP code for this session. All was done via YAML config files that were added to the config/sync folder (by default that one exists in the `sites/default/files` folder) and imported in the Drupal data via `drush cim' (config import).

We only use the plugins that are in Drupal core and the contributed modules `migrate_plus`.

## To get started

### The YAMLS

The **YAML files** in this repo (`config` folder) hold the configurations for the migrations.

Copy them to your `config/sync` folder (by default in the `sites/default/files` folder and import them. You can import them via the Drupal UI or via the `drush cim' command. 

TIP: If your `config/sync` folder is still empty that means your current configuration is not yet exported and available as YAMLs. Before copying the migration YAMLs to the config sync folder export the current configuration first via the Drupal UI or via the `drush cex` command.

### The JSONs

In this repo there are a few **JSON files** ('json` folder) file that holds the content to be migrated.

Copy thos files to the `/sites/default/files/json` folder to make them available for the migration, for example as `public://json/articles.json`.
