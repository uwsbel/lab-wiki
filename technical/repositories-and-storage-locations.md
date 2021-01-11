# Repositories and Storage Locations

As people join and leave the lab relatively frequently, it's really important to keep a record of what people worked on, no matter how small the project. If you're starting a new project, or find yourself organizing many projects on your local machine, this page should help you find a home for the work you're doing. 

Basically, if you are doing some SBEL-related work and are thinking of saving it *only* on your local machine, think really hard and consult this list -- find a place to save it that everyone will be able to access it in the future.

## Git-based

### Chrono (projectchrono/chrono)

_Write-up in progress_

### Chrono-internal (uwsbel/chrono-internal)

Chrono-internal is a place for Chrono code that is not ready for prime-time yet. Specifically, it is only viewable to SBEL members, so it's perfect for long-term additions to Chrono that are in flight but that aren't stable enough to be on a feature branch of the main Chrono repository just yet. For example `Chrono::Sensor` and `SynChrono` started their development life in chrono-internal. 

Please start a separate branch in chrono-internal for your project, so that the develop branch can stay up to date with the latest and greatest from the main Chrono repository. 

This repository should periodically be refreshed from the main chrono repository. To do this you can add a separate remote repo (in this example called 'upstream') to your local copy of chrono-internal

````bash
git remote add upstream git@github.com:projectchrono/chrono.git
````

After this when you run `git remote -v` you should see four items listed, two for the new 'upstream', and two for your original remote that points to chrono-internal (likely called 'origin'). With the new remote in place, you can refresh chrono-internal from the main repo with:

````bash
git pull upstream
git push origin
````
you are pulling into your local copy from the main chrono repo (upstream) and then pushing to the chrono-internal copy that github has (origin)


### Chrono-tutorial (projectchrono/chrono-tutorial)

_Write-up in progress_