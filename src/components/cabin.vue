<template>
    <div class="column__cabin column__cabin_size">{{ go }}</div>
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
        }
    },
    data() {
        return {
            x: 50,
            floor: Math.abs(Math.floor(this.x / 50) - this.arr[column - 1].floorNumber[0]),
        }
    },
    computed: {
        go() {
            try {
                if (this.column === this.chek + 1){
                    this.$el.style.background = 'red';
                    let start = Date.now();
                    let timer = setInterval(function() {
                        this.x += 5;
                        let timePassed = Date.now() - start;
                        this.$el.style.bottom = String(x) + 'px';
                        if (x > 50) clearInterval(timer);
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