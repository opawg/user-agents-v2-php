# user-agents-v2-php
This is a dummy PHP implementation for both [opawg/user-agents-v2](https://github.com/opawg/user-agents-v2) and [opawg/podcast-rss-useragents](https://github.com/opawg/podcast-rss-useragents)

**Note:** For compatibility issue with [user-agents-php](https://github.com/opawg/user-agents-php) (version 1), the field `os` has not been deleted but is now deprecated and is always empty.

## Installation

### Via composer

- Add `opawg/user-agents-v2-php` to your `composer.json`.
- Add `post-install-cmd` / `post-update-cmd` scripts to your `composer.json` so that the class is generated.

```
{
  "require": {
    "opawg/user-agents-v2-php": "*"
  },
  "scripts": {
    "post-install-cmd": [
      "@php vendor/opawg/user-agents-v2-php/src/UserAgentsGenerate.php >  vendor/opawg/user-agents-v2-php/src/UserAgents.php",
      "@php vendor/opawg/user-agents-v2-php/src/UserAgentsRSSGenerate.php >  vendor/opawg/user-agents-v2-php/src/UserAgentsRSS.php"
    ],
    "post-update-cmd": [
      "@php vendor/opawg/user-agents-v2-php/src/UserAgentsGenerate.php >  vendor/opawg/user-agents-v2-php/src/UserAgents.php",
      "@php vendor/opawg/user-agents-v2-php/src/UserAgentsRSSGenerate.php >  vendor/opawg/user-agents-v2-php/src/UserAgentsRSS.php"
    ]
  }
}
```

### Manually
- Clone git repository where you need it:

```
$ git clone https://github.com/opawg/user-agents-v2-php.git
```

- Generate the classes:

```
$ php src/UserAgentsGenerate.php >  src/UserAgents.php
$ php src/UserAgentsRSSGenerate.php >  src/UserAgentsRSS.php
```

Or with composer:

```
$ composer run-script post-install-cmd
```

## Usage
When you need it, just call `\Opawg\UserAgentsPhp\UserAgents::find()` for audio files or `\Opawg\UserAgentsPhp\UserAgentsRSS::find()` for RSS feed:

```
$player = \Opawg\UserAgentsPhp\UserAgents::find($_SERVER['HTTP_USER_AGENT']);
if($player){
	print player['app']."\n";
	print player['device']."\n";
	print player['os']."\n";
	print player['bot']."\n";
} else {
	print "This user-agent was not found.\n";
}

$service = \Opawg\UserAgentsPhp\UserAgentsRSS::find($_SERVER['HTTP_USER_AGENT']);
if($player){
	print service['name']."\n";
	print service['slug']."\n";
	print service['url']."\n";
} else {
	print "This user-agent was not found.\n";
}
```
