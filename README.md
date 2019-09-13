
## Set up

* Install nodejs and npm

```
[fli@centos ~]$ curl -sL https://rpm.nodesource.com/setup_10.x | sudo -E bash -
[sudo] password for fli: 

## Installing the NodeSource Node.js 10.x repo...


## Inspecting system...

+ rpm -q --whatprovides redhat-release || rpm -q --whatprovides centos-release || rpm -q --whatprovides cloudlinux-release || rpm -q --whatprovides sl-release
+ uname -m

## Confirming "el7-x86_64" is supported...

+ curl -sLf -o /dev/null 'https://rpm.nodesource.com/pub_10.x/el/7/x86_64/nodesource-release-el7-1.noarch.rpm'

## Downloading release setup RPM...

+ mktemp
+ curl -sL -o '/tmp/tmp.6UNUvb1GWm' 'https://rpm.nodesource.com/pub_10.x/el/7/x86_64/nodesource-release-el7-1.noarch.rpm'

## Installing release setup RPM...

+ rpm -i --nosignature --force '/tmp/tmp.6UNUvb1GWm'

## Cleaning up...

+ rm -f '/tmp/tmp.6UNUvb1GWm'

## Checking for existing installations...

+ rpm -qa 'node|npm' | grep -v nodesource

## Run `sudo yum install -y nodejs` to install Node.js 10.x and npm.
## You may also need development tools to build native addons:
     sudo yum install gcc-c++ make
## To install the Yarn package manager, run:
     curl -sL https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee /etc/yum.repos.d/yarn.repo
     sudo yum install yarn

[fli@centos ~]$ sudo yum install -y nodejs
...
[fli@centos ~]$ node -v
v10.16.3
[fli@centos ~]$ which npm
/usr/bin/npm
[fli@centos ~]$ npm -v
6.9.0
[fli@centos ~]$  

[fli@centos ~]$ node
> console.log('Node is running');
Node is running
undefined
> .help
.break    Sometimes you get stuck, this gets you out
.clear    Alias for .break
.editor   Enter editor mode
.exit     Exit the repl
.help     Print this help message
.load     Load JS from a file into the REPL session
.save     Save all evaluated commands in this REPL session to a file
> .exit
[fli@centos ~]$ 
```

* Install yarn

```
curl -sL https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee /etc/yum.repos.d/yarn.repo
sudo yum -y install yarn

[fli@centos ~]$ yarn --version
1.17.3
[fli@centos ~]$ 
```

## The npm config
```
[fli@centos ~]$ npm config list
; cli configs
metrics-registry = "https://registry.npmjs.org/"
scope = ""
user-agent = "npm/6.9.0 node/v10.16.3 linux x64"

; node bin location = /usr/bin/node
; cwd = /home/fli
; HOME = /home/fli
; "npm config ls -l" to show all defaults.

[fli@centos ~]$ npm config get prefix
/usr
[fli@centos ~]$ cd ~ && mkdir .node_modules_global
[fli@centos ~]$ npm config set prefix=$HOME/.node_modules_global
[fli@centos ~]$ npm config get prefix
/home/fli/.node_modules_global 
[fli@centos ~]$ cat .npmrc
prefix=/home/fli/.node_modules_global
[fli@centos ~]$ 

[fli@centos ~]$ npm install npm@latest -g
/home/fli/.node_modules_global/bin/npx -> /home/fli/.node_modules_global/lib/node_modules/npm/bin/npx-cli.js
/home/fli/.node_modules_global/bin/npm -> /home/fli/.node_modules_global/lib/node_modules/npm/bin/npm-cli.js
+ npm@6.11.3
added 430 packages from 833 contributors in 7.04s
[fli@centos ~]$ 

[fli@centos ~]$ echo 'export PATH="$HOME/.node_modules_global/bin:$PATH"' >> .bashrc
[fli@centos ~]$ source .bashrc
[fli@centos ~]$ which npm
~/.node_modules_global/bin/npm
[fli@centos ~]$ npm -v
6.11.3
[fli@centos ~]$ 
```

