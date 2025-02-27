<template>
   <div v-if="isOpen" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50" @click="closeModal">
    <div class="bg-white rounded-lg w-11/12 max-w-2xl max-h-[90vh] overflow-y-auto shadow-xl" @click.stop>
      <div class="flex justify-between items-center border-b border-gray-200 p-4">
        <h2 class="text-xl font-semibold">{{ game ? 'Edit Game' : 'Add New Game' }}</h2>
        <button class="text-gray-500 hover:text-gray-800 text-2xl font-bold" @click="closeModal">&times;</button>
      </div>
      
      <div class="p-6">
        <form @submit.prevent="saveGame">
          <div class="mb-4">
            <label for="title" class="block text-sm font-medium text-gray-700 mb-1">Title</label>
            <input 
              id="title" 
              v-model="formData.title" 
              type="text" 
              required
              placeholder="Game title"
              class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500"
            />
          </div>
          
          <div class="mb-4">
            <label for="thumbnail" class="block text-sm font-medium text-gray-700 mb-1">Thumbnail URL</label>
            <input 
              id="thumbnail" 
              v-model="formData.thumbnail" 
              type="url" 
              required
              placeholder="https://example.com/image.jpg"
              class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500"
            />
          </div>
          
          <div class="mb-4">
            <label for="short_description" class="block text-sm font-medium text-gray-700 mb-1">Short Description</label>
            <textarea 
              id="short_description" 
              v-model="formData.short_description" 
              required
              placeholder="Brief game description"
              rows="3"
              class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500"
            ></textarea>
          </div>
          
          <div class="mb-4">
            <label for="game_url" class="block text-sm font-medium text-gray-700 mb-1">Game URL</label>
            <input 
              id="game_url" 
              v-model="formData.game_url" 
              type="url" 
              required
              placeholder="https://example.com/game"
              class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500"
            />
          </div>
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
            <div>
              <label for="genre" class="block text-sm font-medium text-gray-700 mb-1">Genre</label>
              <input 
                id="genre" 
                v-model="formData.genre" 
                type="text" 
                required
                placeholder="Genre"
                class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500"
              />
            </div>
            
            <div>
              <label for="platform" class="block text-sm font-medium text-gray-700 mb-1">Platform</label>
              <input 
                id="platform" 
                v-model="formData.platform" 
                type="text" 
                required
                placeholder="Platform"
                class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500"
              />
            </div>
          </div>
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
            <div>
              <label for="publisher" class="block text-sm font-medium text-gray-700 mb-1">Publisher</label>
              <input 
                id="publisher" 
                v-model="formData.publisher" 
                type="text" 
                required
                placeholder="Publisher"
                class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500"
              />
            </div>
            
            <div>
              <label for="developer" class="block text-sm font-medium text-gray-700 mb-1">Developer</label>
              <input 
                id="developer" 
                v-model="formData.developer" 
                type="text" 
                required
                placeholder="Developer"
                class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500"
              />
            </div>
          </div>
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
            <div>
              <label for="release_date" class="block text-sm font-medium text-gray-700 mb-1">Release Date</label>
              <input 
                id="release_date" 
                v-model="formData.release_date" 
                type="date" 
                required
                class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500"
              />
            </div>
            
            <div>
              <label for="profile_url" class="block text-sm font-medium text-gray-700 mb-1">Profile URL</label>
              <input 
                id="profile_url" 
                v-model="formData.profile_url" 
                type="url" 
                required
                placeholder="https://example.com/profile"
                class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500"
              />
            </div>
          </div>
          
          <div class="flex justify-end space-x-3">
            <button 
              type="button" 
              class="px-4 py-2 bg-gray-200 text-gray-800 rounded-md hover:bg-gray-300 transition-colors" 
              @click="closeModal"
            >
              Cancel
            </button>
            <button 
              type="submit" 
              class="px-4 py-2 bg-red-800 text-white rounded-md hover:bg-indigo-700 transition-colors"
            >
              Save Game
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, computed, watch } from 'vue';

const props = defineProps({
  isOpen: {
    type: Boolean,
    default: false
  },
  game: {
    type: Object,
    default: null
  }
});

const emit = defineEmits(['close', 'save']);

// Create form data with defaults
const defaultFormData = {
  id: null,
  title: '',
  thumbnail: '',
  short_description: '',
  game_url: '',
  genre: '',
  platform: '',
  publisher: '',
  developer: '',
  release_date: '',
  profile_url: ''
};

const formData = ref({...defaultFormData});
watch(() => props.game, (newGame) => {
  if (newGame) {
    if (formData.value.release_date) {
      const date = new Date(formData.value.release_date);
      if (!isNaN(date.getTime())) {
        formData.value.release_date = date.toISOString().split('T')[0];
      }
    }
  } else {
    resetForm();
  }
}, { immediate: true });

watch(() => props.isOpen, (isOpen) => {
  if (!isOpen) {
    resetForm();
  }
});

function resetForm() {
  formData.value = {...defaultFormData};
}

function closeModal() {
  emit('close');
}

function saveGame() {
  if (!formData.value.id) {
  }
  
  emit('save', {...formData.value});
  closeModal();
}
</script>

<style>

</style>