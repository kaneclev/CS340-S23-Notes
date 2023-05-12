
### Overview 
This contains an  overview of Day 16 in class. There is an in class  github activity and a bit more on CI/CD. 
### In class activity 
1. Install : openjdk-19-jdk-headless and maven 
2. Sudo apt install "the thing you want to install" 
3. Fork from repo 
4. Clone : git clone "what you forked " 

### Continuous Integration 
	- Frequent merging or rebasing to main 
	- Automatically test this new commit 

### Continuous Delivery / Deployment 
	- Delivery is package up code to deploy /release 
	- Probably don't want to deploy to all users all at once 
	- High risk if something goes wrong 
	-  Deploy to small subset of users 
>### Canary Deployment : Gradually roll out the deployment. This can include :  Rolling Deployment which is where some people get the feature before you get the feature or blue( old deployment) and green (new deployment). This is implemented using cutover method. 
### Challenge with  CI/ CD requiring multiple commits
	- Feature Development / refactoring can take a long time 
	- Longer than the commit/push/deploy pipeline 
	- Idea : break feature into small chunks 
	- The feature is broken or doesn't work …
	- CI/CD deploys this to this end user 
	- How do we handle broken changes being deployed without breaking the code for the user 

