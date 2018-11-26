NOTE: Below I have provided by understanding of each .js file. 

I have chosen to do this because I am unable to complete the project at this time. I believe this is still due to my lack of understanding full-stack workflow with the software and languages covered. 

I have also provided notes on the obstacles which are currently preventing me from completing this assignment.

--------------------------------------------------------------------------------------------------
OBSTACLE NOTES:

I originally tried to complete this app with my own notes but soon became lost trying to set up the proper workflow. 
Since I could not understand the concept enough to pseudocode it properly I ended up devoting my time beginning on Thursday to reconstruct the app using A. the html framework from the demo, and B. the solution example provided in GitLab.

Even so, two major issues are preventing me from testing my work.
    1. I am able to connect to the server, but when I connect to the localhost URL it immediately disconnects me from the PORT
        I have tested through stack-overflow, but none of the solutions I have come across address an issue close to mine
    2. I am not able to properly set up the app in Heroku. I have registered it on Heroku but there is a second set up process       requiring me to use a password that I don't know.

For all of this, I will be meeting with my tutor on Tuesday. Hopefully I will have it completed by the end of the week, but if I have to devote more time to the current week's homework then I will work on completing it over the winter break.


# eat-burger
You can create your own burgers, devour them and see which you've eaten and which you have left.

--------------------------------------------------------------------------------------------------

BURGER APP REVIEW: HOW DOES IT WORK

connection.js
    creates the db connection using localhost PORT 3306
        pushed into var "connection:
    uses
        a. connection var
        b. ".connect()" mysql method
    exports to -> "orm.js"

orm.js
    creates functions: 
        printQuestionMarks
            loops through a var representing a number
            pushes a "?" into an array = to the number value
        objToSql
            for each key in the object parameter, that key is equal to the object key
            pushes into an array
    defines "orm" variable object
        all
            gets all data from the table && pushes into "cb" as a parameter
        create
            inserts into the table 
            uses printQuestionMarks to define the # of values inserted
        update
            takes object values && columns to insert
            uses objToSql to "parse" each object by key && sets values by key
        SUMMARY: orm.js sets functions to SET, GET, && UPDATE the inputted data
    exports to -> "burger.js"

burger.js
    creates variable "burger"
        all
            takes orm.all
            inputs table "burgers" to get all burgers
        create
            takes orm.create(name, cb)
            inputs "burgers" as the table
            sets object's "burger_name" to the parameter "name" var
            sets object's "devoured" status to "false"
        update
            takes orm.update
            sets devoured to true
    exports to -> "burgers_controller.js"

burgers_controller.js     
    creates routes
        "/" 
            redirects to "/burgers"
        "/burgers"
            takes burger.all 
            to display table data in "index.handlebars" where html tag "burger_data" is
        "/burgers/create"
            takes burger.create(name)
            sets "name" parameter to form input holding the tag "burger_name"
            then redirects to "/" to update the page
        "/burgers/:id" 
            takes burger.update
            uses id contained w/i html handlebars tag "id"
            logs the result
            SUMMARY: updates the devoured burger's status by their id
    exports to -> "server.js"

server.js
    requires express and body parser
    sets the "PORT"
    contains mostly boilerplate code (i.e. bodyparser.urlencoded, exphbs var, default handlebars layout...)
    takes "burgers_controller.js" routes for ALL site functionality
    listens to the PORT - connects to burger database w/i the specified PORT

--------------------------------------------------------------------------------------------------

cb stands for call-back
            