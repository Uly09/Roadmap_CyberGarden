<template>
    <div>
        <b-card>
            <template #header>
                <div v-if="!toggleBtn">Что вы хотите изучить?</div>
                <div v-else>{{ selected }}</div>
            </template>
            <b-form-group v-if="!toggleBtn" v-slot="{ ariaDescribedby }">
                <b-form-radio-group
                    v-model="selected"
                    :options="options"
                    :aria-describedby="ariaDescribedby"
                    name="radios-stacked"
                    plain
                    stacked
                ></b-form-radio-group>
                <b-button :pressed.sync="toggleBtn" variant="outline-secondary">Принять</b-button>
            </b-form-group>
        </b-card>
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
          { text: 'Frontend-разработка', value: 'Frontend-разработка' },
          { text: 'Backend-разработка', value: 'Backend-разработка' },
          { text: 'Серверная разработка', value: 'Серверная разработка' },
          { text: 'Data-science', value: 'Data-science' },
          { text: 'Машинное обучение', value: 'Машинное обучение' },
          { text: 'Верстка сайтов', value: 'HTML-верстка' }
        ]
      }
    }
}
</script>