## Installing Packages in Global Mode
```
[fli@centos ~]$ npm install uglify-js --global
/home/fli/.node_modules_global/bin/uglifyjs -> /home/fli/.node_modules_global/lib/node_modules/uglify-js/bin/uglifyjs
+ uglify-js@3.6.0
added 3 packages from 38 contributors in 0.953s
[fli@centos ~]$ 

[fli@centos ~]$ npm list --global
/home/fli/.node_modules_global/lib
├─┬ npm@6.11.3
│ ├── abbrev@1.1.1
...
└─┬ uglify-js@3.6.0
  ├── commander@2.20.0
  └── source-map@0.6.1

[fli@centos ~]$ 
[fli@centos ~]$ npm list --global --depth=0
/home/fli/.node_modules_global/lib
├── npm@6.11.3
└── uglify-js@3.6.0

[fli@centos ~]$ 
```

## use the Uglify package to minify 'example.js' into 'example.min.js'
```
[fli@centos ~]$ uglifyjs example.js -o example.min.js
```

## Installing Packages in Local Mode

* create package.json
```
[fli@centos koala-node]$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (koala-node) 
version: (1.0.0) 
description: koala app
entry point: (index.js) 
test command: 
git repository: git@github.com:fen9li/koala-node.git
keywords: node
author: Feng Li
license: (ISC) Apache-2.0
About to write to /home/fli/koala-node/package.json:

{
  "name": "koala-node",
  "version": "1.0.0",
  "description": "koala app",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+ssh://git@github.com/fen9li/koala-node.git"
  },
  "keywords": [
    "node"
  ],
  "author": "Feng Li",
  "license": "Apache-2.0",
  "bugs": {
    "url": "https://github.com/fen9li/koala-node/issues"
  },
  "homepage": "https://github.com/fen9li/koala-node#readme"
}


Is this OK? (yes) 
[fli@centos koala-node]$ 

[fli@centos koala-node]$ cat package.json 
{
  "name": "koala-node",
  "version": "1.0.0",
  "description": "koala app",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+ssh://git@github.com/fen9li/koala-node.git"
  },
  "keywords": [
    "node"
  ],
  "author": "Feng Li",
  "license": "Apache-2.0",
  "bugs": {
    "url": "https://github.com/fen9li/koala-node/issues"
  },
  "homepage": "https://github.com/fen9li/koala-node#readme"
}
[fli@centos koala-node]$ 
```

* Git housekeeping
```
[fli@centos koala-node]$ git init
Initialized empty Git repository in /home/fli/koala-node/.git/
[fli@centos koala-node]$ 

git config --global user.name "Feng Li"
git config --global user.email "lifcn@yahoo.com"
git remote add origin git@github.com:fen9li/koala-node.git

[fli@centos koala-node]$ git remote -v
origin	git@github.com:fen9li/koala-node.git (fetch)
origin	git@github.com:fen9li/koala-node.git (push)
[fli@centos koala-node]$ 

[fli@centos koala-node]$ git pull origin master
From github.com:fen9li/koala-node
 * branch            master     -> FETCH_HEAD
[fli@centos koala-node]$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	README.md
	package.json

nothing added to commit but untracked files present (use "git add" to track)
[fli@centos koala-node]$ 

[fli@centos koala-node]$ git checkout -b develop
Switched to a new branch 'develop'
[fli@centos koala-node]$ git status
On branch develop
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	README.md
	package.json

nothing added to commit but untracked files present (use "git add" to track)
[fli@centos koala-node]$ 
```

