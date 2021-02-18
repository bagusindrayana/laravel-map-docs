# MAPBOX-MAP

> Some function based on original javascript api from mapbox-gl-js https://docs.mapbox.com/mapbox-gl-js/api
- namespace BagusIndrayana\LaravelMap\Mapbox
## Basic

```php
$laravelMap = new LaravelMap('mapbox',[
    'center'=>[-122.48695850372314, 37.82931081282506],
    'zoom'=>15,
    'style'=>'mapbox://styles/mapbox/streets-v11',
    'container'=>'map',
    'containerStyle'=>'width: 600px; height: 400px;'
]);
```

## addEvent

- you can add some event like load,click,etch and `$m` will return mapbox object

```php
$laravelMap->map->addEvent('load',function($m){
    //
});
```

## Marker
```php
$markers = [
    new Marker(["lngLat"=>[-122.48369693756104, 37.83381888486939]]),
    new Marker(["lngLat"=>[-122.48695850372314, 37.82931081282506]]),
    new Marker(["lngLat"=>[-122.49378204345702, 37.83368330777276]])
];

$laravelMap->map->addMarker($markers);
```

## Popup
```php
$popup = new Popup(['offset'=>25,'text'=>'Hublaaaa']);

//want add to marker
new Marker(["lngLat"=>[-122.48369693756104, 37.83381888486939],'popup'=>$popup]);

//init to js variable
$popup = new Popup(['offset'=>25,'text'=>'Hublaaaa']);
$laravelMap->map->addExtra('var popup = '.$popup->result().";");
```

## addExtra
if you want to add raw js code
```php
$laravelMap->map->addExtra("alert('test');");
```

## addControl
assigns a control class to the map
```php
$g = new MapboxGeocoder([
    'zoom'=>4,
    'placeholder'=>'Seacrh...',
]);

$c = new NavigationControl();
$c->position = 'bottom-right';

$l = new GeolocateControl([
    'positionOptions'=> [
        'enableHighAccuracy'=> true
    ],
    'trackUserLocation'=> true
]);

$laravelMap->map['mapbox-map']->addControl([$g,$c,$l]);
```

## addMarker
you can add single or multiple marker
```php
$laravelMap->map->addMarker($markers);
```

## giveTo
assign map to another component
```php
$laravelMap->map->giveTo($marker);
```

## addSource
add geojson source data
```php
$laravelMap->m->addSource('route',[
    'type'=>'geojson',
    'data'=>[
        'type'=>'Feature',
        'properties'=>[],
        'geometry'=>[
            'type'=>'LineString',
            'coordinates'=>[
                [-122.48369693756104, 37.83381888486939],
                [-122.48348236083984, 37.83317489144141],
                [-122.48339653015138, 37.83270036637107],
                [-122.48356819152832, 37.832056363179625],
                [-122.48404026031496, 37.83114119107971],
                [-122.48404026031496, 37.83049717427869],
                [-122.48348236083984, 37.829920943955045],
                [-122.48356819152832, 37.82954808664175],
                [-122.48507022857666, 37.82944639795659],
                [-122.48610019683838, 37.82880236636284],
                [-122.48695850372314, 37.82931081282506],
                [-122.48700141906738, 37.83080223556934],
                [-122.48751640319824, 37.83168351665737],
                [-122.48803138732912, 37.832158048267786],
                [-122.48888969421387, 37.83297152392784],
                [-122.48987674713133, 37.83263257682617],
                [-122.49043464660643, 37.832937629287755],
                [-122.49125003814696, 37.832429207817725],
                [-122.49163627624512, 37.832564787218985],
                [-122.49223709106445, 37.83337825839438],
                [-122.49378204345702, 37.83368330777276]
            ]
        ]
    ]
]);
```

## addLayer
add layer to map
```php
$laravelMap->map->addLayer([
    'id'=>'route',
    'type'=>'line',
    'source'=>'route',
    'layout'=>[
        'line-join'=>'round',
        'line-cap'=>'round',
    ],
    'paint'=>[
        'line-color'=>'#888',
        'line-width'=>8
    ]
]);
```

## loadImage
will load custom icon/image from link and url,this will print variable `error` and `image` on callback based on original api from mapbox https://docs.mapbox.com/mapbox-gl-js/api/map/#map#loadimage so if you want add some raw js you can use `error` and `image` as the output variable of the load Image function
```php
$laravelMap->map->loadImage("https://docs.mapbox.com/mapbox-gl-js/assets/custom_marker.png",function($m){
    //loadImage return callback with error and image variable in javascript string
    $m->addLayer([
        'id'=>'titik',
        'type'=>'symbol',
        'source'=>'titik',
        'layout'=>[
            'icon-image'=> 'image-id',
            'icon-allow-overlap'=> true
        ]
    ]);

    $laravelMap->map->addExtra("alert(image);");
},'image-id');
```

## addImage
add image to map https://docs.mapbox.com/mapbox-gl-js/api/map/#map#addimage
```php
$laravelMap->map->addImage('image-id','imageVar',$options);
```

## hasImage 
check if image based on id has been add https://docs.mapbox.com/mapbox-gl-js/api/map/#map#hasimage
```php
$laravelMap->map->hasImage('image-id',function($m){

});
```

## updateImage
update image based on id https://docs.mapbox.com/mapbox-gl-js/api/map/#map#updateimage
```php
$laravelMap->map->loadImage("https://docs.mapbox.com/mapbox-gl-js/assets/custom_marker.png",function($m){
    $m->haseImage('some-image',function($m){
        $m->updateImage('some-image','image');
    });
},'some-image');
```

## flyTo
move map camera position to new coordinates
```php
$mapboxMap->requestCurrentLocation('pos',function($m){
    $m->flyTo([
        'center'=>'[pos.coords.longitude,pos.coords.latitude]',
        'zoom'=>9
    ]);
});
```

## locationPicker
will render input and add event click to map and get coordinat when click on map
```php
$laravelMap->map->locationPicker([
    'varName'=>'coordinate', //render variable name that will be used to store the marker with selected coordinate data,
    'inputId'=>'input-coordinate', // id for input tag
    'inputClass'=>'form-control',//class for input tag
]);