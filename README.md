# element时间选择器 实现本月二十一号之前本月不可选 之后可选

```vue
<template>
	<el-date-picker
                    v-model="params.statementDate"
                    type="month"
                    format="yyyy-MM"
                    value-format="yyyy-MM"
                    placeholder="选择月"
                    :picker-options="pickerOptions">
    </el-date-picker>
</template>
<script>
    export default {
        data() {
            let that = this;
            return {
                params: {
                    statementDate: ""
                },
                pickerOptions: {
                    disabledDate(time) {
                        //先获取本月二十一号的时间
                        let cal = new Date()
                        let now = new Date()
                        cal.setDate(21)
                        cal.setHours(0)
                        cal.setMinutes(0)
                        cal.setSeconds(0)
                        cal.setMilliseconds(0)
                        let calTimeVal = cal.getTime()
                        let nowTimeVal = now.getTime()
                        let val = new Date()
                        let month = null
                        //判断当前时间是否小于本月二十一号的时间
                        if (nowTimeVal < calTimeVal) {
                            //if true 则只能选择本月之前时间
                            month = now.getMonth() - 1
                            month = month < 1 ? 12 : month
                        } else {
                            //else 可以选择本月
                            month = now.getMonth()
                        }
                        val.setMonth(month)
                        val.setDate(1)
                        val.setHours(0)
                        val.setMinutes(0)
                        val.setSeconds(0)
                        val.setMilliseconds(0)
                        return time.getTime() > val.getTime()
                    }
                }
            }
        }
</script>
```

