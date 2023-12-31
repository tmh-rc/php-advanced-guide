# CRUD (Create, Read, Update, Delete) <!-- omit from toc -->

- [Todo](#todo)
- [Steps](#steps)
  - [Step 1](#step-1)
  - [Step 2](#step-2)
- [Testing](#testing)

## Todo

- Create movie CRUD(Create, Read, Update, Delete) functionality.

## Steps

### Step 1

In the controller, fetch movie data from the database and then return it to the view.

```php
<?php

namespace Controllers;

use Core/Database;

class MovieController
{
    private $db;

    public function __construct()
    {
        $this->db = new Database;
    }

    public function index()
    {
        $movies = $this->db->query('SELECT...')->get();

        echo view('movies.index', [
            'movies' => $movies
        ]);
    }

    public function show($id)
    {
        $movie = $this->db->query('SELECT...', ['id' => $id])->first();

        echo view('movies.show', [
            'movie' => $movie
        ]);
    }

    public function create()
    {
        echo view('movies.create');
    }

    public function store()
    {
        $this->db->query('INSERT...', [
            'title' => request('title'),
            'duration_minutes' => request('duration_minutes'),
            'plot_summary' => request('plot_summary'),
            'released_at' => request('released_at'),
            'poster_image_path' => request('poster_image_path'),
        ]);

        redirect('/movies');
    }

    public function edit($id)
    {
        $movie = $this->db->query('SELECT...', ['id' => $id])->first();

        echo view('movies.edit', [
            'movie' => $movie
        ]);
    }

    public function update($id)
    {
        $this->db->query('UPDATE...', [
            'id' => $id,
            'title' => request('title'),
            'duration_minutes' => request('duration_minutes'),
            'plot_summary' => request('plot_summary'),
            'released_at' => request('released_at'),
            'poster_image_path' => request('poster_image_path'),
        ]);

        redirect('/movies');
    }

    public function destroy($id)
    {
        $movie = $this->db->query('DELETE...', ['id' => $id]);

        redirect('/movies');
    }
}
```

### Step 2

The code in the view should adhere to the following outlined structure. Additional elements can be added.

```php
// views/movies/index.php

<ul>
<?php foreach($movies as $movie): ?>
    <li>
        <h3><?php echo $movie['title'] ?></h3>
        <img src="<?php echo asset($movie['poster_image_path']) ?>" >
    </li>
<?php endforeach; ?>
</ul>
```

```php
// views/movies/show.php
<h3><?php echo $movie['title'] ?></h3>
<img src="<?php echo asset($movie['poster_image_path']) ?>" >
<p><?php echo $movie['duration_minutes'] ?> min</p>
<p><?php echo $movie['plot_summary'] ?></p>
<p><?php echo $movie['released_at'] ?></p>
<h3>Movie Create</h3>
<a href="/movies/<?php echo $movie['id'] ?>/edit">Edit</a>
<form action="/movies/<?php echo $movie['id'] ?>" method="POST">
    <input type="hidden" name="_method" value="PUT">
    <button type="submit">DELETE</button>
</form>
```

```php
// views/movies/create.php
<h3>Movie Create</h3>
<form action="/movies" method="POST">
    <input type="text" name="title">
    <input type="text" name="poster_image_path">
    <input type="text" name="duration_minutes">
    <input type="text" name="plot_summary">
    <input type="text" name="released_at">
    <button type="submit">Create</button>
</form>
```

```php
// views/movies/edit.php
<h3>Movie Edit</h3>
<form action="/movies/<?php echo $movie['id'] ?>" method="POST">
    <input type="hidden" name="_method" value="PUT">
    <input type="text" name="title" value="<?php echo $movie['title']; ?>">
    <input type="text" name="poster_image_path" value="<?php echo $movie['poster_image_path']; ?>">
    <input type="text" name="duration_minutes" value="<?php echo $movie['duration_minutes']; ?>">
    <input type="text" name="plot_summary" value="<?php echo $movie['plot_summary']; ?>">
    <input type="text" name="released_at" value="<?php echo $movie['released_at']; ?>">
    <button type="submit">Update</button>
</form>
```

## Testing

Run `php -S localhost:8080` in terminal. Perform CRUD operations.

[Previous](./database.md) | [Next](./session.md)
