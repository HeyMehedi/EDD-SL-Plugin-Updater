# HeyMehedi EDD SL Plugin Updater

This library should be used on add-ons or plugins sold on EDD. 
It handles the updates for plugins integrated with Easy Digital Downloads in WordPress sites.

## Requirements

This class can only be used with EDD v1.7 and later.

## How to use it

### Installing

Add as a requirement using composer:

```
$ composer require HeyMehedi/edd-sl-plugin-updater 
```

Or add it manually to the composer.json file:

```json
{
  "require": {
    "HeyMehedi/edd-sl-plugin-updater": "dev-master"
  }
} 
```

### Loading and initializing

```php
<?php
add_action('admin_init', 'init_updater');

function init_updater()
{
    $apiUrl         = 'https://site-with-edd.com';  // The site for the EDD store.
    $pluginFile     = 'your-plugin/your-plugin.php';  // The version of your add-on/plugin.
    $currentVersion = '1.0.5';
    $addonEddId     = '3252'; // ID for the add-on/plugin on EDD.
    $author         = 'Your Name';
    
    // Initialize the library.
    $updater = new HeyMehedi\EDD_SL_Plugin_Updater(
        $apiUrl,
        $pluginFile,
        [
            'version' => $currentVersion,
            'license' => get_option('upstream_frontend_edit_license_key'),
            'item_id' => $addonEddId,
            'author'  => $author,
            'beta'    => false,
        ]
    );
}
```