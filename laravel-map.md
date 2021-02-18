# LARVEL-MAP


## Initialize

when initialize or create LaravelMap class you need add provider name (mapbox/leaflet),then you can provide the setting value;

```php
$laravelMap = new LaravelMap('porvider-name',$options ?? null);
```

You can also initiate multiple maps at once

```php
$maps = new LaravelMap([
    'leaflet'=>[
        'center'=>[55.665957,12.550343],
        'zoom'=>15,
        'container'=>'leaflet-map',
        'containerStyle'=>'width: 100%; height: 400px;'
    ],
    'mapbox'=>[
        'center'=>[12.550343, 55.665957],
        'zoom'=>15,
        'style'=>'mapbox://styles/mapbox/streets-v11',
        'container'=>'mapbox-map',
        'containerStyle'=>'width: 100%; height: 400px;',
        'css'=>[
            'https://api.mapbox.com/mapbox-gl-js/v2.1.1/mapbox-gl.css',
            'https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/v4.5.1/mapbox-gl-geocoder.css'
        ],
        'js'=>[
            'https://api.mapbox.com/mapbox-gl-js/v2.1.1/mapbox-gl.js',
            'https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/v4.5.1/mapbox-gl-geocoder.min.js',
            'https://cdn.jsdelivr.net/npm/es6-promise@4/dist/es6-promise.min.js',
            'https://cdn.jsdelivr.net/npm/es6-promise@4/dist/es6-promise.auto.min.js'
        ]
    ]
]);
```

## map
Map features can be accessed in the attribute map, of course, these features depend on the map provider chosen.
```php
$laravelMap->map;
```

## requestCurrentLocation

make a request for the user's location,the first parameter is the variable naming in its javascript

```php
$laravelMap->requestCurrentLocation('pos',function($map){
    $map->addExtra('alert(pos.coords.longitude+","+pos.coords.latitude);');
});
```