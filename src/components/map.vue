<template>
    <div id = "mapContainer">

    </div>
</template>

<script>
    var platform = new H.servive.Platform({
        'app_id': 'y0fwQjbIby4yR6IpY7JO',
        'app_code': '0z6_tBhCaH41eAbiiTDbVw'
    });

    var mapLayers = platform.createDefaultLayers();

    var map = new H.map(
        document.getElementById('mapContainer'),
        mapLayers.normal.map,
        {
            zoom: 10,
            center: {
                lat: 60.000973, lng: 30.289268
            }
        });
</script>
