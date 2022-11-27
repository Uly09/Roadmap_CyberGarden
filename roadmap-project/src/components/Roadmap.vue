<template>
    <div class="wrapper">
        <b-card v-if="!toggleBtn">
            <template #header>
                <div >Что вы хотите изучить?</div>
            </template>
            <b-form-group v-slot="{ ariaDescribedby }">
                <b-form-radio-group
                    v-model="selected"
                    :options="options"
                    :aria-describedby="ariaDescribedby"
                    name="radios-stacked"
                    plain
                    stacked
                ></b-form-radio-group>
                <b-button :pressed.sync="toggleBtn" @click="showRoadmap" class="mt-3" variant="outline-secondary">Принять</b-button>
            </b-form-group>
        </b-card>
        <div v-show="toggleBtn"><b-button block variant="secondary">{{ selected }}</b-button></div>
        <div v-show="toggleBtn" ref="roadmapBlock" class="container"></div>
    </div>
</template>

<script>
export default {
  name: 'RoadmapPage',
  data() {
      return {
        toggleBtn: false,
        selected: '',
        options: [
          { text: 'Frontend-разработка', value: 'Frontend-разработка', disabled: false },
          { text: 'Backend-разработка', value: 'Backend-разработка', disabled: true },
          { text: 'Серверная разработка', value: 'Серверная разработка', disabled: true },
          { text: 'Data-science', value: 'Data-science', disabled: true },
          { text: 'Машинное обучение', value: 'Машинное обучение', disabled: true },
          { text: 'Верстка сайтов', value: 'HTML-верстка', disabled: true }
        ],
        roadmap: [
            { caption: "JavaScript", elements: [
                {caption: "Чистый JS", elements: [
                    {caption: "Введение", elements: [
                        {caption: "История ЯП", elements: []},
                        {caption: "Что такое JS", elements: []},
                        {caption: "История версий", elements: []},
                        {caption: "Как запустить код на JS?", elements: []},
                    ]},
                    {caption: "Переменные", elements: [
                        {caption: "Объвление переменных", elements: []},
                        {caption: "Типы переменных", elements: [
                            {caption: "var", elements: []},
                            {caption: "let", elements: []},
                            {caption: "const", elements: []},
                        ]},
                        {caption: "Правила объявления переменных", elements: []},
                        {caption: "Подъём", elements: []},
                    ]},
                    {caption: "Типы данных", elements: [
                        {caption: "Переменные", elements: []},
                        {caption: "Объекты", elements: []},
                        {caption: "Преобразования типов", elements: []},
                    ]},
                ]},
                {caption: "Фреймворки", elements: []}
            ] }

        ]
      }
    },
    methods: {
        generateRoadmap(array, block) {
            block += '<div class="row row-cols-' + array.length + '">';

            array.forEach((item) => {
                block += '<div class="col"><button class="btn btn-secondary">' + item.caption + '</button>';
                if (item.elements.length > 0) block = this.generateRoadmap(item.elements, block);
                block += '</div>';
            });
            block += '</div>';

            return block;
        },
        showRoadmap() {
            let body = this.generateRoadmap(this.roadmap, '');

            this.$refs.roadmapBlock.innerHTML = "";
            this.$refs.roadmapBlock.insertAdjacentHTML('afterbegin', body);
        }
    }
}
</script>

<style scoped>
.wrapper {
    max-width: 90%;
    margin: 50px auto;
}
</style>