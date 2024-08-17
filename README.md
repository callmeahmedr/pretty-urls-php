# Sweet URL Handler

A lightweight and scalable PHP utility to handle clean and pretty URLs in your application.

## Features

- **Easy Integration:** Simple to set up and use in any PHP project.
- **Scalable:** Designed to handle multiple routes efficiently.
- **Customizable:** Easily extendable for more advanced routing needs.

## Installation

### Step 1: Clone the repository:
Clone the repository to your local machine using the following command:
```bash
git clone https://github.com/callmeahmedr/sweet-url-handler.git
```

### Step 2: Include the Handler in Your Project:
Add the `SweetUrlHandler.php` file to your project by including it in your PHP scripts:
```php
require_once 'src/SweetUrlHandler.php';
```

### Step 3: Configure Your `.htaccess` File
Ensure your .htaccess file has the following rules to enable clean URLs:
```apache
RewriteEngine on
RewriteCond %{REQUEST_FILENAME}.php -f
RewriteRule !.*\.php$ %{REQUEST_FILENAME}.php [QSA,L]
Options -Indexes
```

## Basic Usage

Here’s a simple example of how to use the 'SweetUrlHandler' class in your project:
```php
require_once 'src/SweetUrlHandler.php';

$handler = new SweetUrlHandler();

// Get the entire route as an array
$route = $handler->getRoute();
echo 'Current Route: ' . implode('/', $route);

// Get a specific segment of the route
$segment = $handler->getRoute(0); // First segment
echo 'First Segment: ' . $segment;

```

## Advanced Usage
### Route Matching
You can match specific routes using patterns. This allows you to define routes with parameters, making your URL handling more dynamic:
```php
require_once 'src/SweetUrlHandler.php';

$handler = new SweetUrlHandler();

// Example: Match a route like /products/123
$match = $handler->matchRoute('products/{id}');
if ($match) {
    echo 'Product ID: ' . $match['id'];
} else {
    echo 'No match found';
}
```

### Route Matching with Parameters
The `matchRoute()` method has been enhanced to merge route parameters with query parameters, providing a comprehensive set of parameters.
```php
require_once 'src/SweetUrlHandler.php';

$handler = new SweetUrlHandler();

// Example: Match a route like /products/123?sort=asc
$handler->handleRoute('products/{id}', function($params) {
    echo 'Product ID: ' . $params['id'] . '<br>';
    echo 'Sort Order: ' . $params['sort'];
});

// Example: Get a specific route segment
echo 'Second Segment: ' . $handler->getRoute(1);

// Example: Get all query parameters
print_r($handler->getParams());
```
