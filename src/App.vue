<template>
  <div id="app" class="app">
    <Calendar 
    	defaultValue="2018-08-12"
    	@onChange="handleChangeCalendar"
    >
    </Calendar>
    <div class="top2">
    </div>
    <RangeCalendar
        v-bind:rangeValue="rangeValue"
        @onChange="handleChangeRangeCalendar"
    >
    </RangeCalendar> 
  </div>
</template>
<script>
import './assets/style/app.css';
import {Calendar, RangeCalendar} from './components/index.js';
export default {
    name: 'app',
    components: {
        Calendar,
        RangeCalendar
    },
    data() {
        return{
            rangeValue:['2018-08-12', '2018-08-12']
        }
    },
    methods: {
        handleChangeCalendar(newStatus) {
            console.log('newStatus', newStatus)
        },
        handleChangeRangeCalendar(newStatus) {
            console.log('newStatus', newStatus)
        }
    }
}
</script>
