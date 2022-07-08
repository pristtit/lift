<template>
    <div :class="{ cabin_relaxation: isRelaxation }" class="cabin cabin_size"></div>
</template>

<script>
export default {

    props: {
        nextColumn: {
            type: Number,
        },
        nextFloor: {
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
        }
    },

    data() {
        return {
            x: 50,
            isRelaxation: false,
        }
    },

    watch: {
        startParam() {
            if (this.column === this.nextColumn + 1) {
                let h = 0;
                let deltah = Math.round(this.x / 50 - this.queue[0]);
                this.arr[this.column - 1].floorNumber = this.queue[0];
                this.queue.shift();

                let timer = setInterval(() => {
                    this.$el.style.bottom = String(this.x + h) + 'px';

                    if (Math.abs(h) >= Math.abs(deltah) * 50) {
                        this.x += h;
                        this.isRelaxation = true;

                        setTimeout(() => {
                            this.isRelaxation = false;
                            this.arr[this.column - 1].isActive = false;
                        }, 3000);
                        clearInterval(timer);
                    } else {
                        if (deltah > 0) {
                            h -= 5;
                        } else {
                            h += 5;
                        }
                    }
                }, 10)
            }
        }
    }
}
</script>

<style>

.cabin {
    display: inline-block;
    position: relative;
    background-color: blue;
    bottom: 50px;
    left: 4px;
}

.cabin_size {
    width: 50px;
    height: 50px;
}

.cabin_relaxation {
    animation: flicker 1s infinite
}

@keyframes flicker {
    from { opacity: 1; }
    to { opacity: 0.3; }
  }

</style>