<script setup>
    import { ref, watch, computed } from 'vue';
    var props = defineProps({
        end: {
            type: Number,
            required: true
        },
        refresh: {
            type: Number,
            default: 50
        }
    });

    const gts = () => new Date().getTime();

    function format(ms) {
        const MILLISECOND = 1,
            SECOND = MILLISECOND * 1000,
            MINUTE = SECOND * 60,
            HOUR = MINUTE * 60,
            DAY = HOUR * 24,
            MONTH = DAY * 30,
            YEAR = MONTH * 12;
        var year = 0, 
            month = 0, 
            day = 0, 
            hour = 0, 
            minute = 0, 
            second = 0, 
            millisecond = 0, 
            millisecond0 = '000', 
            only = {
                year: 0,
                month: 0,
                day: 0,
                hour: 0,
                minute: 0,
                second: 0,
                millisecond: 0
            };
        // 只计算单独的值
        only = {
            year: (ms / YEAR).toFixed(2),
            month: (ms / MONTH).toFixed(2),
            day: (ms / DAY).toFixed(2),
            hour: (ms / HOUR).toFixed(2),
            minute: (ms / MINUTE).toFixed(2),
            second: (ms / SECOND).toFixed(2),
            millisecond: (ms).toFixed(2)
        };
        // 依次计算年月日时分秒
        if (ms > YEAR) {
            // 若存在"年"
            // 得到有多少年
            year = ~~(ms / YEAR);
            // 将ms减去已获取到的年数的毫秒数
            ms = ms - (year * YEAR);
        }
        // 月
        if (ms > MONTH) { month = ~~(ms / MONTH); ms = ms - (month * MONTH); }
        // 日
        if (ms > DAY) { day = ~~(ms / DAY); ms = ms - (day * DAY); }
        // 时
        if (ms > HOUR) { hour = ~~(ms / HOUR); ms = ms - (hour * HOUR); }
        // 分
        if (ms > MINUTE) { minute = ~~(ms / MINUTE); ms = ms - (minute * MINUTE); }
        // 秒
        if (ms > SECOND) { second = ~~(ms / SECOND); ms = ms - (second * SECOND); }
        // 毫秒
        millisecond = ms;
        millisecond0 = ms
        if (millisecond0 < 10) millisecond0 = '0' + millisecond0;
        if (millisecond0 < 100) millisecond0 = '0' + millisecond0;
        // 返回
        return { 
            year, month, day, hour, minute, second, millisecond, millisecond0, only
        };
    }

    var bind = ref({});
    var nowTimestamp, timestampDiff;

    const endTimestampMs = props.end > 1_000_000_000 ? props.end : props.end * 1000;
    bind.value = format(0);
    setInterval(() => {
        nowTimestamp = gts();
        timestampDiff = endTimestampMs - nowTimestamp;
        bind.value = format(timestampDiff);
    }, props.refresh);
</script>

<template>
    <slot v-bind="bind">
    </slot>
</template>

<!-- 
    占位符	输出	详情
    YY	18	两位数的年份
    YYYY	2018	四位数的年份
    M	1-12	月份，从 1 开始
    MM	01-12	月份，两位数
    MMM	Jan-Dec	缩写的月份名称
    MMMM	January-December	完整的月份名称
    D	1-31	月份里的一天
    DD	01-31	月份里的一天，两位数
    d	0-6	一周中的一天，星期天是 0
    dd	Su-Sa	最简写的星期几
    ddd	Sun-Sat	简写的星期几
    dddd	Sunday-Saturday	星期几
    H	0-23	小时
    HH	00-23	小时，两位数
    h	1-12	小时, 12 小时制
    hh	01-12	小时, 12 小时制, 两位数
    m	0-59	分钟
    mm	00-59	分钟，两位数
    s	0-59	秒
    ss	00-59	秒 两位数
-->