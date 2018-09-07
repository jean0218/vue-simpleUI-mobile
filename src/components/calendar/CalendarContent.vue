<template>
    <Touch 
        class="calendar-content" 
        @onPageDown="handlePage('down')"
        @onPageUp="(newStatus) => {
            this.handlePage('up', newStatus)
        }" 
    >
        <CalendarContentHeader
            @onCancel="handleCancel"
            @onConfirm="handleConfirm"
        />
        <div class="calendar-content-body" v-if="dateList.length">
            <CalendarContentItem
                v-for="item in dateList"
                v-bind:defaultValue="item.title"
                v-bind:list="item.list"
                @onChange="handleChangeDay"
            />                                       
        </div>
    </Touch>
</template>
<script>
import './style/calendarContent.css';
import {dateTime, dateUtil} from 'simple-datetime-utils';
import {Touch} from 'vue-simple-libs';
import CalendarContentHeader from './CalendarContentHeader';
import CalendarContentItem from './CalendarContentItem';
export default {
    name: 'CalendarContent',
    props: {
        validRange: {
            type: Array,
            default: function(){
                return ['1900-01-01', '2090-12-31']
            }
        },
        defaultValue: {
            type: String,
            default: function(){
                return new DateTime().getDate();
            }
        }
    },
    components: {
        Touch,
        CalendarContentHeader,
        CalendarContentItem
    },
    data() {
        return{
            selectValue: this.defaultValue,
            dateList:[],
            dateValueList:[],
        }
    },
    mounted() {
        this.handleInputFocus();
    },
    methods: {
        handleCancel() {
            this.$emit('onCancel', '');
        },
        handleConfirm() {
            this.$emit('onConfirm', this.selectValue);
        },
        handleInputFocus() {
            const { dateValueList } = this;
            let endList;         
            endList = this.handledateValueList('current', dateValueList);
            endList = this.handledateValueList('down', endList);
            this.dateValueList = endList;
            this.dateList = this.goShowDateList(endList);
        },
        handlePage(type, newStatus){
            const { dateValueList } = this;
            this.dateValueList = this.handledateValueList(type, dateValueList, newStatus);
            this.dateList = this.goShowDateList(this.dateValueList);
        },
        handledateValueList(type, valueList, newStatus = true){
            const {selectValue, dateValueList} = this;
            switch(type){
                case 'current':
                    valueList.push({'dateValue':selectValue});
                    break;
                case 'down':
                    valueList.push({'dateValue':dateTime.nextMonth(dateValueList[dateValueList.length - 1].dateValue)});
                    break;
                case 'up':
                    if(!newStatus.refresh){
                        valueList.unshift({'dateValue':dateTime.prevMonth(dateValueList[0].dateValue)});
                    }
                    break;
                default:
            };
            return dateValueList;
        },
        goShowDateList(prelist){
            const {dateValueList, validRange} = this;
            let dateList = [], dateItem = {};
            prelist.map(({dateValue}) =>{
                dateItem.list = dateTime.getCalendarDays(dateValue, validRange[0], validRange[1]);
                dateItem.title = dateUtil.toObject(dateValue);
                dateList.push(dateItem);
                dateItem = {};
            });
            return dateList;
        },
        handleChangeDay(value) {
            this.selectValue = value;
        }
    }
}
</script>
