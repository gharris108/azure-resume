# azure-resume
Azure Project - Resume fully hosted by Azure, following [ACG tutorial.](https://www.youtube.com/watch?v=ieYrBWmkfno) 

govindaharris.com

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

## Backend work
 - Created resume counter in C#, connecting it to Azure functions and Azure DB to dynamically update and store the total number of visitors to the site.

 ```c#
[FunctionName("GetResumeCounter")]
        public static HttpResponseMessage Run(
            [HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)] HttpRequest req,
            [CosmosDB(databaseName:"AzureResume", collectionName: "Counter", ConnectionStringSetting = "AzureResumeConnectionString", Id = "1", PartitionKey = "1")] Counter counter,
            [CosmosDB(databaseName:"AzureResume", collectionName: "Counter", ConnectionStringSetting = "AzureResumeConnectionString", Id = "1", PartitionKey = "1")] out Counter updatedCounter,
            ILogger log)
        {
            log.LogInformation("C# HTTP trigger function processed a request.");

            updatedCounter = counter;
            updatedCounter.Count += 1;
            var jsonToReturn = JsonConvert.SerializeObject(counter);

            return new HttpResponseMessage(System.Net.HttpStatusCode.OK)
            {
                Content = new StringContent(jsonToReturn, Encoding.UTF8, "application/json")
            };

        }
 ```

## Putting it all togther
 - Connected frontend to backend through API.
 - Uploaded static site to Azure Blob Storage.
 - Pushed site live through Azure Static Sites, connected to Google Domains DNS.

![](frontend\images\website.png)
