<script>
import './style/calendarContentItem.css';
export default {
    name: 'CalendarContentItem',
    props: {
        list: {
            type: Array,
            default: function(){
               return []
            }
        },
        defaultValue: {
            type: Object,
            default: function(){
               return {}
            }
        }
    },
    methods: {
        handleTdClick(event) {
            this.$emit('onChange', event.target.getAttribute('data-value'));
        }
    },
    render(h) {
        const { list, defaultValue, handleTdClick } = this;
        let tdDom = [], thisDom = [], itemDom;
        return (
            <div class="calendar-item">
                <div class="calendar-item-header">{defaultValue.y}年{defaultValue.m + 1}月</div>
                <table class = "calendar-table">
                    <thead>
                        <tr>
                            <th>日</th>
                            <th>一</th>
                            <th>二</th>
                            <th>三</th>
                            <th>四</th>
                            <th>五</th>
                            <th>六</th>
                        </tr>
                    </thead>
                    <tbody>
                        {
                            list.map(function(item, index){
                                itemDom = item.value.length !== 0 ? <td><span class={item.class} key={`td-${item.value}`} data-value={item.value} onClick={handleTdClick}>{item.text}</span></td> : <td></td>
                                tdDom.push(itemDom)
                                if(index !== 0 && (index + 1) % 7 === 0){
                                    thisDom = tdDom;
                                    tdDom = [];
                                    return(
                                        <tr>
                                            {thisDom}
                                        </tr>
                                    )
                                }
                            })
                        }
                    </tbody>
                </table>
            </div>
        )
    }
}
</script>
