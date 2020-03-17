# Basic-AJAX

// definim domeniul (url-ul serverului) intr-o variabila pentru ca il vom refolosi
```
var url = "https://jsonplaceholder.typicode.com";
```        
// vom folosy fetch pentru a face un request de tip GET, pentru a obtine detaliile unei postari
// acel 1 reprezinta id-ul postarii a carei detalii vrem sa le luam
```
fetch(url + "/posts/1", {
  method: "GET"
}).then(function(response){
  // variabila response contine raspunsul de la server intr-o forma predefinita de catre Fetch API
  // dar pentru ca noi avem nevoie doar de raspunsul intr-o forma simplificata
  // vom apela metoda json() de pe acest obiect response, pentru al converti in forma dorita
  return response.json();
}).then(function(jsonResp){
   // odara convertit, vom avea in variabila jsonResp, obiectul de mai jos:
   console.log(jsonResp);
//     /*
//     {
//     "userId": 1,
//     "id": 1,
//     "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
//     "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
//     }
//     */
        // pentru a afisa in pagina titlul si respectiv continutul postarii
        // avem nevoie sa cream cele doua elemente HTML, pe care deocamdata le stocam in 
        // doua variabile headerTitle si respectiv paragraph
//     var headerTitle = document.createElement("h1");
//     var paragraph = document.createElement("p");

        // pe header title am folosit innerText, deoarece am presupus ca textul nu poate contine 
        // elemente HTML si ca este un simplu text
//     headerTitle.innerText = jsonResp.title;
        // pentru paragraf am folosit innerHTML, deoarece am presupus ca in continut putem avea elemente
        // html si vom vrea sa fie afisate frumos in pagina
//     paragraph.innerHTML = jsonResp.body;
        // pentru a pune elementele in pagina, trebuie mai intai sa "selectam" elementul body
//     var theBody = document.querySelector("body");
        // iar apoi sa punem in el cele doua elemente headerTitle si respectiv paragraph
//     theBody.appendChild(headerTitle);
//     theBody.appendChild(paragraph);

// });


// daca facem o cerere la server sa ne dea toata lista de postari pe care le are
// facem o cerere de tip GET la acelasi url, dar path-ul nu o sa mai contina nici un id (asa este specificat in documentatia API-ului)
// fetch(url + "/posts", {
//     method: "GET"
// }).then(function(r){
        // variabila r contine raspunsul de la server intr-o forma predefinita de catre Fetch API
        // dar pentru ca noi avem nevoie doar de raspunsul intr-o forma simplificata
        // vom apela metoda json() de pe acest obiect r, pentru al converti in forma dorita
//     return r.json();
// }).then(function(jsonResp){
//     console.log(jsonResp);

        // vom incepe cu "selectarea" elementului body, inainte de a parcurge lista de postari
        // pentru a evita ca pentru fiecare postare sa facem aceeasi "interogare" a DOM-ului
        // pentru a "selecta" acelasi element: body-ul, de fiecare data
//     var theBody = document.querySelector("body");
        // parcurgem lista de postari
//     for(var i = 0; i < jsonResp.length; i++ ) {
            // repetam operatiile de mai sus, pentru fiecarep postare in parte, pt fiecare jsonResp[i]
//         var headerTitle = document.createElement("h1");
//         var paragraph = document.createElement("p");

//         headerTitle.innerText = jsonResp[i].title;
//         paragraph.innerHTML = jsonResp[i].body;

//         theBody.appendChild(headerTitle);
//         theBody.appendChild(paragraph);
//     }
// });

    // incercam crearea unei postari, adica un request de tip POST
    // pentru o cerere de tip POST, ar trebui sa trimitem ceva pe body-ul cererii (a nu se confunda cu body-ul din HTML)
    // iar documentaria ne spune ca pe body trebui sa trimitem: title, body (continutul postarii) si un userId
// fetch(url + "/posts", {
//     method: "POST",
//     body: '{"title":"o noua postare"."body":"continutul postarii mele","userId:5"}'
// }).then(function(response){
//     console.log("the raw response ", response);
//     return response.json();
// }).then(function(jsonResponse){
//     console.log("converted response ", jsonResponse);
// });

// mai sus am construit noi "de mana" string-ul in format JSON si l-am pus direct pe body
// dar in JS, de cele mai multe ori o sa avem un obiect construit intr-o variabila JS
var myPost = {
    title: "o noua postare",
    body: "continutul postarii mele",
    userId: 5
};
// ca sa trimitem acest obiect pe body, o sa trebuiasca sa il serializam
// adica sa il convertim in string
// putem face asta folosind metoda stringify de pe obiectul JSON in javascript
// fetch(url + "/posts", {
//     method: "POST",
//     body: JSON.stringify(myPost)
// }).then(function(response){
//     console.log("the raw response ", response);
//     return response.json();
// }).then(function(jsonResponse){
//     console.log("converted response ", jsonResponse);
        // odata ce am creat o postare noua, API-ul ne returneaza pe jsonResponse doar id-ul noii postari create
        // deci pentru a avea tot continutul postarii noastre, asa cum a fost el stocat pe server
        // vom face un request, similar cu cel de mai sus, un GET, dar de data acesta cu id-ul postarii ce tocmai am creat-o
        // deci la URL vom concatena acest id

        // !!!!!!! folosind acest fake API, request-ul de mai jos o sa returneze 404, pentru ca in realitate 
        // el nu creaza elementul ce zice mai sus ca e creat !!!!!!!

//     fetch(url + "/posts/" + jsonResponse.id , {
//         method: "GET"
//     }).then(function(response){
//         return response.json();
//     }).then(function(jsonResp){

//         console.log("the post we just created ", jsonResp);
//     });

// });

// pentru a face un update la o postare, vom face un request de tip PUT
// dar inainte de a face request-ul, trebuie sa ne cream obiectul cu informatiile ce vrem sa le actualizam
// documentatia API-ului ne spune ca pentru update, vom trimite un JSON cu cheile: id (id-ul postarii ce vrem sa o actualizam),
// title (noul titlu), body (noul continut al postarii), userId (daca vrem sa schimbam si userul ce a creat postarea)
var updatePost = {
    id: 1,
    title: 'foo',
    body: 'bar',
    userId: 3
};

// continutul original al postarii ce vrem sa o actualizam cu datele din obiectul updatePost
//     {
//     "userId": 1,
//     "id": 1,
//     "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
//     "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
//     }

console.log("ceva cod executat INAINTE de requestul la server pt a updata postarea");
    // documentatia ne indica URL-ul si path-ul spre care facem request-ul
    // acest path trebuie sa contina si id-ul postarii ce vrem sa o actualizam
    // si vom face un request de tip PUT care are in body, obiectul nostru serializat (convertit in string JSON)
fetch(url + "/posts/1", {
    method: "PUT",
    body: JSON.stringify(updatePost)
}).then(function(response){
    return response.json();
}).then(function(jsonResp){
    // dupa executarea request-ului, vom aveam in jsonResp, id-ul postarii pe care tocmai am actualizat-o
    console.log("the post we just updated ", jsonResp);
});

console.log("ceva cod executat DUPA ce s-a lansat requestul la server pt a updata postarea");


```
// FUNCTII DE CALLBACK 
function doSomething(a, callback){
    var x = 2;
    x = x + a;
    console.log("the x ", x);
    callback(x);
}

doSomething(3, function(c){
    console.log("the callback response " + "success " + c);

    return "success " + c;
});
```
