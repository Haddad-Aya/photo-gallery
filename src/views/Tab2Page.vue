<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Photo Gallery</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 2</ion-title>
        </ion-toolbar>
      </ion-header>
    </ion-content>
    <ion-content :fullscreen="true">
      <ion-fab vertical="bottom" horizontal="center" slot="fixed">
        <ion-fab-button @click="takePhoto()">
          <ion-icon :icon="camera"></ion-icon>
        </ion-fab-button>
      </ion-fab>
    </ion-content>
    <ion-content>
  <ion-grid>
    <ion-row>
      <ion-col size="6" v-for="(photo,phot) in photos" :key="phot" >
        <ion-img :src="photo.webviewPath"></ion-img>
        <ion-img :src="photo.webviewPath" @click="showActionSheet(photo)"></ion-img>
      </ion-col>
    </ion-row>
    
  </ion-grid>

  <!-- <ion-fab> markup  -->
</ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { camera, trash, close } from 'ionicons/icons';
import { IonPage,IonHeader,IonFab,IonFabButton,IonIcon,IonToolbar,IonTitle,IonContent,IonGrid,IonRow,IonCol,IonImg,actionSheetController } from '@ionic/vue';
import { UserPhoto ,usePhotoGallery } from '@/components/usePhotoGallery';

export default defineComponent({
  name: 'Tab2Page',
  components: { 
    IonPage,
    IonHeader,
    IonFab,
    IonFabButton,
    IonIcon,
    IonToolbar,
    IonTitle,
    IonContent,
    IonGrid,
    IonRow,
    IonCol,
    IonImg,
  },
  setup() {
    const { takePhoto,photos,deletePhoto, } = usePhotoGallery();
    const showActionSheet = async (photo: UserPhoto) => {
  const actionSheet = await actionSheetController.create({
    header: 'Photos',
    buttons: [
      {
        text: 'Delete',
        role: 'destructive',
        icon: trash,
        handler: () => {
          deletePhoto(photo);
        },
      },
      {
        text: 'Cancel',
        icon: close,
        role: 'cancel',
        handler: () => {
          // Nothing to do, action sheet is automatically closed
        },
      },
    ],
  });
  await actionSheet.present();
};
    return {
      takePhoto,
      photos,
      camera,
      trash,
      close,
      showActionSheet,
    };
  },
});


</script>
