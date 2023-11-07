# Advanced Routing

Update route URI

**Current**
```php
// Old Code
$router->get('movies/(\w+)/edit', [MovieController::class, 'edit']);
$router->put('movies/(\w+)', [MovieController::class, 'update']);
$router->get('movies/(\w+)', [MovieController::class, 'show']);
$router->delete('movies/(\w+)', [MovieController::class, 'destroy']);

// New Code
$router->get('movies/{id}/edit', [MovieController::class, 'edit']);
$router->put('movies/{id}', [MovieController::class, 'update']);
$router->get('movies/{id}', [MovieController::class, 'show']);
$router->delete('movies/{id}', [MovieController::class, 'destroy']);
```