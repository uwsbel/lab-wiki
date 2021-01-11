# Repositories and Storage Locations

As people join and leave the lab relatively frequently, it's really important to keep a record of what people worked on, no matter how small the project. If you're starting a new project, or find yourself organizing many projects on your local machine, this page should help you find a home for the work you're doing. 

Basically, if you are doing some SBEL-related work and are thinking of saving it *only* on your local machine, think really hard and consult this list -- find a place to save it that everyone will be able to access it in the future.

## Git-based

### Chrono (projectchrono/chrono)

_Write-up in progress_

### Chrono-internal (uwsbel/chrono-internal)

Chrono-internal is a place for Chrono code that is not ready for prime-time yet. Specifically, it is only viewable to SBEL members, so it's perfect for long-term additions to Chrono that are in flight but that aren't stable enough to be on a feature branch of the main Chrono repository just yet. For example `Chrono::Sensor` and `SynChrono` started their development life in chrono-internal. 

Please start a separate branch in chrono-internal for your project, so that the develop branch can stay up to date with the latest and greatest from the main Chrono repository. 

**Refreshing chrono-internal**

This repository should periodically be refreshed from the main chrono repository. I'll assume that you already have a remote called 'origin' that tracks the chrono-internal repo (you can check with `git remote -v`). To sync with the main chrono repo, you can add _another_ remote (I call it 'upstream', but you could choose a different name). To add the additional repo, run one of the following commands:

````bash
git remote add upstream git@github.com:projectchrono/chrono.git         (ssh version)
git remote add upstream https://github.com/projectchrono/chrono.git     (https version)
````

Just as you can `git push` and `git pull` from origin which points to `chrono-internal`, by using the name upstream, you can `git pull` (you should **never** `git push` to upstream). After this when you run `git remote -v` you should see four items listed, two for the new 'upstream', and two for your original remote that points to chrono-internal (likely called 'origin'). 

With the new remote in place, you are now capable of refreshing chrono-internal from the main repo. Before you do so ensure that your local `chrono-internal/develop` branch has no diverging commits and is up to date with the remote chrono-internal. You should not produce a merge commit when you `git pull`. If everything is ready you can do:

````bash
git pull upstream
git push origin
````
you are pulling into your local copy from the main chrono repo (upstream) and then pushing to the chrono-internal copy that github has (origin).


### Chrono-tutorial (projectchrono/chrono-tutorial)

_Write-up in progress_