<script setup>
import { Head, Link } from '@inertiajs/vue3';
import NavLayout from '@/Layouts/NavLayout.vue';
import VideoCard from '@/Components/VideoCard.vue';
import { onMounted } from 'vue';
import { toRefs } from 'vue';

const props = defineProps({
    videos: Array,
    keyword: String
})

const { videos, keyword } = toRefs(props)

onMounted(() => {
    // console.log(videos.value.length);
    if(keyword.value) {
        document.getElementById("searchInput").value = keyword.value;
    }
})
</script>

<template>
    <Head title="Youtube" />

    <NavLayout>
        <div v-if="videos.length" class="w-[100%]">
            <div class="grid 2xl:grid-cols-5 xl:grid-cols-4 lg:grid-cols-3 md:grid-cols-3 sm:grid-cols-2">
                <div v-for="video, index in videos" :key="video">
                    <Link :href="route('videos.show', { id: video.id })">
                        <VideoCard
                            :title="video.title"
                            :user="video.user"
                            :views="video.views"
                            :image="`https://picsum.photos/id/${index}/100`"
                            :videoUrl="video.video"
                            :thumbnail="video.thumbnail"
                        />
                    </Link>
                </div>
            </div>
        </div>
        <div v-else class="text-red-400 w-[100%] text-center">
            <p>There is no search result.</p>
        </div>
    </NavLayout>
</template>

<style>

</style>
