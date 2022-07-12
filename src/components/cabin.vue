<template>
    <div :class="{ cabin_relaxation: arr[this.column - 1].isRelaxation }" class="cabin cabin_size cabin_position">
        <cabinScoreboard
        :arr="arr"
        :column="column"
        :nextFloor="nextFloor"
        :draw="draw"
        />
    </div>
</template>

<script>
import cabinScoreboard from '@/components/cabinScoreboard.vue'

export default {

    components: {
        cabinScoreboard
    },

    props: {
        commonNextFloor: {
            type: Array,
        },
        nextColumn: {
            type: Number,
        },
        column: {
            type: Number,
        },
        arr: {
            type: Array,
        },
        startParam: {
            type: Boolean,
        },
        queue: {
            type: Array,
        },
        fakeQueue: {
            type: Array,
        },
    },

    data() {
        return {
            height: 50,
            nextFloor: 1,
            draw: true,
        }
    },

    watch: {
        startParam: {
            handler() {
                if (this.nextColumn + 1) {
                    if (this.column === this.nextColumn + 1) {
                        this.go();
                    }
                } else {
                    if (this.arr.filter(item => item.isActive).find(item => item.index === this.column - 1)) {
                        this.go();
                    }
                }
            },
            immediate: true,
        },
    },

    mounted() {
        this.$el.style.bottom = String(this.arr[this.column - 1].height) + 'px';
    },

    methods: {
        go() {
            let h = 0;
            let deltah = Math.round(this.arr[this.column - 1].height - this.arr[this.column - 1].floorNumber * 50);
            this.draw = deltah < 0;
            this.nextFloor = this.arr[this.column - 1].floorNumber;
            
            let timer = setInterval(() => {
                this.$el.style.bottom = String(this.arr[this.column - 1].height) + 'px';

                if (Math.abs(h) >= Math.abs(deltah)) {
                    this.arr[this.column - 1].isRelaxation = true;
                    if (deltah) {
                        this.fakeQueue.splice(this.fakeQueue.indexOf(this.nextFloor), 1);
                    }

                    setTimeout(() => {
                        this.arr[this.column - 1].isRelaxation = false;
                        this.arr[this.column - 1].isActive = false;
                        this.queue.splice(this.queue.indexOf(this.nextFloor), 1);
                    }, 3000);
                    clearInterval(timer);
                } else {
                    if (deltah > 0) {
                        this.arr[this.column - 1].height -= 2;
                        h -= 2;
                    } else {
                        this.arr[this.column - 1].height += 2;
                        h += 2;
                    }
                }
            }, 40)
        }
    }
}
</script>

<style>

.cabin {
    display: flex;
    justify-content: center;
    position: relative;
    background-color: rgb(246, 255, 0);
}

.cabin_size {
    width: 50px;
    height: 50px;
}

.cabin_position {
    width: 50px;
    height: 50px;
    bottom: 50px;
    left: 4px;
}

.cabin_relaxation {
    animation: flicker 1s infinite
}

@keyframes flicker {
    from { opacity: 1; }
    to { opacity: 0.3; }
  }

</style>