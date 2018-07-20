<template>
    <div class="countdown-container">
        <div class="countdown">
            <div v-for="(time, index) in destination" :class="'present-'+index" class="clock orange blink dest">{{ time }}</div>
            <div v-for="(time, index) in present" :class="'present-'+index" class="clock green pres">{{ time }}</div>
            <div v-for="(time, index) in lastDeparted" :class="'present-'+index" class="clock yellow lastDep">{{ time }}</div>
        </div>
    </div>
</template>

<script>
    const floor = Math.floor;
    export default {
        name: "clock",
    data() {
        // init as null
        return {
            time: null,
            // target
            targetTime: new Date(2018, 6, 30, 19, 0),
            // last departed
            last: new Date(1985, 6, 3, 12, 0),
            // how fast to tick
            interval: 1000,
            now: moment.utc().format('X'),
            timestamp: moment.utc(this.countdownDate).format('X')
        }
    },
    props: {
        countdownDate: {
            coerce: str => moment(this.countdownDate).format('MMM DD YYYY HH mm')
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
        height: 1080px;
        background-image: url('../assets/clockface.jpg');
        background-size: contain;
        background-repeat: no-repeat;
        width: 1920px;
        background-position: center;

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
            font-size: 12.4rem;
            position: absolute;
            letter-spacing: 6px;
        }

        .active {
            position: absolute;
        }

        .pres {
            top: 424px;
        }

        .dest {
            top: 58px;
        }

        .lastDep {
            bottom: 46px;
        }

        .present-0 {
            right: 1700px;
        }

        .present-1 {
            right: 1603px;
        }

        .present-2 {
            right: 1506px;
        }

        .present-4 {
            right: 1316px;
        }

        .present-5 {
            right: 1216px;
        }

        .present-7 {
            right: 1029px;
        }

        .present-8 {
            right: 931px;
        }

        .present-9 {
            right: 831px;
        }

        .present-10 {
            right: 731px;
        }

        .present-12 {
            right: 489px;
        }

        .present-13 {
            right: 391px;
        }

        .present-15 {
            right: 198px;
        }

        .present-16 {
            right: 99px;
        }
    }
</style>


