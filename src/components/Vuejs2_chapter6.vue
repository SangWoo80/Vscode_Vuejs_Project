<template>
    <!-- <h1>Chapter 6-1. 필터링된 결과</h1> -->
    <div class="chapter6">
        <h1>Chapter 6-1. 필터링된 결과</h1>
        <section>
            <h2>Let's hear some stories!</h2>
            <h3>Alex's stories</h3>
            <ul class="list-group">
                <li v-for="(story, indexNum) in storiesBy('Alex')" :key="indexNum" class="list-group-item">
                    {{story.writer}} asid "{{story.plot}}"
                </li>
            </ul>
            <h3>John's stories</h3>
            <ul class="list-group">
                <li v-for="(story, indexNum) in storiesBy('John')" :key= "indexNum" class="list-group-item">
                    {{story.writer}} asid "{{story.plot}}"
                </li>
            </ul>
        </section>
        <section>
            <h2>Let's hear some famous stories! ({{famous.length}})</h2>
            <ul class="list-group">
                <li v-for="(story, indexNum) in famous" :key="indexNum" class="list-group-item">
                     {{story.writer}} asid "{{story.plot}}" and upvoted {{story.upvotes}} times.
                </li>
            </ul>
        </section>
        <section>
            <label for="query">
                What are yoe looking for ?
            </label>
            <input v-model="query" class="form-control" id="query">
            <h3>Search result:</h3>
            <ul class="list-group">
                <li v-for="(story, indexNum) in search" :key="indexNum" class="list-group-item">
                    {{story.writer}} said "{{story.plot}}"
                </li>
            </ul>
        </section>
        <br>
        <section>
            <h1>Chapter 6-2. 결과정렬</h1>
            <ul class="list-group">
                <li v-for="(story, indexNum) in orderedStories" :key="indexNum" class="list-group-item">
                    {{story.writer}} asid "{{story.plot}}" and upvoted {{story.upvotes}} times.
                </li>
            </ul>
        </section>
        <section>
            <h1>Chapter 6-3. 사용자 정의 필터</h1>
            <ul class="list-group">
                <li v-for="(hero, indexNum) in heroes" :key="indexNum" class="list-group-item">
                    {{ hero | snitch }}
                </li>
            </ul>
        </section>
    </div>    
</template>

<script>
import Vue from 'vue'

Vue.filter('snitch', function(hero) {
    return hero.secretId + ' is '
        + hero.firstname + ' '
        + hero.lastname + ' in real life!'
});

export default {
    data() {
        return {
            storyes: [
                {
                    plot: "I crashed my car today!",
                    writer: "Alex",
                    upvotes: 28
                },
                {
                    plot: "Yesterday, someone stole my bas!",
                    writer: "John",
                    upvotes: 8
                },
                {
                    plot: "Someone ate my chocolte...",
                    writer: "Alex",
                    upvotes: 51
                },
                {
                    plot: "I ate someone's chocolate!",
                    writer: "John",
                    upvotes: 74
                }
            ],
            query: '',
            heroes: [
                {firstname:'Bruce', lastname:'Wayne',secretId:'Batman'},
                {firstname:'Clark', lastname:'Kent',secretId:'Superman'},
                {firstname:'Jay', lastname:'Garrick',secretId:'Flash'},
                {firstname:'Peter', lastname:'Parker',secretId:'Spider-Man'}
            ]
        }
    },
    methods: {
        storiesBy(writer) {
            return this.storyes.filter(function(story) {
                return story.writer == writer;
            })
        },
        sortValue() {
            console.log(">>>>> sortValue <<<<<");

            var testVals = this.storyes.sort(function(a,b){
                return (a.upvotes - b.upvotes)*-1;
                });

            console.log(testVals);

            return testVals;
        }
    },
    computed: {
        famous() {
            return this.storyes.filter(function(item){
                return item.upvotes > 25;
            })
        },
        search() {
            console.log(">>>>> search <<<<<");
            var query = this.query;

            console.log("query:" + query);

            return this.storyes.filter(function(story){
                return story.plot.includes(query);
            })
        },
        orderedStories() {
            return this.sortValue();
        }
    }
}
</script>

<style scoped>

</style>