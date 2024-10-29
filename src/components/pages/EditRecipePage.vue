<template>
    <main>
        <div class="container-md my-5 py-5">
            <recipe-form
                v-if="detailData && !isLoading" :isEdit="true">
            </recipe-form>
        </div>
    </main>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useStore } from 'vuex';
import { useRoute } from 'vue-router';
import RecipeForm from '../recipeForm/RecipeForm.vue';


const store = useStore();
const route = useRoute();
const detailData = ref();
const isLoading = ref(false);


onMounted(async () => {
    try {
        isLoading.value = true;
        const recipeId = route.params.id;
        await store.dispatch("recipe/getRecipeDetail", recipeId);
        detailData.value =store.state.recipe.recipeDetail;
    } catch (error) {
        console.log(error);
    } finally {
        isLoading.value = false;
    }
});
</script>