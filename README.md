# exp1

Experiment – 1: Git Branching and Merging
1. Initialize Git repository
Open VS Code → Open the experiment folder → Open Terminal.
Execute:
git init
git config --global user.name "username"
git config --global user.email "email "

Create a file named calculator.py.
Initial code:
def calculate(a,b):    
          return a+b
a=10
b=20
print(calculate(a,b))


2. Check status and make initial commit
Execute:
git status
Output: Untracked file – calculator.py

git add .
git status
Output: New file – calculator.py (staged for commit)

Commit the file:
git commit -m "Initial commit"
Expected output:
[master (root-commit) <commit-id>] Initial commit
1 file changed, 7 insertions(+)
create mode 100644 calculator.py


3. Create branches and make changes
A. Create branch b1
git branch
Output:
* master

Create and switch to b1:
git branch b1
git switch b1

Modify the last print statement in calculator.py.
Code in b1:
def calculate(a,b):        
          return a+b
a=10
b=20
print("Answer 1:", calculate(a,b))
Save and commit:
git add .
git commit -m "Branch 1"


B. Create branch b2
First switch back to master:
git switch master

Create b2 and switch to it:
git branch b2
git switch b2

Modify the last print statement in calculator.py.
Code in b2:
def calculate(a,b):    
           return a+b
a=10
b=20
print("Answer 2:", calculate(a,b))

Save and commit:
git add .
git commit -m "Branch 2"


C. View commit history
git log
Output: Displays all commits in the current branch.

Check branches:
git branch
Output:
  b1
* b2
  Master


4. Merge branch b1 into master (Without conflict)
Switch to master:
git switch master

Merge b1:
git merge b1

Fast-forward merge – No conflict
Expected output:
Updating <old-commit>..<new-commit>
Fast-forward
 calculator.py | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)


Final code in master:
def calculate(a,b):    
            return a+b
a=10
b=20
print("Answer 1:", calculate(a,b))

Execute the Python file:
python calculator.py
Output:
Answer 1: 30


5. Merge branch b1 into b2 (With conflict)
Switch to b2:
git switch b2

Merge b1:
git merge b1
Merge conflict occurs

Expected output:
Auto-merging calculator.py
CONFLICT (content): Merge conflict in calculator.py
Automatic merge failed; fix conflicts and then commit the result.

A. Resolve the conflict
Open calculator.py in VS Code.
Git may show:
<<<<<<< HEADprint("Answer 2:", calculate(a,b))=======print("Answer 1:", calculate(a,b))>>>>>>> b1
Select Accept Both Changes in VS Code or manually replace the conflict section.
Final code after resolving the conflict:
def calculate(a,b):
          return a+b
a=10
b=20
print("Answer 2:", calculate(a,b))
print("Answer 1:", calculate(a,b))
Conflict resolved

B. Add and commit the resolved file
Save the file and execute:
git add .
git commit -m "Resolved merge conflict"

C. Execute the Python program
python calculator.py
Expected output:
Answer 2: 30
Answer 1: 30


6. Final verification
git status
Expected output:
On branch b2
nothing to commit, working tree clean














Experiment – 2: Maven dependencies 
1.	Open eclipse
2.	File -> new -> maven project 
3.	Click next -> type “maven-archetype-quickstart” -> select latest version (1.1 or 1.5) -> click on next
4.	Type: 
Group ID: Test1
ArtifactID: test1
Click on finish
5.	After building.. Type y in terminal
6.	Right click on project->new->class
Classname – ReadJson
Type the code: (ReadJson.java)
package Test1.test1;
import java.io.*;
import org.json.simple.*;
import org.json.simple.parser.*;

public class ReadJson {
	public static void main(String[] args) throws Exception{
		JSONParser jsonparser=new JSONParser();
		FileReader reader=new FileReader("./JSON/student.json");
		
		Object obj=jsonparser.parse(reader);
		JSONObject studentobj=(JSONObject) obj;
		
		String fname=(String) studentobj.get("firstname");
		String lname=(String) studentobj.get("lastname");
		
		System.out.println("First name: "+fname);
		System.out.println("Last name: "+lname);
	}
}
7.	Right click on project -> New Folder -> Folder name: JSON 
8.	Right click on JSON -> New File -> File name: student.json
9.	Type the code: 
{ “firstname” : “ABC”,
   “lastname” : “D”  }
10.	Open browser -> type “maven repositories” ->  search “simple json” ->click on first one
11.	Scroll down to versions -> Select “1.1” version -> Scroll down -> Copy the code snippet
12.	Open pom.xml in eclipse -> find <dependencies> part -> paste the code snippet copied inside <dependencies> -> Save the file
13.	Json.simple.1.1 will be there under maven dependencies in the project structure at left.
Try changing 1.1 in the pom.xml to 1.1.1 and the file under maven dependencies will be updated to 1.1.1
14.	Open ReadJson and click on run
OUTPUT: First name: ABC
                 Last name: D






















Experiment – 3 : Docker container
1.	Open VS Code 
2.	Create a folder –> Create files index.html and dockerfile
3.	Type the code: 

index.html
<html>
<head>
         <title> Welcome ! </title>
</head>
<body>
         <h1> Hello from docker ! </h1>
         <p> Web app is successfully containerized </p>
</body>
</html>

dockerfile
FROM httpd:latest
COPY index.html /usr/local/apache2/htdocs/

