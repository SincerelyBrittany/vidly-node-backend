## Introduction
This is the implementation of Vidly in Node.js.

## Setup

Make sure to follow all these steps exactly as explained below. Do not miss any steps or you won't be able to run this application.

### Install MongoDB

To run this project, you need to install the latest version of MongoDB Community Edition first.

https://docs.mongodb.com/manual/installation/

Once you install MongoDB, make sure it's running.

### Install the Dependencies

Next, from the project folder, install the dependencies:

    npm i

### Populate the Database

    node seed.js

### Run the Tests

You're almost done! Run the tests to make sure everything is working:

    npm test

All tests should pass.

### Start the Server

    node index.js

This will launch the Node server on port 3900. If that port is busy, you can set a different point in config/default.json.

Open up your browser and head over to:

http://localhost:3900/api/genres

You should see the list of genres. That confirms that you have set up everything successfully.

### (Optional) Environment Variables

If you look at config/default.json, you'll see a property called jwtPrivateKey. This key is used to encrypt JSON web tokens. So, for security reasons, it should not be checked into the source control. I've set a default value here to make it easier for you to get up and running with this project. For a production scenario, you should store this key as an environment variable.

On Mac:

    export vidly_jwtPrivateKey=yourSecureKey

On Windows:

    set vidly_jwtPrivateKey=yourSecureKey
# practice-mastering-react-node-backend

notes that helped:

### Mongo DB issues
https://stackoverflow.com/questions/58034955/read-only-file-system-when-attempting-mkdir-data-db-on-mac


Catalina has a surprise change: it won't allow changes to the root directory (this was discussed in a forum thread as well):With the new macOS Catalina update, the folder /data/db becomes read-only, you cannot modify it. Follow this procedure to create a DB in another folder:

Change mongod directory :

``sudo mongod --dbpath /System/Volumes/Data/data/db``

Give it an alias to use it as mongod:

``alias mongod="sudo mongod --dbpath /System/Volumes/Data/data/db"``

Just type ``mongod`` in your terminal, it should work.

Extra => If you need to give it current user rights, use this line of code :

``sudo chown -R $(whoami) /System/Volumes/Data/data/db``

(Just for info -> ``$(whoami)`` is just a variable that returns your current user)

Found here: https://forum.codewithmosh.com/t/urgent-deprecated-handleexceptions-will-be-removed-in-winston-4-use-exceptions-handle/16062

and here:  https://stackoverflow.com/questions/58034955/read-only-file-system-when-attempting-mkdir-data-db-on-mac




Getting Application to work (debugging):

Make the following changes: In package.json

“bcrypt”: “^5.0.0”
“mongoose”: “^6.5.2”

``npm update mongoose``
 
In rentals.js:

//Fawn.init 8(mongoose);
Fawn.init(“mongodb://127.0.0.1:27017/vidly”);

Open db.js in startup folder.

Change

``mongoose.connect(db)``
to

``mongoose.connect(db, {useNewUrlParser:true, useUnifiedTopology: true})``

Run: 

``` rm -rf node_modules
npm i
node seed.js
node index.js ```

Then go to http://localhost:3900/api/genres

Used the following links: https://forum.codewithmosh.com/t/urgent-deprecated-handleexceptions-will-be-removed-in-winston-4-use-exceptions-handle/16062

https://forum.codewithmosh.com/t/heroku-mongodb-deployment-error-react-course/297/28

https://forum.codewithmosh.com/t/node-seed-js-error-in-vidly-api-node-mongoerror-unsupported-op-query-command-delete/13939/29?page=2
