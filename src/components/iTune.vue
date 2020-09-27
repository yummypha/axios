<template>
<div>
    <img src="https://www.brighttv.co.th/wp-content/uploads/2018/02/iTune-Store-%E0%B9%80%E0%B8%95%E0%B8%A3%E0%B8%B5%E0%B8%A2%E0%B8%A1%E0%B8%A2%E0%B8%B8%E0%B8%95%E0%B8%B4%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B9%83%E0%B8%8A%E0%B9%89%E0%B8%87%E0%B8%B2%E0%B8%99%E0%B8%9A%E0%B8%99-Windows-XP-Vista-%E0%B9%81%E0%B8%A5%E0%B8%B0-Apple-TV.jpg" alt="" height="150px" width="500px" class="img-fluid mx-auto" />
    <br />
    <br />
    <div class="row">
        <div class="col">
        </div>
        <div class="col">
            <input class="form-control ds-input " type=" text" v-model="keyword" placeholder="กรุณากรอกชื่อเพลง" />
            <br />
            <button @click="searchData" class="btn btn-danger">Search Music</button>
            <!--{{resultData}} -->
        </div>
        <div class="col">
        </div>
    </div>
    <br />
    <br />
    <div class="row">
        <div class="col-sm"></div>
        <div class="col-sm">
            <b-card-group columns>
                <div v-for="data in resultData" :key="data.trackId">
                    <b-card :title="data.title" :img-src="data.artworkUrl100" img-alt="Image" img-top tag="article" style="max-width: 25rem;" class="mb-2">
                        <b-card-text>{{ data.trackName }}</b-card-text>
                        <b-card-text>{{ data.artistName }}</b-card-text>
                        <audio controls >
                            <source :src="data.previewUrl" type="audio/mpeg" />
                        </audio>
                        <b-button :href="data.trackViewUrl" variant="danger">Play</b-button>
                    </b-card>
                </div>
            </b-card-group>
        </div>
        <div class="col-sm"></div>
    </div>
</div>
</template>

<script>
import axios from "axios";
export default {
    data() {
        return {
            resultData: null,
            keyword: "",
        };
    },
    methods: {
        searchData() {
            axios
                .get(
                    "https://itunes.apple.com/search?term=" + this.keyword + "&limit=15"
                )
                .then((response) => {
                    this.resultData = response.data.results;
                })
                .catch((err) => {
                    console.log(err);
                });
        },
    },
};
</script>

<style>
.card {
    background-image: url('https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcSfjBPnA86reAmrdH7wZ9WVe3jm8rNdqHIzJg&usqp=CAU');
}
</style>
