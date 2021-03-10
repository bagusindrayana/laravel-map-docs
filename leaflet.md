# LEAFLET-MAP

> Some function based on original javascript api from leaflet js https://leafletjs.com/reference-1.7.1.html
- namespace BagusIndrayana\LaravelMap\Leaflet
## Basic
```php
$laravelMap = new LaravelMap('leaflet',[
    'center'=>[55.665957,12.550343],
    'zoom'=>15,
    'container'=>'leaflet-map',
    'containerStyle'=>'width: 100%; height: 400px;'
]);
$laravelMap->map->tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',[
    'attribution'=>'&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
]);
```

## addEvent

- you can add some event like load,click,etch and `$m` will return leaflet object

```php
$laravelMap->map->addEvent('load',function($m){
    //
});
```

## Marker

- add simple marker

```php
use Bagusindrayana\LaravelMap\Leaflet\Marker;

$marker = new Marker([
    'latLng'=>[55.666067,12.551453]
]);
$map->giveTo($marker);
```

## Circle

- add simple circle

```php
use Bagusindrayana\LaravelMap\Leaflet\Circle;

$circle = new Circle([
    'latLng'=>[55.666067,12.551453],
    'color'=>'red',
    'fillColor'=>'#f03',
    'fillOpacity'=>0.5,
    'radius'=>500
]);
$map->giveTo($circle);
```

## Polygon

- add simple polygon

```php
use Bagusindrayana\LaravelMap\Leaflet\Polygon;

$polygon = new Polygon([
    'latLng'=>[
        [55.665957,12.550343],
        [55.666067,12.551453],
        [55.667177,12.552563]
    ],
    'color'=>'blue',
    'fillColor'=>'green',
    'fillOpacity'=>0.5,
]);
$map->giveTo($polygon);
```

