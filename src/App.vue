<template>
  <div>
    <h1>My Quiz Game</h1>
    <h2>Question: <span>Python is a programming language.</span></h2>
    
    <div class="options">
      <input type="radio" name="options" id="" value="True">
      <label for="">True</label>
      <input type="radio" name="options" id="" value="False">
      <label for="">False</label>
      
    </div>
    <button class="btn-submit">Submit</button>
  </div>
  
</template>

<script>


export default {
  name: 'App',

}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#app div{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 750px;
  margin: 50px auto;
}

#app div h2{
  font-size: 24px;
  margin-top: 20px;
  border: 2px solid blue;
  border-radius: 12px;
  height: 50px;
  width: 100%;
  padding: 10px 12px;
}

#app span{
  color: blue;
}

#app div .options{
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  gap: 10px;
  margin-top: 30px;
}

.btn-submit{
  padding: 10px 20px;
  background-color: blue;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
}
</style>
