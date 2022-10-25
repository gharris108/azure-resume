# azure-resume
Azure Project - Resume fully hosted by Azure, following [ACG tutorial.](https://www.youtube.com/watch?v=ieYrBWmkfno) 


## First steps
 - Frontend folder contains the website.
 - main.js contains logic for visitor counter on website.

 ```js
const getVisitCount = () => {
    let count = 10;
    fetch(functionApi).then(response => {
        return response.json()
    }).then(response => {
        console.log("Website called function API.");
        count = response.count;
        document.getElementById("counter").innerText = count;
    }).catch(function(error){
        console.log(error);
    });
    return count;
}
 ```