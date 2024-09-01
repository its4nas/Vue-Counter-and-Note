<script setup>
import {ref} from "vue"

const showModel = ref(false)
const noteTitle = ref("")
const noteContent = ref("")
const errorMessage = ref("")
const notes = ref([])

const add_note = () => {
  if(noteTitle.value.length < 2)
{
  return errorMessage.value = "Title must be more than One letter"
}
  notes.value.push({
    id: Math.floor(Math.random() * 1000000),
    title: noteTitle.value,
    content: noteContent.value,
  });

  noteTitle.value = ""
  noteContent.value = ""
  showModel.value = false
  errorMessage.value = ""
}

</script>

<template>
    <main>
      <div class="overlay" v-if="showModel">
                <div class="model">
                    <div class="background">
                        <div class="container">
                            <div class="screen">
                            <div class="screen-header">
                                <div class="screen-header-left">
                                <div class="screen-header-button close"></div>
                                <div class="screen-header-button maximize"></div>
                                <div class="screen-header-button minimize"></div>
                                </div>
                                <div class="screen-header-right">
                                <div class="screen-header-ellipsis"></div>
                                <div class="screen-header-ellipsis"></div>
                                <div class="screen-header-ellipsis"></div>
                                </div>
                            </div>
                            <div class="screen-body">
                                <div class="screen-body-item left">
                                <div class="app-title">
                                    <div class="card">
                                      <h5 class="title" style="font-size: 20px; color: #213547;" v-if="!noteTitle">The Title will be show here</h5>
                                      <h5 class="title" style="font-size: 20px; color: #213547;" v-if="noteTitle">{{ noteTitle }}</h5>
                                        <p class="info" style="font-size: 15px; color: #213547;" v-if="!noteContent">Here will be the message that you have entered.</p>
                                        <p class="info" style="font-size: 15px; color: #213547;" v-if="noteContent">{{ noteContent }}.</p>

                                    </div>
                                </div>
                                </div>

                                <div class="screen-body-item">
                                <div class="app-form">
                                    <div class="app-form-group">
                                    <input v-model.trim="noteTitle" class="app-form-control" placeholder="Title">
                                    </div>
                                    <div class="app-form-group message">
                                    <input v-model.trim="noteContent" class="app-form-control" placeholder="Content">
                                    </div>
                                    <div class="app-form-group buttons">
                                      <p>{{ errorMessage }}</p>
                                    <button class="app-form-button" @click="showModel = false">CANCEL</button>
                                    <button class="app-form-button" @click="add_note()">SAVE</button>
                                    </div>
                                </div>
                                </div>
                            </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

        <div class="container1">
            <header>
                <h1>Note</h1>
                <button id="add-note" @click="showModel = true">+</button>
            </header>

            <div class="cards">
              <div v-for="note in notes" class="card" style="margin-right: 40px;" :key="note.id">
                <h2 class="title">{{ note.title }}</h2>
                <p class="info">{{ note.content }}</p>
	            </div>
            </div>

        </div>
    </main>
</template>

<style scoped>
main {
    margin: 0 0 0 10%;
}

.container1 {
    margin: 0 auto;
}

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
#add-note {
    background-color: #213547;
    color: white;
}
.card {
    background-color: #eeebaa;
    border-radius: 16px;
    box-shadow: 0 30px 30px -25px rgba(65, 51, 183, 0.25);
    max-width: 200px;
    min-width: 150px; /* Set a minimum width for the card */
    word-wrap: break-word;
    overflow: hidden;
    flex: 1;
    margin: 5px; 
}

.cards {
    display: flex;
    align-items: center;
    /* justify-content: space-between; */
    flex-wrap: wrap; /* Allow items to wrap to the next line */
}
.background {
  display: flex;
  min-height: 100vh;
}

.container {
  flex: 0 1 700px;
  margin-left: 10%;
  padding: 10px;
}

.screen {
  position: relative;
  background: #213547;
  border-radius: 15px;
}

.screen:after {
  content: '';
  display: block;
  position: absolute;
  top: 0;
  left: 20px;
  right: 20px;
  bottom: 0;
  border-radius: 15px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, .4);
  z-index: -1;
}

.screen-header {
  display: flex;
  align-items: center;
  padding: 10px 20px;
  background: #2e3f4e;
  border-top-left-radius: 15px;
  border-top-right-radius: 15px;
}

.screen-header-left {
  margin-right: auto;
}

.screen-header-button {
  display: inline-block;
  width: 8px;
  height: 8px;
  margin-right: 3px;
  border-radius: 8px;
  background: white;
}

.screen-header-button.close {
  background: #ed1c6f;
}

.screen-header-button.maximize {
  background: #e8e925;
}

.screen-header-button.minimize {
  background: #74c54f;
}

.screen-header-right {
  display: flex;
}

.screen-header-ellipsis {
  width: 3px;
  height: 3px;
  margin-left: 2px;
  border-radius: 8px;
  background: #999;
}

.screen-body {
  display: flex;
}

.screen-body-item {
  flex: 1;
  padding: 50px;
}


.app-form-group {
  margin-bottom: 15px;
}

.app-form-group.message {
  margin-top: 40px;
}

.app-form-group.buttons {
  margin-bottom: 0;
  text-align: right;
}

.app-form-control {
  width: 100%;
  padding: 10px 0;
  background: none;
  border: none;
  border-bottom: 1px solid #666;
  color: #ddd;
  font-size: 14px;
  text-transform: uppercase;
  outline: none;
  transition: border-color .2s;
}

.app-form-control::placeholder {
  color: #666;
}

.app-form-control:focus {
  border-bottom-color: #ddd;
}

.app-form-button {
  background: none;
  border: none;
  color: #eeebaa;
  font-size: 14px;
  cursor: pointer;
  outline: none;
}

.app-form-button:hover {
  color: #eeebaa;
}


@media screen and (max-width: 520px) {
  .screen-body {
    flex-direction: column;
  }

  .screen-body-item.left {
    margin-bottom: 30px;
  }

  .app-title {
    flex-direction: row;
  }

  .app-title span {
    margin-right: 12px;
  }

}

@media screen and (max-width: 600px) {
  .screen-body {
    padding: 40px;
  }

  .screen-body-item {
    padding: 0;
  }
}

@keyframes fallFromTop {
    0% {
        transform: translateY(-100%);
    }
    100% {
        transform: translateY(0);
    }
}

.overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 9999; /* ensure it's above other content on the page */
    animation: fallFromTop 0.5s ease forwards;
}

.model {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    padding: 20px;
}

.app-form-group p
{
  color: #ed1c6f;
  font-size: 10px;
}

</style>