<template>
  <v-container>
    <v-row align="center" justify="center" class="text-center">
      <v-col cols="12" xl="6" sm="12">
        <v-img v-if="isImageSelect"
               :src="url"
               contain
               min-width="700"
               min-height="700"
        >
        </v-img>
        <v-img v-else
               src="https://socialistmodernism.com/wp-content/uploads/2017/07/placeholder-image.png?w=640"
               contain
               min-width="700"
               min-height="700">
        </v-img>
      </v-col>
      <v-col cols="12" xl="6" sm="12" >
        <v-file-input
            show-size
            label="Seleccionar imagen"
            v-model="selectedFile"
            @click="selectImage(true)"
            @cancel="selectImage(false)"
        >
        </v-file-input>
        <h2>O</h2>
        <v-container style="height: 20px"></v-container>
        <v-btn color="blue" dark
               @click="selectImage">
          Analizar por webcam
        </v-btn>
        <v-container style="height: 80px"></v-container>

        <v-row justify="center">
          <h3 class="headline">
            La firma se asemeja a la de "{{this.personOwn}}" y es "{{this.isRealSignature}}"
          </h3>
        </v-row>
        <v-container style="height: 80px"></v-container>
        <v-btn
        @click="predictSignature">
          analizar
        </v-btn>

      </v-col>
    </v-row>


  </v-container>
</template>

<script>
import * as tf from '@tensorflow/tfjs';
  export default {
    name: 'Home',

    data: () => ({
      modelReady: false,
      isImageSelect:false,
      personOwn:"--",
      isRealSignature:false,
      selectedFile:null,
    }),

    mounted() {
      let that = this;
      async function loadModel(){
        that.model = await tf.loadLayersModel("http://127.0.0.1:8080/model.json")
        that.modelReady = true;
      }
      loadModel();
    },

    computed: {
      url() {
        if (!this.selectedFile) return
        return URL.createObjectURL(this.selectedFile);
      }
    },
    methods:{
      /*fileSelected(evt) {
        this.isImageSelect = !this.isImageSelect;
        evt.preventDefault()
        console.log(evt);
        this.selectedFile = evt.target.files[0]
      },*/
      predictSignature(){
        const im = new Image()
        im.src = this.url
        const resp = this.model.predict(tf.browser.fromPixels(im,1))
        resp.print()
      },

      selectImage(value){
        this.isImageSelect = value
      }
    }
  }
</script>
