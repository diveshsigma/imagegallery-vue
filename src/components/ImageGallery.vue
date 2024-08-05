<template>
  <div class="gallery">
    <h1 class="gallery-heading">My Image Gallery</h1>
    <div class="input-container">
      <input
        v-model="newImageUrl"
        type="text"
        placeholder="Enter image URL"
      />
      <button @click="addImage">Add Image</button>
    </div>
    <div class="gallery-grid">
      <ImageItem
        v-for="(image, index) in filteredImages"
        :key="index"
        :image="image"
        :index="index"
        @select="handleSelect"
        @delete="deleteImage"
      />
    </div>
    <div v-if="selectedImage" class="lightbox" @click="closeLightbox">
      <img :src="selectedImage.src" :alt="selectedImage.alt" />
    </div>
  </div>
</template>

<script>
import ImageItem from './ImageItem.vue';

export default {
  components: { ImageItem },
  data() {
    return {
      images: [
        { src: 'https://via.placeholder.com/300?text=Image+1', alt: 'Image 1' },
        { src: 'https://via.placeholder.com/300?text=Image+2', alt: 'Image 2' },
        { src: 'https://via.placeholder.com/300?text=Image+3', alt: 'Image 3' },
      ],
      selectedImage: null,
      newImageUrl: '',
    };
  },
  computed: {
    filteredImages() {
      return this.images;
    },
  },
  methods: {
    handleSelect(image) {
      this.selectedImage = image;
    },
    closeLightbox() {
      this.selectedImage = null;
    },
    addImage() {
      if (this.newImageUrl.trim() !== '') {
        this.images.push({
          src: this.newImageUrl.trim(),
          alt: `Image ${this.images.length + 1}`
        });
        this.newImageUrl = ''; // Clear the input field
      }
    },
    deleteImage(index) {
      this.images.splice(index, 1);
    },
  },
};
</script>

<style scoped>
.gallery {
  position: relative;
  max-width: 1200px;
  margin: auto;
  padding: 20px;
  background-color: #f0f0f0;
}

.gallery-heading {
  text-align: center;
  color: #333;
  margin-bottom: 20px;
  font-size: 2em;
  font-weight: bold;
}

.input-container {
  text-align: center;
  margin-bottom: 20px;
}

.input-container input {
  padding: 10px;
  font-size: 16px;
  width: 60%;
  max-width: 500px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.input-container button {
  padding: 10px 20px;
  font-size: 16px;
  margin-left: 10px;
  border: none;
  border-radius: 5px;
  background-color: #007bff;
  color: white;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.input-container button:hover {
  background-color: #0056b3;
}

.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 15px;
}

.lightbox {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
}

.lightbox img {
  max-width: 90%;
  max-height: 80%;
  border-radius: 10px;
}
</style>