* Install a package
```
npm install underscore

[fli@centos koala-node]$ pwd
/home/fli/koala-node
[fli@centos koala-node]$ 

[fli@centos koala-node]$ tree
.
├── LICENSE
├── node_modules
│   └── underscore
│       ├── LICENSE
│       ├── package.json
│       ├── README.md
│       ├── underscore.js
│       ├── underscore-min.js
│       └── underscore-min.js.map
├── package.json
├── package-lock.json
└── README.md

2 directories, 10 files
[fli@centos koala-node]$ 

[fli@centos koala-node]$ cat package.json 
{
  "name": "koala-node",
  "version": "1.0.0",
  "description": "koala app",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+ssh://git@github.com/fen9li/koala-node.git"
  },
  "keywords": [
    "node"
  ],
  "author": "Feng Li",
  "license": "Apache-2.0",
  "bugs": {
    "url": "https://github.com/fen9li/koala-node/issues"
  },
  "homepage": "https://github.com/fen9li/koala-node#readme",
  "dependencies": {
    "underscore": "^1.9.1"
  }
}
[fli@centos koala-node]$ cat package-lock.json 
{
  "name": "koala-node",
  "version": "1.0.0",
  "lockfileVersion": 1,
  "requires": true,
  "dependencies": {
    "underscore": {
      "version": "1.9.1",
      "resolved": "https://registry.npmjs.org/underscore/-/underscore-1.9.1.tgz",
      "integrity": "sha512-5/4etnCkd9c8gwgowi5/om/mYO5ajCaOgdzj/oW+0eQV9WxKBDZw5+ycmKmeaTXjInS/W0BzpGLo2xR2aBwZdg=="
    }
  }
}
[fli@centos koala-node]$ 
```

* Remove a package
```
[fli@centos koala-node]$ npm list
koala-node@1.0.0 /home/fli/koala-node
└── underscore@1.9.1

[fli@centos koala-node]$ npm uninstall underscore
removed 1 package in 0.866s
found 0 vulnerabilities

[fli@centos koala-node]$ npm list
koala-node@1.0.0 /home/fli/koala-node
└── (empty)

[fli@centos koala-node]$ 

[fli@centos koala-node]$ tree
.
├── LICENSE
├── package.json
├── package-lock.json
├── README.md
└── test.js

0 directories, 5 files
[fli@centos koala-node]$ cat package.json 
{
  "name": "koala-node",
  "version": "1.0.0",
  "description": "koala app",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+ssh://git@github.com/fen9li/koala-node.git"
  },
  "keywords": [
    "node"
  ],
  "author": "Feng Li",
  "license": "Apache-2.0",
  "bugs": {
    "url": "https://github.com/fen9li/koala-node/issues"
  },
  "homepage": "https://github.com/fen9li/koala-node#readme",
  "dependencies": {}
}
[fli@centos koala-node]$ 
```

## Search and install package
```
[fli@centos koala-node]$ npm search mkdir
NAME                      | DESCRIPTION          | AUTHOR          | DATE       | VERSION  
mkdir                     | Directory creation…  | =joehewitt      | 2012-04-17 | 0.0.2    
output-file-sync          | Synchronously write… | =shinnn         | 2018-02-15 | 2.0.1    
mkdirp                    | Recursively mkdir,…  | =isaacs…        | 2015-05-14 | 0.5.1    
fs-extra                  | fs-extra contains…   | =jprichardson…  | 2019-06-28 | 8.1.0    
safe-mkdir                | mkdir that ignores…  | =talles         | 2016-06-16 | 1.0.4    
write-file                | Writing a file to…   | =vanchoy…       | 2016-11-02 | 1.0.0    
write-json                | Write a JSON file…   | =jonschlinkert  | 2018-01-26 | 3.0.1    
util-mkdirs               | mkdirs recursively…  | =yxxy           | 2017-09-27 | 1.0.3    
mk-dirs                   | A tiny (420B)…       | =lukeed         | 2019-06-09 | 2.0.0    
writestreamp              | A file write stream… | =fent           | 2017-10-26 | 1.1.0    
siwi-mkdirs               | Creating multilevel… | =siwi           | 2018-07-25 | 1.0.0    
utilityFileSystem         | Utility functions…   | =chouchua       | 2017-11-07 | 1.0.11   
recur-fs                  | A collection of…     | =popeindustries | 2016-11-08 | 2.2.4    
nor-fs                    | Asynchronous file…   | =jhh            | 2016-07-30 | 1.0.0    
make-dir                  | Make a directory…    | =sindresorhus   | 2019-04-01 | 3.0.0    
@fcostarodrigo/open-path  | Node module that…    | =fcostarodrigo  | 2019-07-28 | 5.0.1    
@wrote/ensure-path        | Create all…          | =zvr            | 2019-07-03 | 1.1.0    
zmkdirp                   | zeen3's mkdirp…      | =zanehannanau…  | 2018-04-04 | 2.0.1    
then-write-json           | Write contents to…   | =vanchoy…       | 2015-05-31 | 1.0.0    
rfc-open-path-sync        | Create nested…       | =fcostarodrigo  | 2017-03-26 | 1.0.2    
[fli@centos koala-node]$ npm install mkdirp
+ mkdirp@0.5.1
added 2 packages from 1 contributor and audited 2 packages in 1.199s
found 0 vulnerabilities

[fli@centos koala-node]$ 

[fli@centos koala-node]$ npm list
koala-node@1.0.0 /home/fli/koala-node
└─┬ mkdirp@0.5.1
  └── minimist@0.0.8

[fli@centos koala-node]$ cat package.json 
{
  "name": "koala-node",
  "version": "1.0.0",
  "description": "koala app",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+ssh://git@github.com/fen9li/koala-node.git"
  },
  "keywords": [
    "node"
  ],
  "author": "Feng Li",
  "license": "Apache-2.0",
  "bugs": {
    "url": "https://github.com/fen9li/koala-node/issues"
  },
  "homepage": "https://github.com/fen9li/koala-node#readme",
  "dependencies": {
    "mkdirp": "^0.5.1"
  }
}
[fli@centos koala-node]$ 

```

