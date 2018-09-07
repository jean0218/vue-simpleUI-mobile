<template>
    <div class="range-calendar">
        <div class = "range-calendar-header">
            <input
                class="calendar-input"
                v-bind:value="minValue"
                placeholder="请选择日期"
                @focus="handleInputFocus('min')"
                readonly="readonly"
            />
            <span class="calendar-middle">~</span>
            <input
                class="calendar-input"
                v-bind:value="maxValue"
                placeholder="请选择日期"
                @focus="handleInputFocus('max')"
                readonly="readonly"
            />
        </div>
        <CalendarContentWrap
            v-bind:defaultValue="minValue"
            v-bind:inputSource="inputSource"
            v-if="visibleContent"
            @onConfirm="handleConfirm"
            @onCancel="handleCancel"
        />
    </div>

</template>
<script>
import './style/rangeCalendar.css';
import CalendarContentWrap from './CalendarContentWrap';
import {DateTime} from 'simple-datetime-utils';
export default {
    name: 'RangeCalendar',    
    components: {
        CalendarContentWrap
    },
    props: {
        validRange: {
            type: Array
        },
        rangeValue: {
            type: Array,
            default: function(){
                const now = new DateTime().getDate();
                return [now, now]
            }
        },
    },
    data() {
        return{
            minValue: this.rangeValue[0],
            maxValue: this.rangeValue[1],
            visibleContent: false,
            inputSource:''//调用来源
        }
    },
    methods: {
        handleInputFocus(newSatus) {
            this.visibleContent = true; 
            this.inputSource = newSatus;                       
        },
        handleCancel(){
            this.visibleContent = false;
        },
        handleConfirm(newData, type){
            this.visibleContent = false;
            this[`${type}Value`] = newData;
            this.$emit('onChange', [this.minValue, this.maxValue]);
        }      
    }
}
</script>
