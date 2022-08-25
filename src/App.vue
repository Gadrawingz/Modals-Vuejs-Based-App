<!-- @gadrawingz & @donnekt -->
<template>
  <div class="boxx">
    <h1>{{ pageTitle }} </h1>
    <div class="inner">
      <p>{{ pageSubTitle }}</p>
    </div>
    <!-- (1) Here we're passing our modal data using props -->
    <div v-if="showMainModal">
      <Modal :header="header" :content="content" theme="sale" @close="toggleMainModal"/>
    </div>

    <!-- 
      (2) =>
      But sometimes we want to pass complex information 
      in terms of content into a component
      Slot is really useful and focus on passing custom template into reusable component;
      But props is good for passing data like string, boolean or an array: 
    -->
    <teleport to='#modals' v-if="showSecondModal">
    <!-- 
      Lets teleport 2 render for example: this Modal to another div 
      Ex: Lets render it to #modal insted of #app div in our index.html
    -->
      <ComplexModal theme="dark" @close="toggleSecondModal">
        <template v-slot:links> 
          <!-- We need to give a name this slot -->
          <a href="#">1st Link</a>
          <a href="#">2nd Link</a>
        </template>
        <!-- Default content: If below data doesn't exist It will show this -->
        <h1>Complex modal</h1>
        <p>This is a complex modal where we use slots instead of props to pass template into component</p>
      </ComplexModal>
    </teleport>


    <!--
      [3] REUSING OUR COMPONENT AGAIN
      U dont actually have to do anything else inside the ComplexModel file (modal)
      Because its reusable (We can use it in many different places )
      We only change:1) What we pass in, (2)What props we give it, &(3) How we open it
    -->
    <div v-if="showThirdModal">
      <!-- Lets use default theme -->
      <ComplexModal @close="toggleThirdModal">
        <template v-slot:links> 
          <a class="back-link" href="#">Return Back</a>
        </template>
        <h1>Simple Login Form</h1>
        <div>
          <form method="POST">
            <label for="username">Username</label>
            <div class="row">
              <input type="text" name="username">
            </div>
            <label for="password">Password</label>
            <div class="row">
              <input type="password" name="password">
            </div>
            <div class="row">
              <button type="submit">Submit</button>
            </div>
          </form>
        </div>
      </ComplexModal>
    </div>

    <!-- Buttons to control the openings -->
    <div class="buttons">
      <button @click.shift="toggleMainModal">Click+Shift Key to open</button>
      <button @click.ctrl="toggleSecondModal">Click+Ctrl Key to open</button>
      <button @dblclick="toggleThirdModal">[Double Click] to open</button>
    </div>
  </div>
</template>

<script>
import Modal from './components/Modal.vue'
import ComplexModal from './components/ComplexModal.vue'

export default {
  name: 'App',
  components: {
    Modal, ComplexModal,
  },

  data() {
    return {
      pageTitle: "Modal Container",
      pageSubTitle: "Welcome to this project dealing with modals and how to handle them using  vue.js 3.x latest tricks and features such as slots, teleport,etc. Click to one of below buttons as its label says and see the reacton!",
      header: "Main Modal",
      content: "This 1st modal is made by using 1st way, where you have to click and press Shift key to make any reaction",
      
      showMainModal : false,
      showSecondModal : false,
      showThirdModal : false,
    }
  },

  methods: {
    toggleMainModal() {
      this.showMainModal = !this.showMainModal
    },
    toggleSecondModal() {
      this.showSecondModal = !this.showSecondModal
    },
    toggleThirdModal() {
      this.showThirdModal = !this.showThirdModal
    }
  }
}
</script>

<style>
#app, #modals {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.boxx {
  border: 1px solid #000000;
  margin: 20px;
  max-width: 95%;
  border-radius: 8px;
  height: auto;
  padding: 20px;
  background: #f8f9f9;
}

.boxx h1, p {
  text-align: center;
  padding: 10px;
}

.boxx p {
  text-align: center;
  border-bottom: 4px solid #eaf2f8;
  margin-top: 15px;
  margin-bottom: 15px;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-size: 20px;
}

.inner {
  display: flex;
  justify-content: center;
  border-bottom: 4px solid #6c3483;
}

.inner p {
  background: #e8f8f5;
  max-width: 450px;
  border-bottom: none;
  border-left: 2px solid #cb4335;
  display: flex;
  justify-content: center;
  text-align: left;
}

.buttons {
  margin-top: 15px;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}

.buttons button {
  border-radius: 5px;
  font-size: 18px;
  padding: 8px;
  margin: 10px;
  max-width: 200px;
  background: #7d3c98;
  color: white;
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  border: none;
}

/* Form styles */
form label {
  font-weight: bold;
  font-size: 20px;
}

form .row input {
  border: 1px solid #000;
}

form .row button {
  background: green;
  color: white;
  border: none;
}

form .row input,
form .row button {
  border-radius: 4px;
  padding: 8px;
  margin: 5px;
  outline: none;
  font-size: 19px;
}

.back-link {
  color: blue!important;
  text-decoration: none;
  border: none!important;
  font-size: 19px;
}

.back-link:hover {
  color: lightskyblue;
  text-decoration: underline;
}

</style>
