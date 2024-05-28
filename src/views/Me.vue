<template>
        <div class="container text-center">
            <v-card>
            <div class="row col-12">
                <!-- <v-card-title class="col-12 mx-3"><h2>Abount me</h2></v-card-title> -->
                <cardimage></cardimage>
                <v-card-subtitle class="col-2">
                    <b>
                        <p class="text-end">มหาวิทยาลัย:</p>
                        <p class="text-end">คณะ:</p>
                        <p class="text-end">สาขา:</p>
                        <p class="text-end">งานอดิเรก:</p>
                        <p class="text-end">สิ่งที่ชอบ/ไม่ชอบ:</p>
                        <p class="text-end">จุดแข็ง:</p>
                        <p class="text-end"><br>กีฬาที่ชอบ</p>
                    </b>   
                </v-card-subtitle>
                <v-card-subtitle class="col-3">
                    <p class="text-start">ขอนแก่น วิทยาเขตหนองคาย</p>
                    <p class="text-start">สหวิทยาการ</p>
                    <p class="text-start">วิทยาการคอมพิวเตอร์และสารสนเทศ</p>
                    <p class="text-start">ฟังเพลง /เล่นเกม</p>
                    <p class="text-start">ชอบกินกะเพราเนื้อ/ - </p>
                    <p class="text-start">เป็นคนที่แอทีฟตลอดเวลา ชอบลองทำอะไรใหม่ๆ</p>
                    <p class="text-start">สเก็ตบอร์ด/บาสเกตบอล</p>
                </v-card-subtitle>
            </div>
            <div class="row col-12">
                <v-card-title class="col-12 mx-3">SKILL</v-card-title> 
                <v-card-text class="col-12">
                    <v-chip-group class="sm mx-3" >
                        <v-chip>CSS</v-chip>
                        <v-chip>HTML</v-chip>
                        <v-chip>PHP</v-chip>
                        <v-chip>Ux/Ui Design</v-chip>
                        <v-chip>SQL</v-chip>
                        <v-chip>Photoshop</v-chip>
                    </v-chip-group>
                </v-card-text>
            </div>
            <v-divider class="col-12"></v-divider>
            <div class="row col-12">
                    <v-card-title class="col-7 mx-3">Contect</v-card-title> 
                    <v-card-text class="col-7 text-start mx-3">
                        <v-icon class="sm" color="primary">mdi-facebook</v-icon><span class="btn btn-primary">&nbsp;&nbsp;<a href="https://www.facebook.com/FA.PONGSAKORN/">FA Pongsakorn</a></span><br>
                        <v-icon class="sm" color="pink">mdi-instagram</v-icon><span class="btn btn-primary">&nbsp;&nbsp;<a href="https://www.instagram.com/fa_luke">fa_luke</a></span><br>
                        <v-icon class="sm" color="green">mdi-message-text</v-icon><span class="btn btn-primary">&nbsp;&nbsp;flue_967</span><br>
                        <v-icon class="sm" color="red">mdi-email</v-icon><span class="btn btn-primary">&nbsp;&nbsp;fa.pongsakornaks@gmail.com</span><br>
                        <v-icon class="sm" color="primary">mdi-phone</v-icon><span class="btn btn-primary">&nbsp;&nbsp;098-1362490</span>
                    </v-card-text>
            </div>
            </v-card>    
        </div>
</template>
<script>
import cardimage from'../components/CardImg.vue';
export default {
    components: {
        cardimage
    }

}
</script>

<style>

</style>