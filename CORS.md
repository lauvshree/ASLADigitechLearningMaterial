## What is CORS?
  CORS stands for Cross Origin Resource Sharing. It is meant to streamline the resource sharing across multiple web applications one same or different origins. 

### CORS Explained with an example
  Take the case of an ecommerce site. After choosing the items for  purchase, the customer makes payment through one of the many options. In each of these options, the ecommerce site is doing some kind of a resource sharing with the bank or the payment gateway. The bank or the payment gateway should ensure the request is from a recognized origin and then process the payment. This validation is done through the headers sent by the ecommerce site. Let us try to simulate this process. 

### CORS Simulation
We know how to develop a web application with Express.  

Take a look at the simple web application below. It has just one resource mapping or end-point which will returns a JSON object.

```
const express = require('express');

const app = new express();
const port = 3333;

const pokemon = [{
    id : 1,
    name : 'bulbsaur'
},
{
    id : 2,
    name : 'ivysaur'
},
{
    id : 3,
    name : 'venusaur'
}]

app.get("/pokemon", (req,res) => {
    return res.send(pokemon);
});

app.listen(port, () => {
    console.log(`listening at http://localhost:${port}`)
})

```

We can test the url from postman or browser and get the expected result. Now let's create another web application which serves an end-point which will talk to the first end point we created using the `fetch` method we have already learnt about. 

```
const express = require('express');
const fetch = require('node-fetch');

const app = new express();
const port = 3334;

app.get("/myobjs", (mainreq,mainres) => {
    let responseToSend = null;
    const req = fetch("http://localhost:3333/pokemon").then(
        (res)=>{
            return res.json();
        }).then((body) =>{
            mainres.send(body);
        });
});

app.listen(port, () => {
    console.log(`listening at http://localhost:${port}`)
})

```

What is happening here is, in my new web application, I am serving an API end point which is raising a fetch request to the first application's API and returning the data returned by it. 

But when it comes to doing the same from a browser, through java scripts using AJAX requests from HTML pages, there are some operational issues we have to encounter and tackle. Let's create a HTML with a javascript which will send a fetch request to this URL and open the HTML with a live browser.

```
<html>
<script>
    fetch("http://localhost:3333/pokemon", { method: 'GET'})
    .then((res) => {
        console.log(res);
        return res.json()
    })
    .then((body) => {
        document.getElementById('pokemon').innerHTML = JSON.stringify(body); 
    }).catch((err) => {
        console.log(err);
    }) ;

</script>
This is just a dummy html to post fetch request
<div id='pokemon'>
</div>
</html>
```

You will observe that it is making a fetch request in the same manner as we did before except that it is from client side now. This is however seen as a cross origin request. If the html page is in one server  and the web application is in a different server, and a Java script in the HTML is using the web API to make a GET/POST/PUT/FETCH/etc call, a cross origin resource sharing is happening. The web API has to explicitly be told that the application will handle Cross origin resource sharing. This can be done with the help of the CORS module custom built for this purpose. Install cors with npm. 

```npm install cors```

Now all one should do is include these couple of lines, ideally right after the application is created, to make the server CORS enabled.

```
const cors_app = require('cors');
app.use(cors_app());
```

The main idea for CORS is to be able to pass header information from one origin to another, to ensure secuirty. Let's change our main API to authenticate only if the API key passed in the header is valid. 

```
const express = require('express');
const app = new express();
const cors_app = require('cors');
app.use(cors_app());
const port = 3333;

const pokemon = [   {id : 1,name : 'bulbsaur'},
                    {id : 2,name : 'ivysaur'},
                    {id : 3,name : 'venusaur'}];

const validAPIKeys = ['key1','key2','key3'];

app.get("/pokemon", (req,res) => {
    const apikey = req.get("APIKey");
    console.log(apikey);
    if(validAPIKeys.includes(apikey)) {
        return res.send(pokemon);
    } else {
        return res.send({err:'Invalid user'});
    }
});

app.listen(port, () => {
    console.log(`listening at http://localhost:${port}`)
})

```
If there is a valid header named *APIKey* with values *key1 or key2 or key3*, the request will be processed and the names of the pokemon will be fetched. If not, it will return an error message. 

Try this from postman, passing the APIKey in the header. Also make the following changes to your HTML and see if this works.

```
<script>
    headers = {'APIKey':'key1'}
    fetch("http://localhost:3333/pokemon", { method: 'GET',headers:headers})
    .then((res) => {
        console.log(res);
        return res.json()
    })
    .then((body) => {
        document.getElementById('pokemon').innerHTML = JSON.stringify(body); 
    }).catch((err) => {
        console.log(err);
    }) ;

</script>
```

In an ideal situation, the APIKey is generated and given by the host who is providing the API access. There is most times a unique key, which associated with your user credentials to help track the origin of the request. 

The default configuration of CORS application is

```
{
  "origin": "*",
  "methods": "GET,HEAD,PUT,PATCH,POST,DELETE",
  "preflightContinue": false,
  "optionsSuccessStatus": 204
}
```

This means, it allows all origins, all methods, does not pass the output of a preflight check to the next request, a status code to use for successful OPTIONS requests (some legacy browsers choke on 204). We can change these options to make the API selectively restrictive. You can read more about CORS [here](https://expressjs.com/en/resources/middleware/cors.html).
