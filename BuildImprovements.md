# Process Improvements for 4.1

## Code Reviews
Set all repos (-dotnet, -js, -java, -python, -samples, -tools) to required code reviews for everyone (including admins).

## Branching
Review branching strategy so everyone is on the same page. 

| Branch  |Version   |Description
|---|---|---|
|master|4.1.0|This is **tip**. Current work goes in here. This branch has nightly builds pushed to myget using the 4.1.0-preview.{BuildNumber} tag. We *may* push preview bits (using the -preview tag) to npm/nuget at some point, as the semver rules mean this won't break any of our users. 
|4.0 |4.0.7|This is our official 4.0.7 release. BUG FIXES made against the 4.0 branch happen here, and trigger a new manual build (4.0.8), and are then cherrypicked into master. Future releases from the 4.0 branch are git-labeled, but do not result in creation of new branches. This branch DOES NOT have a nightly build. I am able to perform builds + packages + publishing against it. 


## Samples Process Improvements
Add CI + Daily builds, so branches are compiled before merging (C# / TS). 

Develop a plan for how to *test* the samples. 

Improve the VSIX build process 
1. Remove .zip from the build. 
2. Look at generating the template projects
3. Eval level-of-effort to test the VSIX as part of the build. 
4. Check w/ Scott on Yeoman improvements. 

### Integration with ABS
Today the deployment of samples to ABS Blobs is done by hand. Adding this to a nightly build process would provide better everything. How to do this, and how to test? 

### Build against botbuiler-samples **master** should:
1. Build all C# samples against PUBLIC packages. 
2. Build all Typescript samples against PUBLIC packages. 
3. Have a build-badge indicating pass/fail. Send email on failure.

### Builds against V.Next Branch should:
1. Use a Package Redirect (NPM + NuGet) to pickup daily packages from MyGet. 
2. Build C# / TS samples against the daily packages. 

## DotNet Process Improvements
1. Cleanup the CI/CD build pipelines.
2. Unify the CI/CD build and the nightly build. Package generation / signing / publishing should be contitional, and that condition should be set from a Cron, or via an variable settable at build queue time. 
3. Get external PRs building as part of the PR builds. Eval impact of secrets on this. 
4. Validate the Coveralls results. Current results seem questionable. 
5. Figure out how to run tests on both Windows and Linux.
6. Write tests. 
7. Nightly build should trigger Samples build. 

## JS Process Improvements
1. Consider moving from Travis to Azure DevOps.
2. Figure out how to run tests on both Windows and Linux.
3. Code Coverage improvements.
4. Setup a real CRON job. 
5. Enable easy "explicit version" publishing.

## Transcript based testing
1. Plan for testing both C# + JS dialog system using transcript file(s).

## Recognizers-Text 
1. Add CI/CD build for Recognizers-Text in C#
2. Add CI/CD build for Recognizers-Test in JS
3. Add CI/CD build for Recognizers-Test in Java
4. Build + Sign + Publish (to Daily Feed) the relevant packages (NPM / Nuget / Maven).
