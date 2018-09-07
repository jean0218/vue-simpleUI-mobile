<template>
    <div>
    <div>{{defaultValue}}</div>
    <CalendarContent 
        v-bind:defaultValue="defaultValue"
        @onConfirm="handleConfirm"
        @onCancel="handleCancel"
    />
</div>
</template>
<script>
import CalendarContent from './CalendarContent';
export default {
    name: 'CalendarContentWrap',
    props: {
        inputSource: { // 调用来源
            type: String,
            default: ''
        },
        defaultValue: {
            type: String,
        }
    },
    components:{
        CalendarContent
    },
    methods: {
        handleCancel() {
            this.$emit('onCancel', '', this.inputSource);
        },
        handleConfirm(newStatus) {
            this.$emit('onConfirm', newStatus, this.inputSource);
        }        
    },
}
</script>
