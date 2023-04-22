<script>
export default {
	props: {
		data: {
			type: Object,
			required: true
		}		
	}
}
</script>

<template>
    <div id="percipitationContainer">
        <div class="percipitationTile" v-for="element in this.data">
            <div v-if="element.snow">
                <div class="percipitationElement">
                    <span class="rightText percipitationText precipitationTime">{{ new Date(element.dt*1000).getHours().toString().padStart(2, '0') }}:{{ new Date(element.dt*1000).getMinutes().toString().padStart(2, '0') }}</span>
                    <div class="percipitationBarContainer"><div class="percipitationBar" :style="{'width': Math.min(Math.max(element.snow['3h']*10,5), 100).toString()+'%'}"></div></div>
                    <span class="rightText percipitationText">{{ element.rain['3h'] }}mm</span>
                </div>
            </div>
            <div v-if="element.rain">
                <div class="percipitationElement">
                    <span class="rightText percipitationText precipitationTime">{{ new Date(element.dt*1000).getHours().toString().padStart(2, '0') }}:{{ new Date(element.dt*1000).getMinutes().toString().padStart(2, '0') }}</span>
                    <div class="percipitationBarContainer"><div class="percipitationBar" :style="{'width': Math.min(Math.max(element.rain['3h']*10, 5),100).toString()+'%'}"></div></div>
                    <span class="rightText percipitationText">{{ element.rain['3h'] }}mm</span>
                </div>
            </div>
            <div v-if="!element.rain && !element.snow">
                <div class="percipitationElement">
                    <span class="rightText percipitationText precipitationTime">{{ new Date(element.dt*1000).getHours().toString().padStart(2, '0') }}:{{ new Date(element.dt*1000).getMinutes().toString().padStart(2, '0') }}</span>
                    <div class="percipitationBarContainer"><div class="percipitationBar" :style="{'visibility': 'hidden'}"></div></div>
                    <span class="rightText percipitationText">0 mm</span>
                </div>
            </div>
        </div>
    </div>
</template>
