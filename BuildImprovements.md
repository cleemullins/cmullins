# Process Improvements for 4.1

## Code Reviews
Set all repos (-dotnet, -js, -java, -python, -samples, -tools) to required code reviews for everyone (including admins).

## Branching
Review branching strategy so everyone is on the same page. 

## Samples Process Improvements
Add CI + Daily builds, so branches are compiled before merging (C# / TS). 

This public build should:
1. Build all C# samples against PUBLIC packages. 
2. Build all Typescript samples against PUBLIC packages. 
3. Have a build-badge indicating pass/fail. Send email on failure. 

Develop a plan for how to *test* the samples. 
Develop a plan for building + testing v.Next samples against Daily Build Nuget / NPM packages. 

Improve the VSIX path. 
1. Remove remove .zip from the build. 
2. Look at generating the template projects
3. Eval level-of-effort to test the VSIX as part of the build. 
4. Check w/ Scott on Yeoman improvements. 

Integration with ABS. The deployment of samples to ABS Blobs is done by hand. Adding this to a nightly build process would provide better everything. 

## DotNet Process Improvements
1. Cleanup the CI/CD build pipelines.
2. The nightly builds should run tests
3. Get external PRs building as part of the PR builds. 
4. Enable + Publish Coveralls (+badge)
5. Figure out how to run tests on both Windows and Linux.
6. Write tests. 
7. Nightly build should trigger Samples build. 


## JS Process Improvements
1. Debate moving build from Travis to Azure DevOps.
2. Figure out how to run tests on both Windows and Linux.
3. Code Coverage improvements
4. Setup a real CRON job. 
5. Enable easy "explicit version" publishing. 

## Transcript based testing
1. Plan for testing both C# + JS dialog system using transcript file(s).