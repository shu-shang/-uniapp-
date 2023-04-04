<template>
    <view class="content">
        <scroll-view id="scrollview" scroll-y="true" :scroll-top="scrollTop" style="height: 90%;">
            <view class="uni-chatMsgCnt" id="msglistview">
                <div v-for="item in message " class="{{ item.viewclass }}">
                    {{ item.viewtext }}
                </div>
                <!-- <div class="chat-left">这是一个对话框鸭！</div>
                <div class="chat-right">这是一个对话框鸭！</div>
                <div class="chat-left">这是一个对话框鸭！</div>
                <div class="chat-right">这是一个对话框鸭！</div>
                <div class="chat-left">这是一个对话框鸭！</div>
                <div class="chat-right">这是一个对话框鸭！</div>
                <div class="chat-left">这是一个对话框鸭！</div>
                <div class="chat-right">这是一个对话框鸭！</div>
                <div class="chat-left">这是一个对话框鸭！</div>
                <div class="chat-right">这是一个对话框鸭！</div>
                <div class="chat-left">这是一个对话框鸭！</div>
                <div class="chat-right">这是一个对话框鸭！</div>
                <div class="chat-left">这是一个对话框鸭！</div>
                <div class="chat-right">这是一个对话框鸭！</div>
                <div class="chat-left">这是一个对话框鸭！</div>
                <div class="chat-right">这是一个对话框鸭！</div>
                <div class="chat-left">这是一个对话框鸭！</div>
                <div class="chat-right">这是一个对话框鸭！</div>
                <div class="chat-left">这是一个对话框鸭！</div>
                <div class="chat-right">这是一个对话框鸭！</div>
                <div class="chat-left">这是一个对话框鸭！</div>
                <div class="chat-right">这是一个对话框鸭！</div>
                <div class="chat-left">这是一个对话框鸭！</div>
                <div class="chat-right">这是一个对话框鸭！</div> -->
            </view>
        </scroll-view>
        <div class="chat-box">
            <input type="text" v-model="inpitText">
            <button @click="sendMessage">Send</button>
        </div>
    </view>
</template>

<script>
import { send } from 'process'

export default {
    data() {
        return {
            title: 'Hello',
            scrollTop: 0,
            inpitText:'',
            message:[
                {
                    viewclass:"chat-left",
                    viewtext:"这是一个对话框鸭！"
                },
                {
                    viewclass:"chat-right",
                    viewtext:"这是一个对话框鸭！"
                },
                {
                    viewclass:"chat-left",
                    viewtext:"这是一个对话框鸭！"
                },
                {
                    viewclass:"chat-right",
                    viewtext:"这是一个对话框鸭！"
                }
            ]
        }
    },
    onLoad() {

    }, mounted() {
        this.scrollToBottom()
    },
    updated() {
        this.scrollToBottom()
    },
    methods: {
        // 滚动至聊天底部
        scrollToBottom(t) {
            let that = this
            let query = uni.createSelectorQuery()
            query.select('#scrollview').boundingClientRect()
            query.select('#msglistview').boundingClientRect()
            query.exec((res) => {
                // console.log(res)
                if (res[1].height > res[0].height) {
                    that.scrollTop = res[1].height - res[0].height
                }
            })
        },
        sendMessage(){
            if(this.inpitText){
                this.message.push({viewclass:'chat-right',viewtext: this.inpitText})
                this.inpitText = ''
            }
        }
    },
    watch:{
        message:{
            handler (){
                deep:true
            }
        }
    }
}
</script>

<style>
.content {
    position: absolute;
    width: 100%;
    height: 100%;
}
#scrollview,#msglistview{
    width: 100%;
    margin: 0;
    padding:0;
}

.chat-left {
    position: relative;
    margin-top: 1%;
    margin-left: 2%;
    padding-left: 1%;
    width: 80%;
    line-height: 2;
    background: lightblue;
    color: #fff;
    border-radius: 4px;
}

.chat-left::before {
    content: '';
    position: absolute;
    border: 8px solid;
    border-color: transparent lightblue transparent transparent;
    left: -16px;
    top: 8px;
}

.chat-right {
    position: relative;
    /* float: right; */
    right: -17%;
    margin-top: 1%;
    margin-right: 2%;
    padding-left: 1%;
    width: 80%;
    line-height: 2;
    background: lightblue;
    color: #fff;
    border-radius: 4px;
}

.chat-right::before {
    content: '';
    position: absolute;
    border: 8px solid;
    border-color: transparent transparent  transparent lightblue ;
    right: -16px;
    top: 8px;
}


.chat-box {
    position: fixed;
    bottom: 0px;
    width: 100%;
    height: 8%;
    background-color: aliceblue;
}

.chat-box>input {
    margin: 1% 1%;
    padding-left: 2%;
    float: left;
    display: inline-block;
    width: 80%;
    height: 85%;
    border-radius: 15px;
    background-color: azure;
}

.chat-box>button {
    margin: 1% 0 1% 1%;
    float: left;
    display: flex;
    align-items: center;
    width: 15%;
    height: 85%;
    border-radius: 5px;
    font-size: 12px;
    text-align: center;
    line-height: 100%;
    /* display: inline-block; */
    background-color: #9EEA6A;
}
</style>
