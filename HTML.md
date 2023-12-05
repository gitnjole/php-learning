# HTML

**HyperText Markup Language**
	zadnja verzija je HTML5 objavljen 2014.

Skeleton
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>

<body>
	content here
</body>

</html>
```

Povezivanje s CSS
```html
<link rel="stylesheet" href="style.css">
```

Anchor tag
```html
<a href="/">Link name</a>
```

Tables
```html
<table>  

<tr>  
  <th>First Name</th>  
  <th>Last Name</th>  
  <th>Points</th>  
</tr> 

<tr>  
  <td>Jill</td>  
  <td>Smith</td>  
  <td>50</td>  
</tr>  

</table>
```

Korištenje PHP-a

### Inline
```html
<body>
	<?php
		echo "<h1>This is a title</h1>";
	?>
</body>
```

### Short
```html
<body>
	<?= "<h1>This is a title</h1>" ?>
</body>
```

### Alternative
```html
<body> 
	<?php if (condition): ?> 
		<p>Condition is true</p> 
	<?php else: ?> 
		<p>Condition is false</p> 
	<?php endif; ?> 
</body>
```
	: služi za naznačavanje početka kontrolne strukture koja mora završiti s 'endif', 'endwhile', 'endfor' etc.
	: otvara blok koda slično kao {}

## Komentari

```html
<!--- Ovo je komentar! -->
```
	započinju s <!--
	završavaju s -->