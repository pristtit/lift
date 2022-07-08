<template>
    <div :class="{ relaxation: isRelaxation }" class="column__cabin column__cabin_size"></div>
</template>

<script>
export default {
    props: {
        chek: {
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
            try {
                if (this.column === this.chek + 1 && this.arr[this.column - 1].isActive){
                    
                    async function ima() {
                        this.arr[this.column - 1].isActive = false;
                        let h = 0;
                        let deltah = Math.round(this.x / 50 - this.arr[this.column - 1].floorNumber[1]);
                        this.arr[this.column - 1].floorNumber.shift();

                        let time = new Promise((resolve) => {
                            let timer = setInterval(() => {
                            this.$el.style.bottom = String(this.x + h) + 'px';
                            if (Math.abs(h) >= Math.abs(deltah) * 50) {
                                this.x += h;
                                this.isRelaxation = true;
                                setTimeout(() => {
                                    this.isRelaxation = false;
                                    this.$emit('cabineActive', this.column);
                                    resolve('r');
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
                        });

                        let wait = await time;
                        if (this.arr[this.column - 1].floorNumber.length > 1) {
                            ima.call(this);
                        }
                    }
                    ima.call(this);
                }
            } catch(err) { console.log('er') }
        }
    }
}
</script>

<style>

.column__cabin {
    display: inline-block;
    position: relative;
    background-color: blue;
    bottom: 50px;
    left: 4px;
}
.column__cabin_size {
    width: 50px;
    height: 50px;
}

.gogo {
    left: 10px;
}
 

.test {
    right: 30px;
}

.relaxation {
    animation: flicker 1s infinite
}

@keyframes flicker {
    from { opacity: 1; }
    to { opacity: 0.3; }
  }
</style>