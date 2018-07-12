<template>
    <div class="countdown-container">
        <div class="countdown">
            <div v-for="(time, index) in destination" :class="'present-'+index" class="clock orange blink dest">{{ time }}</div>
            <div v-for="(time, index) in present" :class="'present-'+index" class="clock green pres">{{ time }}</div>
            <div v-for="(time, index) in lastDeparted" :class="'present-'+index" class="clock yellow lastDep">{{ time }}</div>
            <!--<small>Diff: {{ weeks.count }}wk {{ days.count }}d {{ hours.count }}h {{ minutes.count }}m {{ seconds.count }}s</small>-->
        </div>
    </div>
</template>

<script>
    const floor = Math.floor;
    export default {
        name: "clock.vue",
    data() {
        // init as null
        return {
            time: null,
            // target
            targetTime: new Date(2018, 6, 15, 19, 30),
            // last departed
            last: new Date(1985, 0, 1, 0, 0),
            // how fast to tick
            interval: 1000
        }
    },
    computed: {
        destination() {
            return moment(this.targetTime).format('MMM DD YYYY HH mm')
        },
        present() {
            return moment(this.time).format('MMM DD YYYY HH mm')
        },
        lastDeparted() {
            return moment(this.last).format('MMM DD YYYY HH mm')
        },
        remainingTime() {
            const timeRemaining = (this.targetTime.getTime() - this.time.getTime()) / this.interval;
            return timeRemaining >= 0 ? timeRemaining : 0
        },
        weeks() {
            return {
                count: floor(this.remainingTime / 604800),
                remainder: this.remainingTime % 604800
            }
        },
        days() {
            return {
                count: floor(this.weeks.remainder / 86400),
                remainder: this.weeks.remainder % 86400
            }
        },
        hours() {
            return {
                count: floor(this.days.remainder / 3600),
                remainder: this.days.remainder % 3600
            }
        },
        minutes() {
            return {
                count: floor(this.hours.remainder / 60),
                remainder: this.hours.remainder % 60
            }
        },
        seconds() {
            return {
                count: floor(this.minutes.remainder),
                remainder: 0
            }
        }
    },
    created() {
        // start the clock
        this.time = new Date()
    },

    watch: {
        // on update, trigger new timeout
        time() {
            setTimeout(
                _ => requestAnimationFrame(
                    _ => (this.time = new Date())
                ),
                this.interval
            )
        }
    }
}
</script>

<style scoped lang="scss">
    @font-face {
        font-family: 'clock-font';
        src: url('../assets/font/digital-7-mono-it.ttf');
    }

    .countdown-container {
        position:relative;
        width: 100vw;
        height: 100vh;
    }

    .countdown {
        position: absolute;
        width: 961px;
        min-height: 60vh;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        padding: 25px 50px;
        background-image: url('../assets/clockface.jpg');
        background-size: cover;
        background-repeat: no-repeat;

        .yellow {
            color: #f4da6c;
        }

        .orange {
            color: #ea5e29;
        }

        .green {
            color: #81f674;
        }

        .blink {
            animation: blink-animation 1s steps(5, start) infinite;
            -webkit-animation: blink-animation 1s steps(5, start) infinite;
        }
        @keyframes blink-animation {
            to {
                visibility: hidden;
            }
        }
        @-webkit-keyframes blink-animation {
            to {
                visibility: hidden;
            }
        }

        .clock {
            font-family: "clock-font", sans-serif, monospaced;
            font-size: 7rem;
            position: absolute;
            letter-spacing: 6px;
        }

        .pres {
            top: 244px;
        }

        .dest {
            top: 37px;
        }

        .lastDep {
            bottom: 29px;
        }

        .present-0 {
            right: 932px;
        }

        .present-1 {
            right: 877px;
        }

        .present-2 {
            right: 821px;
        }

        .present-4 {
            right: 710px;
        }

        .present-5 {
            right: 657px;
        }

        .present-7 {
            right: 550px;
        }

        .present-8 {
            right: 491px;
        }

        .present-9 {
            right: 438px;
        }

        .present-10 {
            right: 379px;
        }

        .present-12 {
            right: 241px;
        }

        .present-13 {
            right: 186px;
        }

        .present-15 {
            right: 75px;
        }

        .present-16 {
            right: 20px;
        }
    }
</style>


<!--var moment = require('moment');-->

<!--export default {-->
<!--mounted() {-->
<!--window.setInterval(() => {-->
<!--this.now = moment.utc().format('X');-->
<!--},1000);-->
<!--},-->

<!--props : {-->
<!--date : {-->
<!--coerce: str => moment.utc(this.date).format('X')-->
<!--}-->
<!--},-->

<!--data() {-->
<!--return {-->
<!--now: moment.utc().format('X'),-->
<!--timestamp: moment.utc(this.date).format('X')-->
<!--}-->
<!--},-->

<!--computed: {-->
<!--seconds() {-->
<!--return (this.timestamp - this.now) % 60;-->
<!--},-->

<!--minutes() {-->
<!--return Math.trunc((this.timestamp - this.now) / 60) % 60;-->
<!--},-->

<!--hours() {-->
<!--return Math.trunc((this.timestamp - this.now) / 60 / 60) % 24;-->
<!--},-->

<!--days() {-->
<!--return Math.trunc((this.timestamp - this.now) / 60 / 60 / 24);-->
<!--}-->
<!--}-->
<!--}-->