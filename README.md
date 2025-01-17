# True Power is Create, Read, Update and Delete.

### Demo: Effortlessly transition between different data interfaces
```
const crud = require("./crud-true-power")(); const dbs = await crud.mongo.connect('tp-crud-testdb'); 

console.log('your files: ', crud.fs.read()) 
// ^ reads your files from the current directory on your file system

crud.fs.read().forEach((file) => {
	crud.mongo.create(dbs, "files", {"path":file}); 
  	// ^ creates item {"path":file} in your MongoDb's collection "files"
});

console.log('your files, now from MongoDb: ', 
            (await crud.mongo.read(dbs, "files"))) 
			// ^ reads your files, now from your MongoDb's collection "files"

// Yet be careful ;) ~ "With true power comes true responsibility"
console.log('your files, deleted, but fortunately just from MongoDb: ', 
            (await crud.mongo.delete(dbs, "files"))) 
			// ^ deletes all items in your MongoDb's collection "files"

// Also works for the internet on friendly receptive websites and API's
console.log((await crud.http.read("https://duckduckgo.com?q=movie-the-matrix-imdb")));
```

## crud.fs (for your file systems)
```
let result = crud.fs.create(path,fcontent=null) // creates file if 2nd parameter is not null, otherwise creates directory
let result = crud.fs.read(path) // returns a file's content or the files of a directory as a list
let result = crud.fs.update(src,dst) // moves a file or directory
let result = crud.fs.delete(path) // deletes a file or directory
```

## crud.mongo (for your MongoDB)
```
let result = await crud.mongo.connect(dbname) // returns dbs (client.db())
let result = await crud.mongo.create(dbs,collection, itemorlist, extra_options={}) // extra_options {"allow_id":1} will preserve _ids of the item or list items
let result = await crud.mongo.read(dbs, collection, criteria={}, justOne=false, extra_options={}) // when string is given criteria transforms to {_id:new ObjectId()}. extra_options
let result = await crud.mongo.update(dbs, collection, criteria={}, itemorlist, justOne=false, extra_options={}) // extra_options: {"no_date":1} will prevent updating last_updated field with latest timestamp
let result = await crud.mongo.delete(dbs, collection, criteria={}, justOne=false);
let result = await crud.mongo.connectWithClient(dbname); // returns both dbs and client {"dbs":..,"client":""} in case you need to close the connection using client.close()
```

## crud.http (for your websites)
```
let result = await crud.http.create(url,data,authValue=null); // authValue sets "Authorization" header for account specific actions
let result = await crud.http.read(url,authValue=null); // authValue sets "Authorization" header for account specific actions
let result = await crud.http.update(url,data,authValue=null); // authValue sets "Authorization" header for account specific actions
let result = await crud.http.delete(url,authValue=null); // authValue sets "Authorization" header for account specific actions
```	


### Install
Yarn and NPM packages coming soon. For now, you can install it in your project using git clone:
```
git clone https://github.com/neil-yoga/crud-true-power
cd crud-true-power && npm install # install dependencies

# Optionally
mv crud* ../ # move files to your project, so you can require crud with ./
```

### Test
```
./node_modules/jest/bin/jest.js
```

### Bonus: Write your own libraries
```
const mylibraries = {"ssh": {"read":function(){ return "todo" }}};
// ^ You can even extend crud with your own libraries like this

const mycrud = require("./crud-true-power")(mylibraries);
// ^ And importing it like this

console.log(mycrud.ssh.read()); // should output todo 
```

### Bonus: Keep things alive
```
// Enjoy the free code sharing. 
//
// ☯️ If you used my code to save time,
//  consider donating eco-friendly crypto:
```

```
nano_3boxqk5q56xsz8ufrw9srrz4pta6ffbkrg9j31aqziz8wtnr6j68ci7s4cnc
```

```
// It matters: Everything is an energy exchange ⚡.
//
//
// ^ Also feel free to copy this template for your own projects and replace the wallets.
// 🙏 You deserve to be happy and free.
```

### Nano?
<a style="color:black;font-size:15px;" href="https://nano.org">Zero Fees, Eco-Friendly, Instant Payments</a>
