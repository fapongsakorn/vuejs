<template>
  <v-container>
    <v-row>
      <v-col cols="6" class="text-center">
        <v-card>
          <v-col>
            <v-container>
              <v-form @submit.prevent="submitSearch">
                <h2 class="text-start">Search</h2>
                <v-text-field v-model="searchInput" label="Enter search query"></v-text-field>
                <v-select v-model="group" :items="groups" label="Group"></v-select>
                <v-textarea v-model="keywordJson" label="Enter Keyword JSON"></v-textarea>
                <v-btn type="submit" color="primary">Search</v-btn>
              </v-form>
            </v-container>
          </v-col>
        </v-card>
      </v-col>
      <v-col cols="6" class="text-center">
        <v-card>
          <v-col>
            <v-container>
              <h2 class="text-start mb-3">Result</h2>
                <p class="text-start" style="font-size: 12px;">ค้นหา:{{ input }}</p>
                <p class="text-start" style="font-size: 12px;">จำนวนที่พบ: {{ count }}</p>
                <p class="text-start" style="font-size: 12px;">อาการ: {{ symptom }}</p>
                <p class="text-start" style="font-size: 12px;">โรค: {{ disease }}</p>
              <v-list>
                <v-list-item v-for="(result, index) in searchResults" :key="index" class="text-center">
                  <v-btn color="orange" width="100%"><b>{{ result.category }}</b> - {{ result.keyword }}</v-btn>
                </v-list-item>
              </v-list>
            </v-container>
          </v-col>
        </v-card>
      </v-col>  
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      searchInput: '',
      group: '',
      groups: ['', 'โรค', 'อาการ'], 
      keywordJson: '',
      searchResults: [],
      input: '',
      count: '',
      disease: '',
      symptom: '',
    };
  },
  methods: {
    async submitSearch() {
      try {
        const requestBody = {
          search: this.searchInput,
          group: this.group,
          keyword: JSON.parse(this.keywordJson),
        };

        const response = await fetch('http://localhost:3000/api/searchkeyword', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify(requestBody),
        });

        if (!response.ok) {
          throw new Error('Network response was not ok');
        }

        const data = await response.json();
        this.searchResults = data.results || [];
        this.input = data.input || '';
        this.count = data.count || 0;
        this.symptom = data.categorycount?.อาการ || 0;
        this.disease = data.categorycount?.โรค || 0;

      } catch (error) {
        console.error('Error searching:', error);
      }
    },
  },
};
</script>
