<template>

</template>

<script defer>
    export default {
        name: "map",
        methods: {
            initMap: function () {
                var platform = new H.service.Platform({
                'app_id': 'y0fwQjbIby4yR6IpY7JO',
                'app_code': '0z6_tBhCaH41eAbiiTDbVw'
            });

            var mapLayers = platform.createDefaultLayers();

            var map = new H.Map(
                document.getElementById('mapContainer'),
                mapLayers.normal.map,
                {
                    zoom: 10,
                    center: {
                         lng: 30.2, lat: 60
                    }
                });

            var mapEvents = new H.mapevents.MapEvents(map);
            var behavior = new H.mapevents.Behavior(mapEvents);

            // map UI
            var ui = H.ui.UI.createDefault(map, mapLayers, 'ru-RU');
            var mapSettings = ui.getControl('mapsettings');
            var zoom = ui.getControl('zoom');
            var scalebar = ui.getControl('scalebar');
                
            mapSettings.setAlignment('top-left');
            zoom.setAlignment('middle-left');
            scalebar.setAlignment('top-left');	

            // console.log(mapSettings.getLocalization());

            var moveToLocation = (map, latNum, lngNum) => {
                map.setCenter({lat: latNum, lng: lngNum});
                map.setZoom(14);
            };


            document.addEventListener('click', () => {
                // Attach an event listener to map display
                // obtain the coordinates and display in an alert box.
                map.addEventListener('tap', function (evt) {
                    var coord = map.screenToGeo(evt.currentPointer.viewportX,
                            evt.currentPointer.viewportY);
                    alert('Clicked at ' + Math.abs(coord.lat.toFixed(4)) +
                        ((coord.lat > 0) ? 'N' : 'S') +
                        ' ' + Math.abs(coord.lng.toFixed(4)) +
                            ((coord.lng > 0) ? 'E' : 'W'));
                });
            });
            }
        }
    }
</script>
