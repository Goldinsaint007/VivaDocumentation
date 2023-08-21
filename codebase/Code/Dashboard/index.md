# Viva Real Estate Laravel and Livewire Code Components Documentation

## Table of Contents

- [Viva Real Estate Laravel and Livewire Code Components Documentation](#viva-real-estate-laravel-and-livewire-code-components-documentation)
  - [Table of Contents](#table-of-contents)
  - [Laravel Controller: Dashboard](#laravel-controller-dashboard)
    - [Controller Overview](#controller-overview)
      - [Authentication Middleware](#authentication-middleware)
      - [Index Method](#index-method)
  - [Laravel View: Dashboard-View](#laravel-view-dashboard-view)

## Laravel Controller: Dashboard

The `Dashboard` Laravel controller is responsible for managing the dashboard view and related functionality in the Viva Real Estate project. This controller is part of the Laravel and Livewire setup that facilitates the rendering of the dashboard interface and retrieving relevant user data.

### Controller Overview

The `Dashboard` controller extends the base Laravel `Controller` class and defines the necessary methods to render the dashboard view.

```php
<?php

namespace App\Http\Controllers\Dashboard;

use App\Http\Controllers\Controller;
use App\Http\HTML_Elements\HTML_Elements;

class Dashboard extends Controller {

    public function __construct() {
        $this->middleware('auth');
    }

    public function index() {
        $htmlEmements = app(HTML_Elements::class);
        $user = auth()->user();
        $role = $user->role->value;
        $username = $user->first_name . ' ' . $user->last_name;

        return view('dashboard.newdash', [
            'htmlEmements' => $htmlEmements,
            'user' => $user,
            'role' => $role,
            'username' => $username,
        ]);
    }
}
```

#### Authentication Middleware

The controller's `__construct` method includes the `auth` middleware to ensure that only authenticated users can access the dashboard:

```php
use App\Http\Controllers\Controller;

class Dashboard extends Controller {

    public function __construct() {
        $this->middleware('auth');
    }

    // ...
}
```

#### Index Method

The `index` method is responsible for rendering the dashboard view and passing relevant data to it. It uses the `auth` middleware to ensure that only authenticated users can access the dashboard.

```php
use App\Http\Controllers\Controller;

class Dashboard extends Controller {

    // ...

    public function index() {
        // Obtain an instance of HTML_Elements
        $htmlEmements = app(HTML_Elements::class);

        // Get the authenticated user's information
        $user = auth()->user();
        $role = $user->role->value;
        $username = $user->first_name . ' ' . $user->last_name;

        // Pass data to the view
        return view('dashboard.newdash', [
            'htmlEmements' => $htmlEmements,
            'user' => $user,
            'role' => $role,
            'username' => $username,
        ]);
    }
}
```

## Laravel View: Dashboard-View

GOTO [Laravel View: Dashboard-View](view.md)
