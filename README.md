<h2> <a href="https://github.com/ShubhPatil95/DVC-02-Data_Versioning"> 02 - DVC Data File Versioning </a></h2>

<p>
<strong> Here in this tutorial we will see how we can keep track of data file which changes over time and how can we restore the data file of particuler commits</strong>
  
### Step1
* Create a main folder named DVC-02-Data_Versioning and 2 subfolder under it named DataFileVersioning and DVCRemote. Then move into 02-DVC_Data_Versioning
```ruby
mkdir DVC-02-Data_Versioning
cd DVC-02-Data_Versioning
mkdir DataFileVersioning DVCRemote
cd DataFileVersioning
```
### Step2  
* Now you are into DataFileVersioning folder, hence intiate the git and dvc 
```ruby
git init
dvc init
```
### Step3  
* Create dummy data file under name data.txt and write sentence "This is first commit"
```ruby
nano data.txt
```  
### Step4  
* Add dvc remote, here we will use remote folder as DVCRemote however you can use either local or cloud storage like google drive, s3bucket etc. Make sure you putting your absolute path of DVCRemote folder instead of mine /usr/home/DVCRemote. After running below command you can go to DVCRemote folder and see what exactly udpated over there.
```ruby
dvc remote add -d My_Local_Remote /home/shubham/tutorial/DVC-02-Data_Versioning/DVCRemote 
```   
### Step5
* Add data.txt file into dvc, this will create data.txt.dvc file which contains the information about data.txt
```ruby
dvc add data.txt
git add .
git commit -m "First Commit"
dvc push
```  
### Step6
* Now edit the data.txt file and write the sentence "This is second commit". Further add edited data.txt to DVC and commit/push the changes to git and dvc.
```ruby
nano data.txt
dvc add data.txt
git add .
git commit -m "Second Commit"
dvc push
```  
### Step7
* Again edit the data.txt file and write the sentence "This is third commit". Further add edited data.txt to DVC and commit/push the changes to git and dvc.
```ruby
nano data.txt
dvc add data.txt
git add .
git commit -m "Third Commit"
dvc push
```  
### Step8
* Finally create a github repository named DVC-02-Data_Versioning and push the commits into it.
```ruby
git remote add origin https://github.com/ShubhPatil95/DVC-02-Data_Versioning.git
git branch -M main
git push -u origin main
```  
### Step9
* Now what if you want to go to first commit where your data.txt containing sentence "This is first commit". Just find the commit id(SHA ID) of first commit using git log --oneline and checkout to that one
```ruby
git log --oneline  ## copy the commit id of first commit, mine is f7d5a7e
git checkout f7d5a7e  ## make sure to paste your commit Id of first commit
cat data.txt  ## You can see even thoough you checkout to first commit,but data.txt is file is not yet udpated
dvc checkout  ## this command will update the data.txt file
cat data.txt  ## you can see data.txt is updated with "This is firstcommit"
```     
### Step10
* Now, Just go back to third commit.
```ruby
git checkout main
dvc checkout
cat data.txt  ## see test.txt is udpated with "This is third commit"
```    
### Step11
* Now what if you want to again go back to second commit where your data.txt containing sentence "This is second commit". Just find the commit id(SHA ID) of second commit using git log --oneline and checkout to that one
```ruby
git log --oneline  ## copy the commit id of second commit, mine is befab47
git checkout befab47  ## make sure to paste your commit Id of second commit
cat data.txt  ## You can see even thoough you checkout to second commit,but data.txt is file is still showing third commit file
dvc checkout  ## this command will update the data.txt file
cat data.txt  ## you can see data.txt is updated with "This is second commit"
```         
</p>
</details> 
