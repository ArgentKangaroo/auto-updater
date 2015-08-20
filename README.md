# Auto-Updater

[Node.js](http://nodejs.org/) auto-update plugin.

# Installation
	
With [npm](http://npmjs.org) do:

    $ npm install auto-updater

# What does it do?

 * Compares local version with remote version.
 * If versions dont match, it downloads the repository.
 * It extracts the repository, overwriting the modifies files.
 * Compares local dependencies with remote dependencies and tells if they don't match.

# Events

 * `git-clone` The user has a git clone. Recommend use the "git pull" command
 * `check.up-to-date ( v )` versions match
 * `check.out-dated ( v_old , v)` versions dont match
 * `update.downloaded` Update downloaded in the machine
 * `update.not-installed` Update was already in the dir, so it wasnt installed
 * `update.extracted` The update has been extracted correctly.
 * `download.start ( name )` The download of "name of the update" has started
 * `download.progress ( name , % )` The download has been updated. New percentage
 * `download.end ( name )` The download has ended
 * `download.error ( err )` Something happened to the download
 * `end` Called when all is over ( along with 'check-up-to-date' if there are no updates, or with 'extracted' if it was installed )

# Public Methods:

 * `use ( config )`
 * `on ( event, callback )` Sets the events ([EventEmitter](https://nodejs.org/api/events.html#toc) compatible)
 * `fire ( command )` Fires a command

## Config
 * `pathToJson: ''` from repo main folder to package.json (only subfolders. Can't go backwards)
 * `autoupdate: false` if true, all stages run one after the other. Else, you need to force the stages with the force methods
 * `checkgit: true` Checks if the .git folder exists, so its a dev and doesnt download the proyect.
 * `jsonhost: 'raw.githubusercontent.com'` URL of raw remote package.json
 * `contenthost: 'codeload.github.com'` URL of full remote zip
 * `progressDebounce: 0` URL of full remote zip

## Commands
 * `check-dependencies` Returns bool if client has all the remote dependencies. Undefined if they weren't checked yet (need forceCheck first)
 * `diff-dependencies` Returns an array of dependencies (only the names) that dont match
 * `check` Compares the two versions. Triggers: 'git-clone','check-up-to-date','check-out-dated'
 * `download-update` Downloads the update. Triggers: 'update-downloaded','update-not-installed','download-*'
 * `force-extract` Extracts (or installs) the update reeplacing old files (it doesnt delete untracked files). Triggers: 'update.extracted'

Warning: do not run this methods in other order.

# Package.json configuration
	
	"version":"0.0.1",
	"auto-updater":{
		"repo":"/github-user/github-repo",
		"branch":"master"
	}

That segment must be added to the proyect (local). It is critical that the package.json of the app you are using has a version field (so it can be compared with the remote package.json stored on github), and the auto-updater field, so it knows where to get the remote data.

# Example
```javascript
	
```

# Dependencies
 * [Adm-zip](https://github.com/cthackers/adm-zip)
 * [underscore](https://www.npmjs.com/package/underscore)
 * [node-promise](https://www.npmjs.com/package/node-promise)