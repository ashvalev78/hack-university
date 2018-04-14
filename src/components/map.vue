<template>

</template>

<script defer>
    export default {
        name: "map",
        data() {
            return {
                globMap
            };
        },
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
                        zoom: 11,
                        center: {
                            lng: 30.2, lat: 60
                        }
                });

                this.globMap = map;
                // console.log(this.globMap);

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

                // var moveToLocation = (map, latNum, lngNum) => {
                //     map.setCenter({lat: latNum, lng: lngNum});
                //     map.setZoom(14);
                // };

                // Attach an event listener to map display
                // obtain the coordinates and display in an alert box.
                
            },
            addMarker: function () {

                globMap.addEventListener('tap', function cb(evt) {
                    var coord = globMap.screenToGeo(evt.currentPointer.viewportX,
                            evt.currentPointer.viewportY);
                    console.log(coord);
                    // Define a variable holding SVG mark-up that defines an icon image:
                    var svgMarkup = '<svg width="24" height="24" ' +
                    'xmlns="http://www.w3.org/2000/svg">' +
                    '<rect stroke="white" fill="#1b468d" x="1" y="1" width="22" ' +
                    'height="22" /><text x="12" y="18" font-size="12pt" ' +
                    'font-family="Arial" font-weight="bold" text-anchor="middle" ' +
                    'fill="white">H</text></svg>';

                    // Create an icon, an object holding the latitude and longitude, and a marker:
                    var icon = new H.map.Icon(svgMarkup),
                    marker = new H.map.Marker(coord, {icon: icon});

                    // Add the marker to the map and center the map at the location of the marker:
                    globMap.addObject(marker);
                    evt.currentTarget.removeEventListener(evt.type, cb);
                });
            }
        }
    }
</script>
