<template>
    <div>
        <div v-if="showLoader">
            <loader></loader>
        </div>
        <div v-else>
            <div class="main">
                <input type="text" v-model="search" placeholder="Search Title" />
                <div class="header">
                    <p class="sNum">S.no</p>
                    <p class="title">Title</p>
                    <p class="completed">Completed</p>
                </div>
                <div class="searchNoFound" v-if="DisplayArray.length <= 0">
                    <span>No results found</span>
                </div>
                <div class="list" v-for="data in DisplayArray" :key="data.id">
                    <p class="sNum">{{ data.id }}</p>
                    <p class="title">{{ data.title }}</p>
                    <p class="completed">{{ data.completed }}</p>
                </div>
            </div>
            <div class="buttton">
                <button @click="showPreview()">Preview</button>
                <div class="pageButton">
                    <button @click="page(1)">1</button>
                    <button @click="page(2)">2</button>
                    <button @click="page(3)">3</button>
                    <button @click="page(4)">4</button>
                    <button @click="page(5)">5</button>
                    <button @click="page(6)">6</button>
                    <button @click="page(7)">7</button>
                    <button @click="page(8)">8</button>
                    <button @click="page(9)">9</button>
                    <button @click="page(10)">10</button>
                </div>
                <button @click="showNext()">Next</button>
            </div>
        </div>
    </div>
</template>

<script>
import Loader from "./Loader.vue";
import axios from "axios";
export default {
    name: "home",
    components: {
        Loader,
    },
    data() {
        return {
            data: "",
            search: "",
            showLoader: true,
            start: 0,
            end: 10,
            numberOfItemPerPage: 10,
        };
    },
    methods: {
        showNext() {
            if (this.data.length > this.end) {
                this.start = this.start + this.numberOfItemPerPage;
                this.end = this.end + this.numberOfItemPerPage;
            }
        },
        showPreview() {
            if (this.end > this.numberOfItemPerPage) {
                this.start = this.start - this.numberOfItemPerPage;
                this.end = this.end - this.numberOfItemPerPage;
            }
        },
        page(value) {
            this.start = this.numberOfItemPerPage * value - this.numberOfItemPerPage;
            this.end = this.numberOfItemPerPage * value;
        },
    },

    created() {
        axios.get("https://jsonplaceholder.typicode.com/todos").then((response) => {
            this.data = response.data;
            this.showLoader = false;

            console.log(response.data);
        });
    },
    computed: {
        DisplayArray() {
            return this.data.filter((data) => data.title.toLowerCase().includes(this.search.toLowerCase())).slice(this.start, this.end);
        },
    },
};
</script>

<style scoped>
.main {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    /* padding: 20px; */
    font-family: "Abhaya Libre";
    font-size: 22px;
}
.list {
    display: flex;
    width: 70%;
    border-right: 2px solid rgb(226, 223, 223);
    border-bottom: 2px solid rgb(226, 223, 223);
}
.sNum {
    width: 15%;
}
.title {
    width: 100%;
}
.completed {
    width: 25%;
}
.header {
    display: flex;
    width: 70%;
    border-right: 2px solid rgb(226, 223, 223);
    border-top: 2px solid rgb(226, 223, 223);
    border-bottom: 2px solid rgb(226, 223, 223);
}
.header p {
    height: 20px;
    font-size: 20px;
    font-weight: 700;
    padding-bottom: 30px;
}
p {
    border-left: 2px solid rgb(226, 223, 223);
    margin: 0px;
    padding: 8px;
    width: 50%;
    font-weight: 550;
}
.main input {
    width: 70%;
    height: 40px;
    margin-bottom: 10px;
    border: 2px solid rgb(226, 223, 223);
    outline: none;
    padding-left: 30px;
}
.buttton {
    display: flex;
    justify-content: space-evenly;
    margin: 30px;
}
.buttton button {
    height: 35px;
    width: 80px;
    font-weight: 600;
    cursor: pointer;
}
.pageButton {
    display: flex;
}
.pageButton button {
    width: 45px;
    height: 40px;
    margin: 2px;
}
.searchNoFound {
    margin: 80px 0px 50px 0px;
}
</style>
