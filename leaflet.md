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

