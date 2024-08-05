<template>
    <div class="image-item">
      <img :src="image.src" :alt="image.alt" @click="selectImage" />
      <button class="delete-button" @click.stop="deleteImage">❌</button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      image: {
        type: Object,
        required: true,
      },
      index: {
        type: Number,
        required: true,
      },
    },
    methods: {
      selectImage() {
        this.$emit('select', this.image);
      },
      deleteImage() {
        this.$emit('delete', this.index);
      },
    },
  };
  </script>
  
  <style scoped>
  .image-item {
    position: relative;
    overflow: hidden;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }
  
  .image-item:hover {
    transform: scale(1.05);
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
  }
  
  .image-item img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 10px;
  }
  
  .delete-button {
    position: absolute;
    top: 10px;
    right: 10px;
    background-color: #ff4d4d;
    border: none;
    color: white;
    border-radius: 50%;
    width: 30px;
    height: 30px;
    font-size: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .delete-button:hover {
    background-color: #cc0000;
  }
  </style>
  