<template>
    <div class="day" v-bind:class="[{active: activeClass}, dayClass]" @click="handleClick">
        <div class="date">
            {{ day.date }}
        </div>
        <div class="day-string">
            <!--{{ day.day}}-->
        </div>
    </div>
</template>
<script>
    export default {
        name: 'Day',
        props: {
            day: {
                type: Object,
                default: () => {}
            }
        },
        data: () => ({
            activeClass: false,
        }),
        computed: {
            dayClass: function () {
                return {
                    weekend: this.isWeekend()
                }
            },
        },
        methods: {
            isWeekend () {
                if (this.day.day === 'Saturday' || this.day.day === 'Sunday') {
                    return true;
                }
            },
            handleClick () {
                if (this.day.day !== '') {
                    this.$emit('dayClick', this.day);
                    this.activeClass = true;
                }
            }
        }
    }
</script>
<style lang="scss">
    $dayWidth: 6rem;
    .date {
        margin: .5rem;
    }
    .day-string {
        margin: .5rem;
    }
    .day {
        width: $dayWidth;
        height: $dayWidth;
        border: .001rem solid gainsboro;
    }
    .day:hover {
        cursor: pointer;
        background-color: lightyellow;
        color: black;
    }
    .weekend {
        background-color: cornflowerblue;
        color: gainsboro;
    }
    .active {
        background-color: green;
        color: gainsboro;
    }
</style>