4.	Login to docker desktop and docker hub
5.	Type commands
docker build -t profile .
docker run -d –name c1 -p 9090:80 profile
6.	Open browser and type url 
localhost:9090
7.	Open docker desktop -> Go to images -> Copy the image ID
8.	Type commands
docker tag (paste image ID) “username”/profile
9.	Push
docker push “username”/profile
10.	Pull from others
docker pull “username”/”imagename”











Experiment – 4: Kubernetes orchestration, scaling up and down, load balancing

1.	Open VS Code 
2.	Create a folder –> Create files index.html and dockerfile
3.	Type the code: 

index.html
<html>
<head>
         <title> Welcome ! </title>
</head>
<body>
         <h1> Hello from docker ! </h1>
         <p> Web app is successfully containerized </p>
</body>
</html>

dockerfile
FROM httpd:latest
COPY index.html /usr/local/apache2/htdocs/

4.	Login to docker desktop and docker hub
5.	Type commands
docker build -t profile .
docker run -d –name c1 -p 9090:80 profile

6.	Open browser and type url 
localhost:9090
Open docker desktop -> Go to Kubernetes -> Create cluster
Select kubeadm -> Create -> Install

7.	Type commands: 
kubectl version 

8.	Copy paste deployment.yml and service.yml
Change name, app, image to the imagename (profile)

9.	Type commands:
kubectl apply -f deployment.yml
kubectl get deployments
kubectl get pods                       (OUTPUT: 3)
kubectl apply -f service.yml
kubectl get services 

10.	Scaling up and down
kubectl scale deployment profile - -replicas=5
kubectl get pods                       (OUTPUT: 5)
kubectl scale deployment profile - -replicas=2
kubectl get pods                       (OUTPUT: 2)

11.	High availability
kubectl delete pod (pod name)
kubectl get pods                              (that pod gets deleted and gets replaced)

12.	Load balancing
kubectl get endpoints profile          (10.1.0.11:80,10.1.0.6:80)

























Experiment – 5 : Jenkins and Slack integration

1. Create a GitHub repository
1.	Open GitHub.
2.	Click New repository.
3.	Repository name: Slack-Experiment.
4.	Select Public.
5.	Click Create repository.

2. Create main.py
1.	Open the newly created repository.
2.	Click Add file → Create new file.
3.	File name: main.py.
4.	Enter the following code:
print("DevOps")
print(“VVCE”)
5. Click Commit changes to save the file.

3. Create a Jenkins project
1.	Open Jenkins.
2.	Click New Item.
3.	Enter item name: Slack-Notifier.
4.	Select Freestyle project.
5.	Click OK.

4. Configure Source Code Management
In the project configuration page:
1.	Go to Source Code Management.
2.	Select Git.
3.	Repository URL: Copy and paste your GitHub repository URL.
Example:
https://github.com/username/Slack-Experiment.git
4.	Under Branches to build, change the branch name to:
*/main

5. Configure Build Steps
1.	Scroll to Build Steps.
2.	Click Add build step.
3.	Select Execute Windows batch command.
4.	Open Command Prompt and execute:
where python
5.	Copy the first Python installation path.
6.	In the Jenkins command box, enter:
"path" main.py

6. Configure Post-build Actions
1.	Scroll down to Post-build Actions.
2.	Select Slack Notifications.
3.	Enable these options:
o	Notify Build Start
o	Notify Success
o	Notify Every Failure
4.	Click Apply.
5.	Click Save.
Jenkins job configuration completed

7. Create a Slack workspace
1.	Open Google Chrome.
2.	Search for Slack Login.
3.	Click Continue with Google.
4.	Log in using your Google account.
5.	Create a workspace with the name:
Vvce
6.	Click Create.
7.	Skip the invitation and other optional setup steps.

8. Create a Slack channel
1.	Open your Slack workspace dashboard.
2.	Under Channels, click the + icon.
3.	Select Create a channel.
4.	Enter the channel name:
demo_exp9
5.	Select Public.
6.	Click Create.
7.	Skip adding members.
Slack workspace and channel created.

9. Add Jenkins application to Slack
1.	In Slack, click Agents and Tools or the three-dot menu, depending on the interface.
2.	Select Apps.
3.	Search for Jenkins.
4.	Select the Jenkins CI application.
5.	Click Add to Slack.
6.	It will open the Jenkins Slack application page in a new browser tab.
7.	Click Add to Slack again.
8.	Select the channel demo_exp9 from the channel dropdown.
9.	Click Add Jenkins CI integration. 
After authorization, you will get the Slack integration details.
•	Team Subdomain: Your Slack workspace subdomain (for example, vvce or the actual subdomain displayed). (vvce-r935744)
•	Bot User OAuth Token: The secret token generated for the Jenkins Slack application.
(rXJUzMSj4wg1rKShfVa9XXsH)

10. Configure Slack in Jenkins
1.	Open Jenkins Dashboard.
2.	Go to Settings → System
3.	Scroll down to the Slack section.
4.	Workspace: vvce-r935744
Credential:  Click on Add 
                      Select Global -> Secret text -> Next 
                                    Secret: rXJUzMSj4wg1rKShfVa9XXsH
                                    ID: ----
                                    Description: notifier
                       Click on create

Default channel: Type the channel name created (demo_exp9)

Select the description name in the credential drop down (notifier)

Click on test connection 
OUTPUT: success

Click on apply - > Save

5.	Open the Slack_Notifier -> Click on build -> Build success
Output: DevOps
               VVCE

and 

OUTPUT in slack :

Slack-Notifier
Build #1 completed successfully.
Started by user “username”
Job: Slack-Notifier
Status: SUCCESS


