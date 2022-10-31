<template>
  <div id="app">
    <h1>Products</h1>

    <div class="products">

      <!-- search -->
      <InputAction 
        @action="filterResults" 
        :active="true"
        :placeholder="'Find a Product'">
        Search
      </InputAction>

      <!-- product - no action for this / not required -->
      <InputAction 
        :active="false"
        :placeholder="'Add a Product'">
        Add Product
      </InputAction>
      
      <!-- products - bit of a exageration of slot usage, but this is what was wanted -->
      <ItemList v-for="(item, index) in paginatedResults" :key="index">
        <Product>
          <ImageHolder :image="item.image" :title="item.name" />
          <Status :status="item.status" />
          <InformationBlock class="fill-width">{{ item.name }}</InformationBlock>
          <!-- for a sake of quick reusability, it is a bit messy though -->
          <InformationBlock>{{ item.date ? formattedDate(item.date) : '' }}</InformationBlock>
          <!-- no real functionality -->
          <Toggle />
        </Product>
      </ItemList>

    </div>

    <!-- pagination control -->
    <div>
      <Pagination :total="totalPages">
        <!--ok, I used slots to not emit stuff.. bit lazy I know, time restrain -->
        <select name="pageNumber" id="pageselector" v-model="currentPage">
          <option v-for="(item, index) in totalPages" :key="index" :value="index+1">{{ index+1 }}</option>
        </select>
      </Pagination>
      <div>
      </div>

      <!-- component for sorting-->
      <!-- not implemented in timeframe, but easy to do.. -->
      <div>
        Sort by Name
      </div>
      <!--component for items per page, also did not get it in 1h time.. can be component.. -->
      <div>
        Number of Items:
        <select name="numberPerPage" id="selector" v-model="perPage">
          <option value="3">3</option>
          <option value="5">5</option>
          <option value="10">10</option>
        </select>
      </div>
    </div>
  
  </div>
</template>

<script>
import InputAction from './components/InputAction.vue'
import ItemList from './components/ItemList.vue'
import Product from './components/Product.vue'
import ImageHolder from './components/ImageHolder.vue'
import Status from './components/Status.vue'
import InformationBlock from './components/InformationBlock.vue'
import Toggle from './components/Toggle.vue'
import Pagination from './components/Pagination.vue'

export default {
  name: 'App',
  data() {
    return {
      currentPage: 1,
      perPage: 10,
      filter: '',
      userData: [
        {
          name: 'Americano',
          image: 'https://picsum.photos/48',
          status: 'green',
          date: null,
        },
        {
          name: 'Espresso',
          image: 'https://picsum.photos/48',
          status: 'yellow',
          date: null,
        },
        {
          name: 'Mocha',
          image: '',
          status: 'green',
          date: null,
        },
        {
          name: 'White Mocha',
          image: '',
          status: 'yellow',
          date: 704305433,
        },
        {
          name: 'Latte',
          image: 'https://picsum.photos/48',
          status: 'green',
          date: 1666715033,
        },
        {
          name: 'Cappucino',
          image: 'https://picsum.photos/48',
          status: 'green',
          date: null,
        },
        {
          name: 'Walking with Giants',
          image: 'https://picsum.photos/48',
          status: 'green',
          date: null,
        },
        {
          name: 'Turbinator 2',
          image: 'https://picsum.photos/48',
          status: 'red',
          date: null,
        },
        {
          name: 'Super Cali Fragilistic Expialidocious',
          image: '',
          status: 'red',
          date: 704305433,
        },
        {
          name: 'Baseball Hat',
          image: 'https://picsum.photos/48',
          status: 'green',
          date: null,
        },
      {
          name: 'Americano',
          image: 'https://picsum.photos/48',
          status: 'green',
          date: null,
        },
        {
          name: 'Espresso',
          image: 'https://picsum.photos/48',
          status: 'yellow',
          date: null,
        },
        {
          name: 'Mocha',
          image: '',
          status: 'green',
          date: null,
        },
        {
          name: 'White Mocha',
          image: '',
          status: 'yellow',
          date: 704305433,
        },
        {
          name: 'Latte',
          image: 'https://picsum.photos/48',
          status: 'green',
          date: 1666715033,
        },
        {
          name: 'Cappucino',
          image: 'https://picsum.photos/48',
          status: 'green',
          date: null,
        },
        {
          name: 'Walking with Giants',
          image: 'https://picsum.photos/48',
          status: 'green',
          date: null,
        },
        {
          name: 'Turbinator 2',
          image: 'https://picsum.photos/48',
          status: 'red',
          date: null,
        },
        {
          name: 'Super Cali Fragilistic Expialidocious',
          image: '',
          status: 'red',
          date: 704305433,
        },
        {
          name: 'Baseball Hat',
          image: 'https://picsum.photos/48',
          status: 'green',
          date: null,
        },

      ]
    }
  },
  components: {
    InputAction,
    ItemList,
    Product,
    ImageHolder,
    Status,
    InformationBlock,
    Toggle,
    Pagination
  },
  computed: {
    filteredResults() {
      // first Filter.. apply filter
      // then also show addecuate page
      if (this.filter !== '') {
        return this.userData.filter(item => {
          let name = item.name.toLowerCase()
          return name.includes(this.filter);
        });
      }
      else {
        return this.userData
      }
    },
    paginatedResults() {
      // todo: before return we can also format the sorting of this array.. to sort by property or whatever
      return this.filteredResults.slice((this.currentPage - 1) * this.perPage, (this.currentPage * this.perPage))
    },
    totalPages() {
      let number = (this.filteredResults.length / this.perPage).toFixed(0)
      return (number == 0) ? parseInt(1) : parseInt(number)
    }
  },
  methods: {
    // I used a basic function for date formatting, so no need to import a lib
    formattedDate(time) {
      const today = new Date(time);
      // a bit ugly implementation, but the quickest not to bother with -100/+100 if years are our of 1900-2000 range
      const yyyy = today.getFullYear().toString().substring(2,4)
      let mm = today.getMonth() + 1
      let dd = today.getDate()

      if (dd < 10) dd = '0' + dd;
      if (mm < 10) mm = '0' + mm;

      const formattedToday = mm + '/' + dd + '/' + yyyy;

      return formattedToday
    },
    filterResults(val) {
      this.currentPage = 1
      this.filter = val.toLowerCase()
    },
  }
}
</script>

<style>
body {
  background: #ECECEC;
}

::placeholder {
  color: #ccc;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: auto;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  width: calc(100vw - 32px);
  max-width: 600px;
}

.products {
  padding: 8px;
  border-radius: 4px;
  background: white;
  max-height: calc(100vh - 262px);
  overflow: hidden;
}

.fixed-size {
  width: 24px;
  height: 24px;
}

.fill-width {
  width: calc(100% - 120px);
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
</style>
