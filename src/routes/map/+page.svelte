<script>

    import L from 'leaflet'
    import { browser } from '$app/environment'
    
    let map

    function mapInit() {
        if (browser) {
            const icon = L.icon({
                iconUrl: 'https://img.freepik.com/free-vector/location_53876-25530.jpg?size=626&ext=jpg',
                iconSize:     [28, 40],
                iconAnchor:   [14, 40]
            })
            map = L.map('map', {scrollWheelZoom: false}).setView([37.535661, 13.037825], 15)
            let layer = new L.TileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png')
            let marker = L.marker([37.535661, 13.037825], {icon: icon}).addTo(map)
            map.addLayer(layer)

            return {
                destroy: () => {
                    map.remove()
                    map = null
                }
            }
        }
    }

</script>

<svelte:head>
    <script src="https://unpkg.com/leaflet@1.9.3/dist/leaflet.js" integrity="sha256-WBkoXOwTeyKclOHuWtc+i2uENFpDZ9YPdf5Hf+D7ewM=" crossorigin=""></script>
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css" integrity="sha512-xodZBNTC5n17Xt2atTPuE1HxjVMSvLVW9ocqUKLsCC5CXdbqCmblAshOMAS6/keqq/sMZMZ19scR4PsZChSR7A==" crossorigin=""/>
</svelte:head>

<section id="map" use:mapInit />

<style>
    #map {
        height: 100vh;
    }
</style>