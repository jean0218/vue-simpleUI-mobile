<template>
    <div class="calendar-content-header">
        <span @click="$emit('onCancel')"><i class="iconfont">&#xe628;</i></span>
        <b>选择日期</b>
        <span @click="$emit('onConfirm')">确定</span>
    </div>
</template>
<script>
export default {
    name: 'CalendarContentHeader'
}
</script>