## test.js
```
[fli@centos koala-node]$ cat test.js 
const mkdirp = require("mkdirp");
mkdirp("foo", function(err) {
  if (err) console.error(err);
  else console.log("Directory created!");
});
[fli@centos koala-node]$ 

[fli@centos koala-node]$ node test.js 
Directory created!
[fli@centos koala-node]$ 

[fli@centos koala-node]$ ll
total 40
drwxrwxr-x. 2 fli fli     6 Sep 13 22:50 foo
-rw-rw-r--. 1 fli fli 11357 Sep 13 22:04 LICENSE
drwxrwxr-x. 5 fli fli    48 Sep 13 22:45 node_modules
-rw-rw-r--. 1 fli fli   546 Sep 13 22:45 package.json
-rw-rw-r--. 1 fli fli   536 Sep 13 22:45 package-lock.json
-rw-rw-r--. 1 fli fli 13383 Sep 13 22:47 README.md
-rw-rw-r--. 1 fli fli   141 Sep 13 22:49 test.js
[fli@centos koala-node]$
```

## Managing npm Cache
```
[fli@centos koala-node]$ ll ~/.npm
total 4
-rw-rw-r--. 1 fli fli 171 Sep 13 22:36 anonymous-cli-metrics.json
drwxrwxr-x. 5 fli fli  51 Sep 13 21:12 _cacache
drwxrwxr-x. 2 fli fli   6 Sep 13 22:36 _locks
drwxrwxr-x. 2 fli fli  48 Sep 13 21:12 _logs
[fli@centos koala-node]$ npm cache clean --force
npm WARN using --force I sure hope you know what you are doing.
[fli@centos koala-node]$ ll ~/.npm
total 4
-rw-rw-r--. 1 fli fli 171 Sep 13 22:36 anonymous-cli-metrics.json
drwxrwxr-x. 2 fli fli   6 Sep 13 22:36 _locks
drwxrwxr-x. 2 fli fli  48 Sep 13 21:12 _logs
[fli@centos koala-node]$ 
```

## npm command commonly used aliases
```
npm i <package> – install local package
npm i -g </package><package> – install global package
npm un </package><package> – uninstall local package
npm up – npm update packages
npm t – run tests
npm ls – list installed modules
npm ll or npm la – print additional package information while listing modules
```

## [About GitHub Package Registry](https://help.github.com/en/articles/about-github-package-registry)
