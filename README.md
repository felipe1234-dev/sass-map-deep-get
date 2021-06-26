# A SASS/SCSS function to improve `map-get()`... ENJOY!
SCSS/SASS function to get data from complex map structures.

## Source code

```scss
@function map-deep-get($map, $keys...) {
    $aux: map-get(
        $map, 
        nth($keys, 1) 
    );
    
    @for $i from 2 through length($keys) {
        $aux: map-get(
            $aux, 
            nth($keys, $i) 
        );
    }
    
    @return $aux;
}
```

## Examples

**Normal `map-get()` usage**:

```scss
// _config.scss
$font: (
  color      : #666,
  family     : (Arial, Helvetica),
  size       : 16px,
  line-height: 1.4
);
 
// _presets.scss
body {
  color      : map-get($font, color);
  font-family: map-get($font, family);
  font-size  : map-get($font, size);
  line-height: map-get($font, line-height);
}

// Output
body {
  color      : #666;
  font-family: Arial, Helvetica;
  font-size  : 16px;
  line-height: 1.4;
}
```
**What `map-deep-get()` can do**:

```scss
// Scheme of colors
$colorScheme: (
  gray: (
    base : #ccc,
    light: #f2f2f2,
    dark : #666
  ),
  brown: (
    base : #ab906b,
    light: #ecdac3,
    dark : #5e421c
  )
);

// Sass
.element {
  color: map-deep-get($colorScheme, brown, base);
}
.element-light {
  color: map-deep-get($colorScheme, brown, light);
}

// Output
.element {
    color: #ab906b;
}
.element--light {
    color: #ecdac3;
}
```
