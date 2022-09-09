<script setup>
    import CountDown from '../components/CountDown.vue';
    const DATE_OBJ = new Date();
    const MONTH = DATE_OBJ.getMonth() + 1;
    const DATE = DATE_OBJ.getDate()
    var Sep25stYear = DATE_OBJ.getFullYear();
    // 判断下次925在下一年还是这一年
    if (MONTH > 9 || (MONTH == 9 && DATE >= 25)) Sep25stYear++;
    const Sep25stTimestamp = new Date(Sep25stYear + '-09-25 00:00:00').getTime()
</script>

<template>
    <div class="index">
        <div class="middle">
            <div class="container">
                <CountDown 
                    :end="Sep25stTimestamp"
                    v-slot="slotProps"
                >
                    <h1>距离{{Sep25stYear}}年9月25日还有</h1>
                    <p>
                        <span v-if="slotProps.year"><span class="num">{{slotProps.year}}</span>年</span>
                        <span v-if="slotProps.month"><span class="num">{{slotProps.month}}</span>个月</span>
                        <span v-if="slotProps.day"><span class="num">{{slotProps.day}}</span>天</span>
                        <span v-if="slotProps.hour"><span class="num">{{slotProps.hour}}</span>小时</span>
                        <span v-if="slotProps.minute"><span class="num">{{slotProps.minute}}</span>分钟</span>
                        <span v-if="slotProps.second"><span class="num">{{slotProps.second}}</span>秒</span>
                        <span class="num">{{slotProps.millisecond0}}</span>毫秒
                    </p>
                    <p class="alias">
                        也就是
                        <span class="num">{{slotProps.only.day}}</span>天 或 
                        <span class="num">{{slotProps.only.hour}}</span>小时 或 
                        <span class="num">{{slotProps.only.minute}}</span>分钟 或 
                        <span class="num">{{slotProps.only.second}}</span>秒
                    </p>
                </CountDown>
            </div>
        </div>
    </div>
</template>

<style lang="less" scoped>
    .index {
        display: flex;
        flex-direction: column;
        height: 100%;
        .num {
            font-family: 'pixel';
            margin: 0.2em;
        }
        .middle {
            display: flex;
            justify-content: center;
            align-items: center;
            flex: 1;
            font-size: large;
            .container {
                h1, 
                p {
                    text-align: center;
                }
                .alias {
                    font-size: small;
                }
            }
        }
    }
</style>