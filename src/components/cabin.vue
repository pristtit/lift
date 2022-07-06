<template>
    <div class="column__cabin column__cabin_size"></div>
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
            t: null,
        }
    },
    watch: {
        startParam() {
            try {
                if (this.column === this.chek + 1){
                    console.log('iter');
                    let h = 0;
                    let deltah = Math.round(this.x / 50 - this.arr[this.column - 1].floorNumber[0]);
                    console.log(deltah);
                    let timer = setInterval(function() {
                        this.$el.style.bottom = String(this.x + h) + 'px';
                        if (Math.abs(h) >= Math.abs(deltah) * 50) {
                            this.x += h;
                            console.log(this.x); 
                            clearInterval(timer);
                        } else {
                            if (deltah > 0) {
                                h -= 5;
                            } else {
                                h += 5;
                            }
                        }
                    }.bind(this), 10);
                }
            } catch(err) { console.log(err) }
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
</style>