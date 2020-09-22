TO GET ON BASTION AND DOWNLOAD OUR ANSIBLE PLAYBOOKS --> https://medium.com/@mschirbel/wordpress-on-aws-using-terraform-and-ansible-8c3e04cb76e9


Guide @ https://www.infinitypp.com/ansible/install-wordpress-using-ansible-ubuntu-php7/


Create wp-config.php in wordpress/templates directory
The wp-config.php variables will be replaced by the ones we declared in the main.yml (defaults) directory.

define('DB_NAME', '{{ wp_db_name }}');
define('DB_USER', '{{ wp_db_username }}');
define('DB_PASSWORD', '{{ wp_db_password }}');
define('DB_HOST', '{{ wp_db_host }}');
define('DB_CHARSET', 'utf8');
define('DB_COLLATE', '');
{{ wp_salt.stdout }}
$table_prefix  = '{{ wp_table_prefix }}';
define('WPLANG', '');
define('WP_DEBUG', {{ wp_debug_mode }});
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__) . '/');
require_once(ABSPATH . 'wp-settings.php');




Define our website, virtual host
Every website has a virtual host config. In-order to automate this process we’ll create vhost.conf.js in the wordpress/templates directory
This file will contain the virtual host config for our WordPress Website.

<VirtualHost>
       DocumentRoot {{ path }}
       ServerName {{ website_address }}
</VirtualHost>