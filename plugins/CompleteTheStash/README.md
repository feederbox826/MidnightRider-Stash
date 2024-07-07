# Complete The Stash

This plugin is designed to compare local performer scenes with those available on StashDB. Any missing scenes will be created in a separate, missing Stash instance.

This plugin will not add, modify or delete anything in your main Stash instance. This plugin will read which performers you have tagged to be included in the comparison, get a list of all scenes of those performers from StashDB and create these missing scenes in the separate, missing Stash instance. Now you can easily see from that separate instance which scenes you are missing and you can filter those by site or by tags.

## History

This plugin was originally developed by Serechops but due to major overhaul it was split as a separate plugin.

You can find the original plugin here: https://github.com/Serechops/Serechops-Stash/tree/main/plugins/performerSceneCompare#performer-scene-compare

## Features

- Compare local performer scenes with StashDB.
- Automatically create missing scenes with studios, tags and descriptions in a separate, missing Stash instance for performers tagged with your configured tag (by default Completionist).
- Missing scenes can be excluded by tags e.g. for avoiding compilations.
- Missing scenes are automatically deleted from the missing Stash instance when you add those to your main Stash.

## Requirements

`pip install stashapp-tools`

## Configuration

```
  LOCAL_GQL_SCHEME = "http"
  LOCAL_GQL_HOST = "localhost"
  LOCAL_GQL_PORT = 9999
  LOCAL_API_KEY = ""  # Leave blank if you don't have credentials on your Stash.

  MISSING_GQL_SCHEME = "http"
  MISSING_GQL_HOST = "localhost"
  MISSING_GQL_PORT = 6969
  MISSING_API_KEY = ""  # Leave blank if you don't have credentials on your missing Stash.

  STASHDB_ENDPOINT = "https://stashdb.org/graphql"
  STASHDB_API_KEY = "your_stashdb_api_key"  # Replace with your StashDB API key

  PERFORMER_TAGS = ["Completionist"]  # Performers with these tags will be selected.

  EXCLUDE_TAGS = []  # Scenes containing any of these tags will be excluded.
```

## Usage

The script is designed to be executed as a plugin within Stash. It is triggered by:

- Executing "Process performers" task manually. This will create, update and possibly delete missing scenes.
- Local scene being updated. If a previously missing scene is now found in local Stash, it is deleted from missing Stash.

The separate task for longer running processing is critical for good user experience. For example if performer processing was triggered when a performer is tagged with Completionist, local Stash UI would look like being stuck until all, possibly thousands of scenes for that performer would have been processed.