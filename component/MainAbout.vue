<template>
  <div class="bg_image">
    <div class="container">
      <h1 class="text_c">LATEST EPISODES</h1>
      <div>
        <img
          src="../assets/images/uzbekistan-absolute-image-2.jpg"
          class="abs_image"
          alt="no image"
        />
      </div>
      <div class="flex gap-5 p-3 items-center justify-center media_f">
        <div
          v-for="banner in mobileBanners.slice(0, 1)"
          :key="banner.id"
          class="p-2 hover:rounded-lg cursor-pointer duration-150"
        >
          <NuxtLink
            :href="banner.link"
            target="_blank"
            rel="noopener noreferrer"
          >
            <div class="col-md-6 col-lg-4">
              <div class="item animated wow fadeIn">
                <img
                  :src="banner.banner_thumbnail.medium"
                  class="rounded-lg m-auto object-cover"
                  :alt="`Banner ${banner.id}`"
                />
                <div class="overlay fade-overlay"></div>
              </div>
            </div>
            <!-- <p class="text-primary text-[16px] text-center mt-2">
            {{ banner.id }}
          </p> -->
          </NuxtLink>
        </div>
        <!-- <div v-for="banner in mobileBanners.slice(0, 4)" :key="banner.id">
        {{ banner.id }}
      </div> -->
        <!-- <div v-if="videoTitle" class="text-center mt-5">
      <h2>Video Title: {{ videoTitle }}</h2>
    </div> -->

        <div class="flex flex-col">
          <div v-for="items in text" :key="items">
            <div class="text-white flex flex-col">
              <NuxtLink
                :to="`/products/${items.title.toLowerCase()}/${items.id}`"
              >
                <div class="text_g">
                  <h1 class="text_h1">
                    {{
                      items.name == "OZBEKISTONLIK"
                        ? "O'ZBEKISTONLIK"
                        : items.name
                    }}
                  </h1>
                  <p class="text_p">{{ items.title }}</p>
                </div>
              </NuxtLink>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const { data: bannersData } = await useFetch(
  "https://uzbekistans.club/api/v1/banners_mobile/?format=json"
);

const mobileBanners = computed(() => {
  if (!bannersData.value || !bannersData.value.results) return [];
  return bannersData.value.results;
});

async function fetchYouTubeVideoTitle(videoId, apiKey) {
  const url = `https://www.googleapis.com/youtube/v3/videos?id=${videoId}&key=${apiKey}&part=snippet`;

  try {
    const response = await fetch(url);
    const data = await response.json();

    if (data.items.length === 0) {
      throw new Error("Video not found");
    }

    return data.items[0].snippet.title;
  } catch (error) {
    console.error("Error fetching YouTube video:", error.message);
    return null;
  }
}

function getVideoId(url) {
  const regex =
    /(?:https?:\/\/)?(?:www\.)?(?:youtube\.com\/(?:[^\/\n\s]+\/\S+\/|(?:v|e(?:mbed)?)\/|.*[?&]v=)|youtu\.be\/)([a-zA-Z0-9_-]{11})/;
  const matches = url.match(regex);
  return matches ? matches[1] : null;
}

const videoId = getVideoId("https://www.youtube.com/watch?v=QkrMop0xGCE");
console.log(bannersData.value.results);
const apiKey = "AIzaSyA0fF8lH9No9fDHkWzrLuGZ9XPZa3Lnr8U";

const videoTitle = ref(null);

fetchYouTubeVideoTitle(videoId, apiKey)
  .then((title) => {
    videoTitle.value = title;
  })
  .catch((err) => {
    console.error("Error:", err);
  });

const text = [
  {
    id: 11,
    name: "O'zbekistonlik. Students | Episode 1",
    title: "STUDENTS",
  },
  {
    id: 2,
    name: "O'zbekistonlik | Episode 3 | Official Teaser | (4K)",
    title: "OZBEKISTONLIK",
  },
  {
    id: 3,
    name: "O'zbekistonlik | Episode 2",
    title: "OZBEKISTONLIK",
  },
  {
    id: 4,
    name: "O'zbekistonlik | Episode 2 | Official Teaser",
    title: "OZBEKISTONLIK",
  },
];
</script>

<style lang="scss" scoped>
// .bg_image {
//   background-color: #111;
// }
.abs_image {
  position: absolute;
  margin-left: -195px;
  top: 650px;
}
.text_c {
  position: relative;
  display: flex;
  align-items: start;
  font-size: 45px;
  font-weight: 700;
  margin-top: 100px;
  color: #fff;
  z-index: 99;
}
.text_h1 {
  font-size: 19px;
  margin-bottom: 10px;
  transition: 0.5s ease;

  &:hover {
    color: #e3b269;
  }
}
.text_p {
  font-size: 15px;
  margin-bottom: 25px;
  color: #e3b269;
}
.overlay {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  background-color: hsla(43, 68%, 55%, 0.4);
  border: 2px solid #e3b269;
  overflow: hidden;
  width: 100%;
  height: 100%;
  transition: 0.5s ease;
  border-radius: 9px;
}

.item {
  position: relative;
  overflow: hidden;
  margin: 20px 0;
  img {
    width: 1000px;
    height: 100%;
  }
}

.item:hover .overlay {
  bottom: 0;
  height: 100%;
  width: 100%;
}

.top-overlay {
  bottom: 100%;
  height: 0;
}
.item:hover .top-overlay {
  bottom: 0;
}
.bottom-overlay {
  top: 100%;
}

.item:hover .bottom-overlay {
  top: 0;
}

.right-overlay {
  left: 100%;
  height: 100%;
}

.item:hover .right-overlay {
  left: 0;
}

.left-overlay {
  right: 100%;
  height: 100%;
  left: auto;
}

.item:hover .left-overlay {
  right: 0;
}
.fade-overlay {
  height: 100%;
  opacity: 0;
}

.item:hover .fade-overlay {
  opacity: 1;
}
.title-overlay {
  height: auto;
  top: auto;
  opacity: 0;
}
.item:hover .title-overlay {
  opacity: 1;
  height: auto;
  padding: 50px 0;
}

@media (max-width: 820px) {
  .media_f {
    display: flex;
    flex-direction: column;
  }
}

@media (max-width: 689px) {
  .container {
    max-width: 690px;
  }
}

@media (max-width: 556px) {
  .container {
    padding: 0px;
    max-width: 556px;
  }
  .text_c {
    font-size: 25px;
  }
}
</style>
