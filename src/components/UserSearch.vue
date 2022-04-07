<template>
  <div class="container">
    <div class="input-line">
      <input type="text" v-model="inputValue" placeholder="Search Github username" @keyup.enter="search">
      <button @click="search">Search</button>
    </div>
    <div class="card">
      <div class="user-data" v-if="result">
        <div class="image">
          <img :src="result.avatar_url" alt="Avatar">
        </div>
        <div class="data">
          <h1>
            {{result.name}}
          </h1>
          <a :href="result.html_url" target="_blank">
            @{{result.login}}
          </a>
        </div>
      </div>
      <div class="bio" v-if="result">
        <p v-if="result.bio != null">
          {{result.bio}}
        </p>
        <p v-else-if="result.bio == null">
          This profile has no bio
        </p>
      </div>
      <div class="row" v-if="result">
        <div class="row-item">
          <div class="col">
            <h3>Repos</h3>
            <p>
              {{result.public_repos}}
            </p>
          </div>
        </div>
        <div class="row-item">
          <div class="col">
            <h3>Followers</h3>
            <p>
              {{result.followers}}
            </p>
          </div>
        </div>
        <div class="row-item">
          <div class="co">
            <h3>Following</h3>
            <p>
              {{result.following}}
            </p>
          </div>
        </div>
      </div>
      <div class="wrap" v-if="result">
        <div class="row-item">
          <div class="inline">
            <img src="@/assets/img/icon-location.svg" alt="Icon">
            <p v-if="result.location != null">
              {{result.location}}
            </p>
            <p v-else-if="result.location == null">
              Not available
            </p>
          </div>
        </div>
        <div class="row-item">
          <div class="inline">
            <img src="@/assets/img/icon-website.svg" alt="Icon">
            <p v-if="result.blog != ''">
              <a :href="result.blog" target="_blank">
                {{result.blog}}
              </a>
            </p>
            <p v-else-if="result.blog == ''">
              Not available
            </p>
          </div>
        </div>
        <div class="row-item">
          <div class="inline">
            <img src="@/assets/img/icon-twitter.svg" alt="Icon">
            <p v-if="result.twitter_username != null">
              {{result.twitter_username}}
            </p>
            <p v-else-if="result.twitter_username == null">
              Not available
            </p>
          </div>
        </div>
        <div class="row-item">
          <div class="inline">
            <img src="@/assets/img/icon-company.svg" alt="Icon">
            <p v-if="result.company != null">
              {{result.company}}
            </p>
            <p v-else-if="result.company == null">
              Not available
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      inputValue: '',
      result: [],
    }
  },
  mounted(){
    this.fetchData()
  },
  methods:{
    fetchData(){
      fetch(`https://api.github.com/users/ArturHarutyunyan1`)
      .then((res) => res.json())
      .then((data) => {this.result = data})
    },
    search(){
      if(this.inputValue != ''){
        fetch(`https://api.github.com/users/${this.inputValue}`)
        .then((res) => res.json())
        .then((data) => {this.result = data})
      }else{
        alert("You must fill in the input field")
      }
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Condensed&display=swap');
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

:root{
    --main-bg: #141d2f;
    --card-bg: #1e2a47;
    --search-button: #0079ff;
    --text-color: #ffffff;
    --link-color: #0b5ab7;
}

body{
    width: 100%;
    min-height: 100vh;
    max-height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    font-family: 'Roboto Condensed', sans-serif;
    background: var(--main-bg);
}

.container{
    width: 700px;
    height: 500px;
}

.input-line{
    width: 100%;
    height: 70px;
    background: var(--card-bg);
    border-radius: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
}

input{
    width: 80%;
    height: 100%;
    background: transparent;
    outline: none;
    border: none;
    padding-left: 15px;
    font-size: 20px;
    color: var(--text-color);
}

button{
    width: 15%;
    height: 60%;
    background: var(--search-button);
    color: var(--text-color);
    border: none;
    outline: none;
    border-radius: 5px;
    cursor: pointer;
}

::placeholder{
    color: var(--text-color);
}

.card{
    width: 100%;
    min-height: 400px;
    max-height: auto;
    margin-top: 15px;
    border-radius: 5px;
    background: var(--card-bg);
}

.user-data{
    width: 60%;
    height: 100px;
    padding-top: 15px;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
}

.image{
    width: 100px;
    height: 100px;
    border-radius: 50%;
}

.image img{
    width: 100%;
    height: 100%;
    border-radius: 50%;
    object-fit: cover;
}

.bio{
    width: 90%;
    height: auto;
    margin: 35px auto;
}

.row{
    width: 90%;
    height: 100px;
    margin: 15px auto;
    border-radius: 5px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    text-align: center;
    background: var(--main-bg);
}

.row-item{
    width: 50%;
}

.row-item h3{
    font-size: 18px;
    color: var(--text-color);
}

.row-item p{
    font-size: 25px;
    color: var(--text-color);
}


.wrap{
    width: 50%;
    margin: auto;
    padding-top: 1rem;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    flex-wrap: wrap;
}

.wrap .row-item{
    width: 39%;
    height: 50px;
}

.inline{
    display: flex;
    align-items: center;
}

.inline p{
    margin-left: 15px;
    font-size: 14px;
}

h1, p{
    color: var(--text-color);
    margin-top: 5px;
}

a{
    color: var(--link-color);
    text-decoration: none;
}


@media (max-width: 768px){
    .container{
        width: 100%;
        height: auto;
    }
    .user-data{
        width: 100%;
        margin: auto;
        flex-direction: column;
        height: auto;
        text-align: center;
    }
    .bio{
        text-align: center;
    }
    .inline a{
        font-size: 12px;
    }
    .input-line{
        width: 100%;
    }
    .wrap{
        width: 100%;
        flex-direction: column;
    }
}

</style>