### KoBoToolbox Dev -> Staging -> Production

1. We have forked the main kobotoolbox/kpi
   * We could do similar with kobotoolbox/kobocat if needed
1. We have made a dai-collect branch for our repo
1. We have made changes to those dai-collect branch
1. We test those changes on a dev/staging site with local files
1. Once changes are complete, we tag our version of the dai-collect branch 
1. Rebuild docker image in docker hub
1. On staging we change the docker-compose.frontend.override.yml
1. Testing on staging
1. On production we change the docker-compose.frontend.override.yml
1. Go live



### Key Principles
1. Do not make DAI changes in the master branch
   * This makes it easy to pull in upstream changes from kobotoolbox repos
1. DAI changes should be done in the dai-collect branch
1. Tags should be of the form dai-collect-vX.Y.Z
   * We do not want to conflict with tags in main kobotoolbox repo	


### Create new DAI Collect release image


##### Make sure you have kobotoolbox repo as upstream remote repo
```
git remote add upstream git@github.com:kobotoolbox/kpi.git
```

##### Fetch upstream
```
git fetch upstream --tags
```

##### Checkout master repo
```
git checkout master
```

##### Merge upstream into master
```
git merge upstream/master
```

##### Push changes to github
```
git push --tags
```

##### Align with kobotoolbox release
```
git checkout dai-collect
git merge <tag>
git push
```


##### Tagging Example
```
# Make the verion number part of the tag match the release from kobotoolbox
git tag -a dai-collect-v2.020.25 -m "updated landing page with DAI branding message"
git push origin dai-collect-v0.020.25

```

#### Docker Hub

There is an auto-build rule that creates news images in DockerHub whenever a new dai-collect-vX.Y.Z tag is pushed to github.
