<template>
    <div id="root">
        <div id="month-year-wrapper">
            <div id="year">
                {{ this.year}}
            </div>
            <div id="time">
                {{ this.time }}
            </div>
        </div>
        <div id="calendar-wrapper">
            <div class="day-wrapper" v-for="(day, index) in days" v-bind:key="index">
                <Day
                    :day="day"
                    @dayClick="handleDaySelect"
                >
                </Day>
            </div>
        </div>
    </div>
</template>
<script>
    import moment from 'moment';
    import Day from './Day';
    import momenttimezone from 'moment-timezone';
    export default {
        name: 'Dashboard',
        components: {
          Day
        },
        props: {
            msg: String
        },
        data: () => ({
            days: [],
            mom: moment,
            selected: {},
            year: '',
            time: '',
            timezone: 'America/New_York',
        }),
        mounted () {
            this.initDateTimeData()
            this.setTime();
            setInterval(this.setTime, 1000);
        },
        methods: {
            handleDaySelect (selected) {
                this.selected = selected
                /* eslint-disable no-console */
                console.log(selected);
            },
            initDateTimeData () {
                this.getMonths()
                this.formatDays()
            },
            getMonths () {
                let lengthOfMonth = moment().daysInMonth()
                let dayArray = [];

                for (let i = 1; i < lengthOfMonth; i++) {
                    let currentDay = moment().format("YYYY-MM-" + i);
                    let dayObj = {}
                    dayObj.date = moment(currentDay).format("DD");
                    dayObj.day = moment(currentDay).format("dddd");
                    dayObj.fullDate = currentDay;
                    dayArray.push(dayObj);
                }
                this.days = dayArray;
            },
            formatDays () {
                const firstDayOfMonth = moment(this.days[0].fullDate).day();
                for (let i = firstDayOfMonth; i > 0; i--) {
                    let dayObj = {}
                    dayObj.date = '';
                    dayObj.day = '';
                    dayObj.fullDate = '';
                    this.days.unshift(dayObj);
                }

                const lastDayOfMonth = moment(this.days[this.days.length - 1].fullDate).day();
                for (let i = lastDayOfMonth; i < 6; i++) {
                    let dayObj = {}
                    dayObj.date = '';
                    dayObj.day = '';
                    dayObj.fullDate = '';
                    this.days.push(dayObj);
                }
            },
            setTime () {
                let time = momenttimezone().tz(this.timezone);
                this.year = time.format('h:mm:ss a');
                this.time = time.format('MMMM Do YYYY');
            }
        }
    }
</script>
<style lang="scss">
    $dayWidth: 6.5rem;
    #calendar-wrapper {
        width: 100%;
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
    }
    #root {
        width: calc(7 *  #{$dayWidth});
        margin-left: auto;
        margin-right: auto;
    }
    #month-year-wrapper {
        width: 100%;
        font-size: 1.3rem;
        font-weight: 600;
        display: flex;
        flex-direction: row;
        justify-content: space-evenly;
        margin-bottom: .5rem;
        margin-top: .5rem;
    }
    #time {
        margin-left: 2rem;
        margin-right: 2rem;
    }
    #year {
        margin-left: 2rem;
        margin-right: 2rem;
    }
</style>
