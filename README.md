A [mysql2](https://github.com/sidorares/node-mysql2) fork of the [mysql-semaphore](https://www.npmjs.com/package/mysql-semaphore) library for Node.js and MySQL. Allows you to generate a semaphore in a clustered Node.js environment using MySQL. This is useful for such things as cron jobs or long running tasks that you only want to occur on a single instance. 

Requirements:
MySQL server

### Installation

```sh
npm install mysql2-semaphore --save
```

### Initialization:

Refer to [mysql2 documentation](https://github.com/sidorares/node-mysql2) for MySql configuration settings.

```sh
var Semaphore = require('mysql-semaphore');
var semaphore = new Semaphore({host: 'localhost', database: 'mydb', user: 'someuser', password: 'somepassword'});
```

### Before You Begin:
Be aware that this library requires that the lock name be unique for a particular usage. If another application uses the same lock name, a lock could be inadvertantly unlocked. It is recommended that the lock name include application and database name and usage to ensure uniqueness - for example: mydb_myapp_myprocess as the lockName parameter.

### Methods:

#### Get Lock

```sh
semaphore.lock('test', 2) //test is the lock name
	.then(function(didLock){
		//didLock will be true if lock is successful, false if unable to attain a lock
		console.log(didLock);
	})
	.catch(function(err){
		console.log(err);
	});
```

#### Release Lock

```sh
semaphore.unlock('test') //test is the lock name
	.then(function(didUnlock){
		console.log('unlocked!', didUnlock);
	})
	.catch(function(err){
		console.log(err);
	});
```

#### Check If Locked

```sh
semaphore.islocked('test') //test is the lock name
	.then(function(isLocked){
		console.log('islocked', isLocked);
	})
	.catch(function(err){
		console.log(err);
	})
```


### Tests:

```sh
npm test
```
