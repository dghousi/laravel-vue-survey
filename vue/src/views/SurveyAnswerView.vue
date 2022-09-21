<template>
  <PageComponent title="Result">
    <div v-if="loading" class="flex justify-center">Loading...</div>

    <div
      v-else
      class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5 text-gray-700">

        <DashboardCard class="order-1 lg:order-1" style="animation-delay: 0.2s">
            <template v-slot:title>Survey</template>
            <div
            class="text-4xl pb-4 font-semibold flex-1 flex items-center justify-center"
            >
            {{survey?.title}}
            </div>
        </DashboardCard>
        <DashboardCard class="order-1 lg:order-1" style="animation-delay: 0.2s">
            <template v-slot:title>Survey Question & Answers</template>
            <div v-if="currentSurveyResult?.length" class="text-left">
            <a
                href="#"
                v-for="question of currentSurveyResult"
                :key="question.id"
                class="block p-2 hover:bg-gray-100/90"
            >
                <div class="font-semibold">{{ question?.question }}</div>
                <small>
                Answerskk:
                <i class="font-semibold">{{ question?.answer }}</i>
                </small>
            </a>
            </div>
            <div v-else class="text-gray-600 text-center py-16">
            Your don't have answers yet
            </div>
        </DashboardCard>

    </div>
  </PageComponent>
</template>



<script setup>
    import DashboardCard from "../components/core/DashboardCard.vue";
    import PageComponent from "../components/PageComponent.vue";
    import { computed } from "vue";
    import {  useStore } from "vuex";
    import { useRoute } from "vue-router";
    
    const store = useStore();
    const route = useRoute();

    const loading = computed(() => store.state.dashboard.loading);

    const currentSurveyResult = computed(() => store.state.currentSurveyResult.data);
    
    const survey = computed(() =>  store.state.currentSurvey.data);

    if (route.params.id) {
        store.dispatch("getSurvey", route.params.id);
        store.dispatch("getSurveyResult", route.params.id);
    }

    </script>
    
    <style scoped></style>