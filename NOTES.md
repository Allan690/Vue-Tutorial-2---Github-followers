#### What was wrong
When fetching data from the REST API we were doing it like this:
```vuejs
 const results = await axios({
                    method: 'get',
                    url: `https://api.github.com/users/${this.userName}/followers`,
                    Authorization: `token ${process.env.GITHUB_TOKEN}`
                });
                const { data } = results;
```
You notice that we missed to update the followers array that is in the data property. This is where we missed it. After fetching is complete, the follower array must always be updated because in the `v-for` of our template we are reading from it i.e 

```vue
 <div class="card" v-for="follower in followersArray" v-bind:key="follower.id">
            <img :src="follower.avatar_url" alt="Avatar" style="width:100%">
            <div class="container">
                <h4><b>{{ follower.login}}</b></h4>
                <p>{{follower.html_url }}</p>
            </div>
        </div>
``` 

What was happening was that the card could not render because the follower array was always empty, and that because when fetching data we were not updating it. So I fixed it by simply updating it as follows:
```vuejs
 const results = await axios({
                    method: 'get',
                    url: `https://api.github.com/users/${this.userName}/followers`,
                    Authorization: `token ${process.env.GITHUB_TOKEN}`
                });
                const { data } = results;

                 // update followers array
                this.followersArray = data;
```

#### Concepts covered in lesson & Notes
1. Consuming REST APIs with axios in Vue.
- We learned about using axios, a promise-based http library for making http requests to a third party API
- We learned about the fundamental difference between how REST and GraphQL APIs return data
- We went through the fundamentals of a REST API covering:
   1. Token based authentication - due to the stateless nature of http, the server looks for authentication information within each http request. So the client sends auth credentials with the request.
   2. HTTP Verbs - i.e GET, POST, PUT, PATCH, DELETE - GET retrieves data from a store, while PUT updates the store with new data, PATCH performs a partial update and DELETE deletes data from the store.
- We covered(partially), the concept of Javascript promises and using async-await as a wrapper around promises. We also covered the asynchronous nature of javascript.   
    

