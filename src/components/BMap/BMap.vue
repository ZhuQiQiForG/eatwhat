<template>
	<div class="BMap" id="BMapContainer">
	</div>
</template>

<script type="text/ecmascript-6">
	import BMap from 'BMap';
	const BMAP_STATUS_SUCCESS = 0;

	export default {
		mounted() {
			this.drawMap(500);
		},
		methods: {
			drawMap(distance, random) {
				let p = distance;
				let map = new BMap.Map('BMapContainer');
				let geolocation = new BMap.Geolocation();
				map.setMapStyle({style: 'midnight'});
				geolocation.getCurrentPosition(function(r) {
					if (this.getStatus() === BMAP_STATUS_SUCCESS) {
						map.centerAndZoom(r.point, 15);
						let mk = new BMap.Marker(r.point);
						map.addOverlay(mk);
						map.panTo(r.point);
						let circle = new BMap.Circle(r.point, p, {fillColor: 'blue', strokeWeight: 1, fillOpacity: 0.3, strokeOpacity: 0.3});
						map.addOverlay(circle);
						let options = {
							onSearchComplete: function(results) {
								if (local.getStatus() === BMAP_STATUS_SUCCESS) {
									for (let i = 0; i < results.getCurrentNumPois(); i++) {
										let marker = new BMap.Marker(results.getPoi(i).point);
										map.addOverlay(marker);
										let opts = {
											width: 200,
											height: 80,
											title: results.getPoi(i).title
										};
										let infoWindow = new BMap.InfoWindow(results.getPoi(i).address, opts);
										marker.addEventListener('click', function() {
											map.openInfoWindow(infoWindow, results.getPoi(i).point);
											// 开启信息窗口
										});
									}
									if (random) {
											map.clearOverlays();
											map.addOverlay(mk);
											console.log(results.getCurrentNumPois());
											let randomNum = Math.random() * results.getCurrentNumPois();
											randomNum = Math.floor(randomNum) + 1;
											let newMarker = new BMap.Marker(results.getPoi(randomNum).point);
											map.addOverlay(newMarker);
											let opts = {
												width: 200,
												height: 80,
												title: results.getPoi(randomNum).title
											};
											let infoWindow = new BMap.InfoWindow(results.getPoi(randomNum).address, opts);
											map.openInfoWindow(infoWindow, results.getPoi(randomNum).point);
										}
								}
							}
						};
						var local = new BMap.LocalSearch(map, options, {renderOptions: {map: map, autoViewport: false}});
						local.searchNearby('酒吧', r.point, p);
					} else {
						alert('failed' + this.getStatus());
					}
				}, {enableHighAccuracy: true});
				let geolocationControl = new BMap.GeolocationControl();
				map.addControl(geolocationControl);
				map.addControl(new BMap.NavigationControl());
			}
		}
	};
</script>

<style lang="stylus" rel="stylesheet/stylus">
	.BMap
		width: 100%
		height: 100%
</style>