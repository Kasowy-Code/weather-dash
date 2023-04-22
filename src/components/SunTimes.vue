<script>
export default {
	props: {
		data: {
			type: Object,
			required: true
		}		
	},
}
</script>

<template>
    <div class="SunTimesContainer">
        <div class="sunTimeTile">
            <div class="sunTileInfo">
                <i class="bi bi-sunrise rightText" style="font-size:3rem;"></i>
                <div>
                    <h4 class="sunEvent">Sunrise</h4>
                    <h3 class="rightText">{{ new Date((data.sys.sunrise + (new Date().getTimezoneOffset() * 60) + data.timezone)*1000).getHours().toString().padStart(2, '0') }}:{{ new Date(data.sys.sunrise*1000).getMinutes().toString().padStart(2, '0') }}</h3>
                </div>
            </div>
            <h3 class="rightText" v-if="new Date(data.sys.sunrise*1000) > new Date(Date.now())">
                In {{ new Date(data.sys.sunrise*1000 - Date.now()).getHours() }} hours
            </h3>
            <h3 class="rightText" v-if="new Date(data.sys.sunrise*1000) <= new Date(Date.now())">
                {{ new Date(Date.now()-data.sys.sunrise*1000).getHours() }} hours ago
            </h3>
        </div>
        <div class="sunTimeTile">
            <div class="sunTileInfo">
                <i class="bi bi-sunset rightText" style="font-size:3rem;margin-right: 1rem;"></i>
                <div>
                    <h4 class="sunEvent">Sunset</h4>
                    <h3 class="rightText">{{ new Date((data.sys.sunset + (new Date().getTimezoneOffset() * 60) + data.timezone)*1000).getHours().toString().padStart(2, '0') }}:{{ new Date(data.sys.sunset*1000).getMinutes().toString().padStart(2, '0') }}</h3>
                </div>
            </div>
            <h3 class="rightText" v-if="new Date(data.sys.sunset*1000) > new Date(Date.now())">
                In {{ new Date(data.sys.sunset*1000 - Date.now()).getHours() }} hours
            </h3>
            <h3 class="rightText" v-if="new Date(data.sys.sunset*1000) <= new Date(Date.now())">
                {{ new Date(Date.now()-data.sys.sunset*1000).getHours() }} hours ago
            </h3>
        </div>
    </div>
</template>
