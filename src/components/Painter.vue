<template>
    <div class="painter-app">
        <div v-if="imageSrc" class="show-image" :style="`background-image:url( ${imageSrc} )`">
            <splice v-if="nums > 0" :nums="nums"></splice>
            <div class="action">
                <button @click="splice(2)">2 x 2</button>
                <button @click="splice(4)">4 x 4</button>
            </div>
            <button type="reset" class="reset-button" @click="reset">X</button>
        </div>
        <div v-else class="upload-image">
            <input type="file" @change="upload" id="inputImage"/>
        </div>
    </div>
</template>

<script>
import Splice from './plugin/Splice'
export default {
    data() {
        return {
            imageInfo: {},
            imageSrc: "",
            nums: 0
        };
    },
    computed: {
    },
    methods: {
        upload: function(e){
            let file = e.target.files[0];
            console.log(file)
            let image = new Image();
            let reader = new FileReader();
            this.imageInfo = file;
            reader.readAsDataURL(file)
            reader.onloadend = (e)=> {
                this.imageSrc = e.target.result;
                image.src = this.imageSrc;
                image.onload = function(){
                    // 打印
                    console.log('width:'+image.width+',height:'+image.height)
                }
            }
        },
        splice: function(nums) {
            this.nums = nums
        },
        reset: function(){
            this.imageSrc = ""
        }
    },
    components : {
        Splice
    }
};
</script>

<style lang="scss" scoped>
.painter-app {
    display: flex;
    width: 100vw;
    height: 100vh;
    max-width: 100%;
    max-height: 100%;
    overflow: hidden;
    background-color: #cccccc;
    .upload-image {
        width: 200px;
        height: 200px;
        border: 3px dotted #dadada;
        border-radius: 8px;
        margin: auto;
        position: relative;
        input[type="file"] {
            opacity: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
        }
        &::before{
            content: "点击，上传图片！";
            display: block;
            position: absolute;
            color: #ffffff;
            width: 100%;
            top: 50%;
            z-index: 300;
            font-weight: bold;
            text-shadow: 1px 1px 10px #000000;
            pointer-events:none;
        }
        &::after{
            content: "";
            display: block;
            width: 200px;
            height: 200px;
            filter: blur(3px);
            z-index: 100;
            background-image: url('../assets/painter.png');
            background-size: contain;
            position: absolute;
            left: 0;
            top: 0;
            pointer-events:none;
        }
    }
}


.show-image {
    background-repeat: no-repeat;
    width: 100%;
    background-size: contain;
    margin: auto;
    height: 100%;
    background-position: center;
}

.action {
    position: absolute;
    width: calc(100% - 20px);
    height: 30px;
    bottom: 20px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 10px;
    margin: 10px;
    justify-items: center;
    button {
        width: 100px;
        background-image: linear-gradient(#BDBDBD,#F0F0F0);
        border: none;
        border-radius: 8px;
        color: #ffffff;
        box-shadow: 1px 1px 5px 1px #c1c1c1;
        &:focus {
            border: none;
            outline: none;
        }
        &:active {
            background-image: none;
            background-color: #BDBDBD;
        }
    }
}

.reset-button {
    position: absolute;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    right: 30px;
    top: 30px;
    box-shadow: 1px 1px 3px 3px #d6d6d6;
    text-align: center;
    line-height: 20px;
    border: 1px solid #cccccc;
    color: #cccccc;
}
</style>