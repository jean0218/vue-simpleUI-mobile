<template>
    <div class="calendar">
        <div class="calendar-header">
            <input
                class="calendar-input"
                v-bind:value="value"
                placeholder="请选择日期"
                @focus="handleInputFocus"
                readonly="readonly"
            />
        </div>
        <CalendarContent 
            v-bind:defaultValue="value"
            v-bind:validRange="validRange"
            v-if="visibleContent"
            @onConfirm="handleConfirm"
            @onCancel="handleCancel"
        />
    </div>
</template>
<script>
import './style/calendar.css';
import CalendarContent from './CalendarContent';

export default {
    name: 'Calendar',    
    components: {
        CalendarContent
    },
    props: {
        validRange: {
            type: Array
        },
        defaultValue: {
            type: String
        },
    },
    data() {
        return{
            value: this.defaultValue,
            visibleContent: false,
        }
    },
    methods: {
        handleInputFocus() {
            this.visibleContent = true;            
        },
        handleCancel(){
            this.visibleContent = false;
        },
        handleConfirm(newData){
            this.visibleContent = false;
            this.value = newData;
            this.$emit('onChange', newData);
        }      
    },
}
</script>

