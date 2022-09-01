# DVC Architecture NLP pipeline AIOPs

## Reference Links :

[Reference repository](https://github.com/iterative/example-get-started)

[DVC Studio](https://studio.iterative.ai/)

[My DVC Studio](https://studio.iterative.ai/user/Jateendra/projects/DVC-NLP_Pipeline-AIOPs-zbmme52lxp)

### STEP 01- Create a repository by using template repository

### STEP 02- Clone the new repository

### STEP 03- Create a conda environment after opening the repository in VSCODE

```bash
conda create --prefix ./env python=3.7 -y
```

```bash
conda activate ./env
```
OR
```bash
source activate ./env
```

OR
```bash
conda create -n dvc-nlp python=3.7 -y
source activate dvc-nlp
```

### STEP 04- install the requirements
```bash
pip install -r requirements.txt
```

### STEP 05- initialize the dvc project
```bash
dvc init
```

If error copy : sqlite3.dll from loc:C:\Users\jatpradh\Anaconda3\DLLs to loc: C:\Users\jatpradh\Anaconda3\envs\dvc-ml\DLLs

```bash
dvc init -f
```
To see the pipeline configuration

```bash
dvc repro
```

### STEP 06- commit and push the changes to the remote repository

### *******************************************

### Special Commands

To ignore .logs files to be commited to github while comitting .
```bash
echo "*.logs" >> logs/.gitignore
```
To remove file from Github.
```bash
rm 'logs/running_logs.log'
```

### Working in DVC Studio :

[DVC Studio](https://studio.iterative.ai/)  [ Use github for login ]

    - Login in to DVC Studio 
    - Under section "Step Two - Import a repository" -> Add a project
    - Click on "Configure Git integrations settings"
    - Click on "Configure"
    - Select "Only select repositories" -> < Select the current working repository > -> Install & Authorize
    - Again Click on "Add a project" -> Skip & Continue 
    - Repository will be shown in the home page .

### At the end :

    - You can change params.yaml and do the changes to params.yaml as below :

        ```bash
        featurize:
            max_features: 2000
            ngrams: 3

        train:
            seed: 2001
            n_est: 100
            min_split: 16 
        ```
    - You can see the changes in the Plots and Compare in DVC Studio between 2 different commit branches .

        - Link  https://studio.iterative.ai/user/Jateendra/projects/DVC-NLP_Pipeline-AIOPs-zbmme52lxp?panels=plots%2C&commits=4328253%2Cprimary
        
### CI/CD Running :

    - Add a file : .github/workflows/ci-cd.yaml
    - << Write code for execution >>
    - Make sure below setting already done in github :
        repo_token: ${{ secrets.GITHUB_TOKEN }}
        If not set by : Profile -> setting -> Developer settings -> Github Apps -> Personal access tokens
    - commit the file : ci-cd.yaml
        Follow by : Repository -> Actions -> click link & see the status of execution .
    - You can see all the changes in DVC studio also : https://studio.iterative.ai/user/Jateendra/projects/DVC-NLP_Pipeline-AIOPs-zbmme52lxp?commits=4328285%2Cprimary
        You can do a lot of parameter changes in DVC studio and keep running the experiments.
        Which ever parameter suits best , you can choose that and merge with main branch .

### CICD Running via AWS :

ci-cd yaml :

   PERSONAL_ACCESS_TOKEN setting :
	
	- PERSONAL_ACCESS_TOKEN : Profile -> Settings -> Developer Setting -> Github Apps -> Personal access tokens -> Create a token with checkmark "workflow" .
	- Copy the code << copy the code >>
	- Goto the Repository -> Settings -> Secrets -> Actions -> New repository secret ->
		Name : PERSONAL_ACCESS_TOKEN
		Value : << paste the code >>

   AWS Setting :

	- Login to AWS ( mypython1.pradhan@gmail.com )

	- IAM -> Users -> Add Users -> aiops-pipeline-001 -> Check below :
		Access key - Programmatic access
		Password - AWS Management Console access

	- Custom password ( << Give a password >> ) -> Next: Permissions

	- Create a group "EC3-S3" , give permissions :
		AmazonEC2FullAccess
		AmazonS3FullAccess

	- Attach existing policies directly
		AmazonEC2FullAccess
        
	- Next Tag -> Next Review -> Create User -> << Will generate access key >>

      AWS_ACCESS_KEY_ID setting in Github :
	
	- Goto the Repository -> Settings -> Secrets -> Actions -> New repository secret ->
		Name : AWS_ACCESS_KEY_ID
		Value : << paste Access key ID >>

		Name : AWS_SECRET_ACCESS_KEY
		Value : << Secret access key >>

    If you push the changes to Github , then all the execution will run . 
