# HeyMehedi EDD SL Plugin Updater

This library should be used on add-ons or plugins sold on EDD. 
It handles the updates for plugins integrated with Easy Digital Downloads in WordPress sites.

## Requirements

This class can only be used with EDD v1.7 and later.

## How to use it

### Installing

Add as a requirement using composer:

```
$ composer require heymehedi/edd-sl-plugin-updater 
```

Or add it manually to the composer.json file:

```json
{
  "require": {
    "heymehedi/edd-sl-plugin-updater": "dev-master"
  }
} 
```

### Loading and initializing

**Usage 1:**
```php
add_action('admin_init', 'init_updater');

function init_updater()
{
    $api_url         = 'https://loginmenow.com';  // The site for the EDD store.
    $plugin_file     = 'your-plugin/your-plugin.php';  // The version of your add-on/plugin.
    $current_version = '1.0.5';
    $product_id     = '3252'; // ID for the add-on/plugin on EDD.
    $author         = 'Your Name';
    
    // Initialize the library.
    $updater = new HeyMehedi\EDD_SL_Plugin_Updater(
        $api_url,
        $plugin_file,
        [
            'version' => $current_version,
            'license' => get_option( 'my_plugin_license' ),
            'item_id' => $product_id,
            'author'  => $author,
            'beta'    => false,
        ]
    );
}
```

**Usage 2:**
```php
/**
 * Login Me Now Pro Updater.
 *
 * @package Login Me Now
 * @since 1.0.0
 * @version 1.0.0
 */

namespace Login_Me_Now_Pro;

use HeyMehedi\EDD_SL_Plugin_Updater;

if ( ! defined( 'ABSPATH' ) ) {
	exit; // Exit if accessed directly.
}

defined( 'ABSPATH' ) || exit;

/**
 * Class Updater
 *
 * @since 1.0.0
 */
class Updater {
	public $api_url;
	public $plugin_file;
	public $version;
	public $product_id;
	public $author;
	public $lic_key;

	public function __construct() {
		$this->api_url     = 'https://loginmenow.com';
		$this->plugin_file = LOGIN_ME_NOW_PRO_BASE_FILE;
		$this->version     = LOGIN_ME_NOW_PRO_VERSION;
		$this->product_id  = '1212';
		$this->author      = 'Login Me Now';
		$this->lic_key     = get_option( 'my_plugin_license' );

		add_action( 'admin_init', array( $this, 'init_updater' ) );
	}

	public function init_updater() {
		$updater = new EDD_SL_Plugin_Updater(
			$this->api_url,
			$this->plugin_file,
			array(
				'version' => $this->version,
				'license' => $this->lic_key,
				'item_id' => $this->product_id,
				'author'  => $this->author,
				'beta'    => false,
			)
		);
	}
}

new Updater();
```
