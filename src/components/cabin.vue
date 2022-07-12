<template>
    <div :class="{ cabin_relaxation: isRelaxation }" class="cabin cabin_size cabin_position">
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
            isRelaxation: false,
            nextFloor: 1,
            draw: true,
        }
    },

    // mounted() {
    //     this.height = JSON.parse(sessionStorage.getItem("height")) || 50
    //     this.isRelaxation = JSON.parse(sessionStorage.getItem("isRelaxation")) || false
    //     this.nextFloor = JSON.parse(sessionStorage.getItem("nextFloor")) || 1
    //     this.draw = JSON.parse(sessionStorage.getItem("draw")) || true
    // },

    watch: {
        startParam() {
            if (this.column === this.nextColumn + 1) {
                let h = 0;
                let deltah = Math.round(this.height / 50 - this.commonNextFloor[0]);
                this.draw = deltah < 0;
                this.arr[this.column - 1].floorNumber = this.commonNextFloor[0];
                this.nextFloor = this.commonNextFloor[0];
                this.commonNextFloor.shift();
                
                let timer = setInterval(() => {
                    this.$el.style.bottom = String(this.height + h) + 'px';

                    if (Math.abs(h) >= Math.abs(deltah) * 50) {
                        this.height += h;
                        this.isRelaxation = true;
                        this.fakeQueue.splice(this.fakeQueue.indexOf(this.nextFloor), 1);

                        setTimeout(() => {
                            this.isRelaxation = false;
                            this.arr[this.column - 1].isActive = false;
                            this.queue.splice(this.queue.indexOf(this.nextFloor), 1);
                        }, 3000);
                        clearInterval(timer);
                    } else {
                        if (deltah > 0) {
                            h -= 2;
                        } else {
                            h += 2;
                        }
                    }
                }, 40)
            }
        },

        // height(newValue) {
        //     sessionStorage.setItem("height", JSON.stringify(newValue));
        // },
        
        // isRelaxation(newValue) {
        //     sessionStorage.setItem("isRelaxation", JSON.stringify(newValue));
        // },

        // nextFloor(newValue) {
        //     sessionStorage.setItem("nextFloor", JSON.stringify(newValue));
        // },

        // draw(newValue) {
        //     sessionStorage.setItem("draw", JSON.stringify(newValue));
        // },

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