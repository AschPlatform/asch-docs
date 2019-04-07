# Dapp Development Tutorial 3: Asch Dapp Mini DAO
This tutorial shows how to create a new type transaction or smart contract, and demonstrates a mini dao project with project management and voting function. The complete source of the Dapp can be downloaded at [Asch Mini DAO](https://github.com/bassjobsen/asch-mini-dao).

With this Dapp one can add projects (title and description) and gain votes for it.

## Setup your environment

### Install ASCH

```
# clone asch
git clone https://github.com/aschplatform/asch.git asch && cd asch && npm install && cd ..
```

### Setup your file structure
Your file and directory structure should look like that shown beneath:

```
├── config.json
├── contract
├── dapp.json
├── genesis.json
├── init.js
├── interface
├── model
└── public
    └── index.html
```

You can also install the [Basic Asch Dapp](https://github.com/bassjobsen/asch-test-dapp).

```
> git clone https://github.com/bassjobsen/asch-test-dapp.git asch-mini-dao
```

### Install Asch redeploy

```
npm install --global asch-redeploy
```

More information about Asch redeploy can be found at: [Asch redeploy](https://github.com/AschPlatform/asch-redeploy)

## Run the Dapp on the localnet
After setting your environment you can navigate to the Dapp directory and run Asch redeploy.

```
> cd asch-mini-dao
> asch-redeploy 
```

The above commands will give you the output like that shown beneath:

```
...
[2018-07-21 21:50:241][INFO] starting to register Dapp...
[2018-07-21 21:50:268][INFO] dapp: {
  "name": "test-BOPTsZpkzdvw",
  "link": "https://test-RLLEzdTFyAEG.zip",
  "category": 1,
  "description": "A hello world demo for asch dapp",
  "tags": "asch,dapp,demo",
  "icon": "http://o7dyh3w0x.bkt.clouddn.com/hello.png",
  "type": 0,
  "delegates": [
    "db18d5799944030f76b6ce0879b1ca4b0c2c1cee51f53ce9b43f78259950c2fd",
    "590e28d2964b0aa4d7c7b98faee4676d467606c6761f7f41f99c52bb4813b5e4",
    "bfe511158d674c3a1e21111223a49770bee93611d998e88a5d2ea3145de2b68b",
    "7bbf62931cf3c596591a580212631aff51d6bc0577c54769953caadb23f6ab00",
    "452df9213aedb3b9fed6db3e2ea9f49d3db226e2dac01828bc3dcd73b7a953b4"
  ],
  "unlockDelegates": 3
}
[2018-07-21 21:50:876][INFO] DAPP registered, DappId: a09a3917cc1d05b11ed25566634586f8a5100d3d1094b4e93b77a6a227c8b926
[2018-07-21 21:50:692][INFO] dappId "a09a3917cc1d05b11ed25566634586f8a5100d3d1094b4e93b77a6a227c8b926" successfully added to "../asch/config.json"
...
```

Now you can visit your Dapp at `http://localhost:4096/api/dapps/<dappId>/`.

Asch redeploy helps you to watch for changes on your Dapp and re-deploy it automatically. Asch redeploy installs a new Dapp when you change the files of your Dapp every time. Notice that you can stop and restart the tool when you have to change more than one file.

In stead of running Asch redeploy you can also install the Dapp on the Localnet yourself. Follow the instructions at [Dapp Development Tutorial 1: Asch Dapp Hello World](https://github.com/AschPlatform/asch-docs/blob/master/dapp/hello_world/en.md) to do so.

## Create your models
To store our projects and votes in the database we'll have to create the models. Asch use the [SQlite](https://www.sqlite.org/index.html) database and the [JSON-SQL](https://github.com/AschPlatform/json-sql) library for mapping mongo-style query objects to SQL queries. To store your project create a new `models/projects.json` file that contains the following JSON code:


```
module.exports = {
  name: 'projects',
  alias: 'p',
  fields: [
     {
      name: 'id',
      type: 'BigInt',
      not_null: true,
      unique: true,
      primary_key: true
    },   
    {
      name: 'transactionId',
      type: 'String',
      length: 64,
      not_null: true,
      unique: true
    },
    {
      name: 'name',
      type: 'String',
      length: 16,
      not_null: true
    },
    {
      name: 'description',
      type: 'Text',
      not_null: true
    },
    {
      name: 'authorId',
      type: 'String',
      length: 50,
      not_null: true
    },
    {
      name: 'votes',
      type: 'Number',
      not_null: true
    },
    {
      name: 'timestamp',
      type: 'Number',
      not_null: true
    }
  ]
}
```

## Create a smart contract
To create a new project you'll have to pay a fee. So we use a smart contract to create a new project. Create a new `contracts/project.js` file that contains the following code to do so:

```
module.exports = {
  addProject: async function(name, description) {
      app.sdb.create('Project', {
      name: name,
      description: description, 	
      id: app.autoID.increment('project_max_id'),
      transactionId: this.trs.id,
      votes: 0,
      authorId: this.trs.senderId,
      timestamp: this.trs.timestamp
      })
  }
}
```

### Make your contract available

Write down the following code into the `init.js` file now:

```
app.registerContract(1002, 'project.addProject')
```

In the above `1002` is an unique number used to call the contract. The `project.addProjects` string sets up a call to the `addProjects` function in the `contracts/project.js` file created in the [previous step](#create-a-smart-contract). See also [registerContract](https://github.com/AschPlatform/asch-docs/blob/master/sdk_api/en.md#82-appregistercontracttype-name)

###

Optional you can add [parameter validation](https://github.com/AschPlatform/asch-docs/blob/master/sdk_api/en.md#81-appvalidatetype-value) in the contract files like that shown beneath:


```
      app.validate('string', name, { length: { minimum: 1, maximum: 256 }})
      app.validate('string', description, { length: { minimum: 1, maximum: 1024 }})
```

## Create a REST Api endpoint
In this step we create a REST Api endpoint which return the list of projects. Create a new `interface/project.js` file. Write down the following code into this file:

```
app.route.get('/project/all',  async function (req) {
    return await app.model.Project.findAll()
});
```

In the above code the `[app.route.get()](https://github.com/AschPlatform/asch-docs/blob/master/sdk_api/en.md#41-approutegetpath-handler)` call sets up a API endpoint. You can access this API endpoint with a GET call to `http://localhost:4096/api/dapps/<dappId>/project/all`. The `app.model.Project.findAll` queries all data items in the `project` table for the specified condition. More information about the Data Model can be found at: [Data Model of the Asch SDK API](https://github.com/AschPlatform/asch-docs/blob/master/sdk_api/en.md#3-data-model).

## Howto build the user-interface
The HTML UI can be found in the `public/` directory of your Dapp. In this tutorial we'll use a single file to create the UI. The UI is build with HTML and [jQuery](https://jquery.com/). Create a new HTML file called `public/index.html`:

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    
    <title>Asch Mini DAO</title>
    <script
    src="https://code.jquery.com/jquery-3.3.1.min.js" integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8="     crossorigin="anonymous"></script>
    <script type="text/javascript">

    $(document).ready(function() {

	// javacript code here

      });//end of document.ready
      </script>
</head>
<body>
    <h1>Asch Mini DAO</h1>
	<!-- HTML Code here -->
</body>
</html>
```

### The HTML part

#### Create a HTML form to add a new project

```
        <h2>新建项目</h2>
        <div>
            <input type="text" id="projectNameInput" placeholder="请输入项目名称"><br/>
            <textarea rows="6" cols="22" id="projectDescText" placeholder="请输入项目描述"></textarea></br>
            <input type="button" value="新建" id="newProjectBtn">
        </div>
```

#### Create a HTML table to display the project list

```
        <h2>所有项目</h2>
        <div>
            <table id="projectTable" border="1">
                <tr>
                    <th>ID</th>
                    <th>名称</th>
                    <th>描述</th>
                    <th>创建者</th>
                    <th>票数</th>
                    <th>操作</th>
                </tr>
            </table>
        </div>

```

### The javaScript part

#### Add a new project

```
        $('#newProjectBtn').click(function () {
            var prjName = $('#projectNameInput').val();
            var prjDesc = $('#projectDescText').val();
            if (!prjName || !prjDesc) {
                return alert('您输入的内容不正确!');
            }
            var fee = '10000000'
            let data = {
                secret: UserInfo.secret,
                fee: fee,
                type: 1002,
                args: JSON.stringify([prjName,prjDesc])
            }
            invoke(data);
            
  	    $('#projectNameInput').val('');
            $('#projectDescText').val('');
        });
```

##### The invoke() function

The `invoke()` creates a `PUT` request to `/api/dapps/<dappId>/transactions/unsigned`. You can read more about the API at .
Notice that the smart contract is hardcoded set by `type: 1002` as defined in `config.json`. (see: [Make your contract available](#make-your-contract-available))

#### Get the list of projects:

```
	function getProjects() {
            $.ajax({
                type: 'GET',
                url: BASE_URL + '/project/all',
                data: null,
                dataType: 'json',
                success: function (projects) {
                  updateProjectView(projects);
		  return;
                } 
            })	
	}
```

The jQuery code above creates a GET request to `/api/dapps/<dappId>/project/all` and returns a list of projects. We create the REST Api endpoint before, see [Create a REST Api endpoint](#create-a-rest-api-endpoint).

#### Refresh the project list
To refresh the project list every 10 seconds we can use the folloqing code:

```
        State.timer = setInterval(function () {
            if (UserInfo.publicKey) {
		getProjects();
            }
        }, 10 * 1000);
```

##### Update the HTML code 
The `getProjects()` function calls the updateProjectView() which updates the HTML table:

```
        function updateProjectView(projects) {
            // find projects
	    console.log(projects);
	    var $table = $('#projectTable');
            $table.find('tr:not(:first)').remove();
            for (var i = 0; i < projects.length; ++i) {
                var prj = projects[i];
                var keys = ['id', 'name', 'description', 'authorId', 'votes'];
                var values = keys.map(function (k) {
                    return prj[k];
                });
                values.push('<button class="vote-btn">投票</button>');
                $table.append(constructTr(values));
		    invoke(data);
		
                });
            }
        }
```

The complete code also adds a button for voting to the project HTML table. The `constructTr()` function can be found in the source code too.

## The Voting system
Now you shoud be able to setup the voting system yourself. Good Luck.
