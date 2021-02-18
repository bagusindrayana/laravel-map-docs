# JS

> will convert php code to js
- namespace BagusIndrayana\LaravelMap
## Basic
```php
$js = new Js();
$js->raw(function(){
    $a = 10;
    $b = 20;
    
    function plus($a,$b){
        return $a+$b;
    }

    $c = plus($a,$b);
});
return $js->result();
```

will convert to : 

```js
var a = 10;
var b = 20;
function plus(a,b){
    return a+b
}
var c = plus(a,b);
```

## Usange With Laravel-Map
```php
$laravelMap = new LaravelMap('mapbox',[
    'center'=>[-122.48695850372314, 37.82931081282506],
    'zoom'=>15,
    'style'=>'mapbox://styles/mapbox/streets-v11',
    'container'=>'map',
    'containerStyle'=>'width: 600px; height: 400px;'
]);


$laravelMap->map->raw(function($mapboxMap){
    $leafletMap->on('load',function($e)use($mapboxMap){
        $leafletMap->addSource('titik',[
            'type'=>'geojson',
            'data'=>[
                'type'=>'FeatureCollection',
                'features'=>new JsArray([
                    [
                        'type'=>'Feature',
                        'properties'=>[
                            'description'=>'Hublaaa 1'
                        ],
                        'geometry'=>[
                            'type'=>'Point',
                            'coordinates'=>new JsArray([12.550343, 55.665957])
                        ]
                    ],
                    [
                        'type'=>'Feature',
                        'properties'=>[
                            'description'=>'Hublaaa 2'
                        ],
                        'geometry'=>[
                            'type'=>'Point',
                            'coordinates'=>new JsArray([12.551453, 55.666067])
                        ]
                    ],
                    [
                        'type'=>'Feature',
                        'properties'=>[
                            'description'=>'Hublaaa 3'
                        ],
                        'geometry'=>[
                            'type'=>'Point',
                            'coordinates'=>new JsArray([12.552563, 55.667177])
                        ]
                    ],
                ])
            ]
        ]);

        $mapboxMap->loadImage(
            "https://docs.mapbox.com/mapbox-gl-js/assets/custom_marker.png",
            function($error,$image)use($mapboxMap){
                if(!$error && $mapboxMap->hasImage("imgId")){
                    $mapboxMap->addImage('imgId',$image);
                } else if($error == 2){
                    console.log("xdxd");
                } else {
                    console.log("hublaa");
                }
                $mapboxMap->addLayer([
                    'id'=>'titik',
                    'type'=>'symbol',
                    'source'=>'titik',
                    'layout'=>[
                        'icon-image'=> 'imgId',
                        'icon-allow-overlap'=> true
                    ]
                ]);
            }
        );
    });



});

$laravelMap->requestCurrentLocation('pos',function($m){
    $m->addExtra(Js::ajax('get',url('test'),"'longitude='+pos.coords.longitude+'&latitude='+pos.coords.latitude"));
    
});
```

result :

```js
mapboxgl.accessToken = 'pk.eyJ1IjoiYmFndXNpbmRyYXlhbmEiLCJhIjoiY2p0dHMxN2ZhMWV5bjRlbnNwdGY4MHFuNSJ9.0j5UAU7dprNjZrouWnoJyg';
var mapboxMap = new mapboxgl.Map({
	accessToken: 'pk.eyJ1IjoiYmFndXNpbmRyYXlhbmEiLCJhIjoiY2p0dHMxN2ZhMWV5bjRlbnNwdGY4MHFuNSJ9.0j5UAU7dprNjZrouWnoJyg',
	style: 'mapbox://styles/mapbox/streets-v11',
	container: 'map',
	zoom: 15,
	center: [-122.48695850372314, 37.82931081282506],
});
leafletMap.on('load', function(e) {
	leafletMap.addSource('titik', {
		'type': 'geojson',
		'data': {
			'type': 'FeatureCollection',
			'features': [{
				'type': 'Feature',
				'properties': {
					'description': 'Hublaaa 1'
				},
				'geometry': {
					'type': 'Point',
					'coordinates': [12.550343, 55.665957]
				}
			}, {
				'type': 'Feature',
				'properties': {
					'description': 'Hublaaa 2'
				},
				'geometry': {
					'type': 'Point',
					'coordinates': [12.551453, 55.666067]
				}
			}, {
				'type': 'Feature',
				'properties': {
					'description': 'Hublaaa 3'
				},
				'geometry': {
					'type': 'Point',
					'coordinates': [12.552563, 55.667177]
				}
			}]
		}
	});
	mapboxMap.loadImage('https://docs.mapbox.com/mapbox-gl-js/assets/custom_marker.png', function(error, image) {
		if(!error && mapboxMap.hasImage('imgId');) {
			mapboxMap.addImage('imgId', image);
		} else {
			if(error == 2) {
				console.log('xdxd')
			} else {
				console.log('hublaa')
			}
		}
		mapboxMap.addLayer({
			'id': 'titik',
			'type': 'symbol',
			'source': 'titik',
			'layout': {
				'icon-image': 'imgId',
				'icon-allow-overlap': true
			}
		});
	});
});
if(navigator.geolocation) {
	navigator.geolocation.getCurrentPosition(function(pos) {
		var xhttp = new XMLHttpRequest();
		xhttp.open('get', 'http://laravel-map.dev.com/send-api?' + 'longitude=' + pos.coords.longitude + '&latitude=' + pos.coords.latitude, true);
		xhttp.send();
	});
} else {
	alert('Geolocation is not supported by this browser');
}
```


