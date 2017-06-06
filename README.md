# ObHighchartsBundle fork with maps support added

`ObHighchartsBundle` eases the use of highcharts to display rich graphs, charts and maps in your Symfony2/Symfony3 applications by
providing Twig extensions and PHP objects to do the heavy lifting. The bundle uses the excellent JS library
[Highcharts](http://www.highcharts.com).

DRY out your chart code by writing it all in PHP!

[![Build Status](https://travis-ci.org/marcaube/ObHighchartsBundle.png?branch=master)](https://travis-ci.org/marcaube/ObHighchartsBundle)
[![Total Downloads](https://poser.pugx.org/ob/highcharts-bundle/downloads.png)](https://packagist.org/packages/ob/highcharts-bundle)
[![Scrutinizer Quality Score](https://scrutinizer-ci.com/g/marcaube/ObHighchartsBundle/badges/quality-score.png?s=a22d41fd17b944f8275e92c6d5aba27aca2ff18d)](https://scrutinizer-ci.com/g/marcaube/ObHighchartsBundle/)
[![Code Coverage](https://scrutinizer-ci.com/g/marcaube/ObHighchartsBundle/badges/coverage.png?s=3d779351f7ef378fe0f6679809c90c17ad6f11b4)](https://scrutinizer-ci.com/g/marcaube/ObHighchartsBundle/)
[![SensioLabsInsight](https://insight.sensiolabs.com/projects/4cf81d53-f79c-478e-a172-ac2f60b55f02/mini.png)](https://insight.sensiolabs.com/projects/4cf81d53-f79c-478e-a172-ac2f60b55f02)

## Documentation

* [Installation](Resources/doc/installation.md)
* [Usage](Resources/doc/usage.md)
* [Cookbook](Resources/doc/cookbook.md) (See below or in the Coobook for maps charts examples.)
* [Highcharts API](http://api.highcharts.com/highcharts)


## Map chart support added

This is a simple recipe to create an French map chart demo at [highcharts.com/maps/demo/color-axis](http://www.highcharts.com/maps/demo/color-axis)

In the controller file

```php
$ob = new Highmap();
$ob->chart->renderTo('mapchart');
$ob->chart->borderWidth(1);
$ob->title->text('My map chart');
$ob->mapNavigation->enabled(true);
$ob->series(array(
    array(
        'data' => array(
            array('value' => rand(1, 100), 'code' => 'Île-de-France', 'price' => rand(1, 100)),
            array('value' => rand(1, 100), 'code' => 'Bourgogne', 'price' => rand(1, 100)),
            array('value' => rand(1, 100), 'code' => 'Alsace', 'price' => rand(1, 100)),
            array('value' => rand(1, 100), 'code' => 'Centre', 'price' => rand(1, 100)),
        ),
        'name' => 'FR',
        'mapData' => new Expr("Highcharts.maps['countries/fr/fr-all']"),
        'joinBy' => array('name', 'code'),
        'tooltip' => array('pointFormat' => '{point.code}: {point.value}'),
            'dataLabels' => array(
                'enabled' => true,
                'format' => '{point.price}',
            ),
        )
    ));
    // with plotOptions you can add some events like JS functions on map click
    $ob->plotOptions->series(array(
        'events' => array(
            'click' => new Expr(
                "function() {
                    console.log(event.point.code + ' clicked!');
                }"
            )
        ),
        // specify cursor on map hover
        'cursor' => 'pointer',
    ));
```

In the twig file

```javascript
<script src="https://code.highcharts.com/maps/highmaps.js"></script>
<script src="https://code.highcharts.com/mapdata/countries/fr/fr-all.js"></script>
<script type="text/javascript">
    {{ chart(mapchart) }}
</script>
```

```twig
<div id="mapchart" style="height: 500px; min-width: 310px; max-width: 600px; margin: 0 auto"></div>
```

Map chart Result :

![Alt text](img/mapchart.png?raw=true "Map chart result")


## Contributing

See [CONTRIBUTING](CONTRIBUTING.md) file.


## License

ObHighchartsBundle is released under the MIT License. See the bundled [LICENSE](LICENSE) file for details.

Please note that the Highcharts JS library is **not** free for commercial use, see their
[FAQ](http://shop.highsoft.com/faq) for more details on what constitutes a non-commercial project or their
[product page](http://shop.highsoft.com/highcharts.html) for details on pricing.
