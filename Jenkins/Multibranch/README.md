# Jenkins Multibranch Pipeline - Lab Guide

## 📌 Prerequisites
- Jenkins installed and running
- GitHub (or GitLab/Bitbucket) repository with a `Jenkinsfile`
- Required plugins:
  - **Pipeline**
  - **Git plugin**
  - **GitHub Branch Source Plugin**
  - **Bitbucket Branch Source Plugin** (if using Bitbucket)

## 📝 Step 1: Prepare the Git Repository
1. **Create a new repository** on GitHub/GitLab/Bitbucket.
2. Add a `Jenkinsfile` in the root directory:

   ```groovy
   pipeline {
       agent any
       stages {
           stage('Build') {
               steps {
                   echo 'Building...'
               }
           }
           stage('Test') {
               steps {
                   echo 'Testing...'
               }
           }
           stage('Deploy') {
               steps {
                   echo 'Deploying...'
               }
           }
       }
   }
   ```
3. Commit and push the changes.

## 🖥 Step 2: Configure Multibranch Pipeline in Jenkins
1. **Login to Jenkins** and go to **New Item**.
2. Select **Multibranch Pipeline** and enter a name.
3. Click **OK**.

## ⚙️ Step 3: Configure Source Code Management
1. In the **Branch Sources** section:
   - Click **Add source** → Select **Git** (or GitHub).
   - Enter the **repository URL** (e.g., `https://github.com/yourusername/yourrepo.git`).
   - If using GitHub, click **Add** → Add your credentials (Personal Access Token).
2. Click **Save**.

## 🚀 Step 4: Run the Pipeline
1. Go to **Dashboard > Your Multibranch Pipeline Job**.
2. Click **Scan Multibranch Pipeline Now** (detects branches automatically).
3. Jenkins will scan the repository and create jobs for branches containing a `Jenkinsfile`.
4. Click on any branch and **Build Now**.

## 🔎 Step 5: View the Pipeline Execution
1. Click on a branch → **Build History**.
2. Click on a build number and select **Console Output** to view logs.

## ✅ Step 6: Automate with Webhooks (Optional)
1. Go to your GitHub repository → **Settings** → **Webhooks**.
2. Click **Add Webhook**:
   - **Payload URL**: `http://your-jenkins-server/github-webhook/`
   - **Content Type**: `application/json`
   - **Events**: Select `Push` event.
3. Click **Save**.

Now, any new commit will trigger an automatic build!

## 🎯 Summary
✔ **Created a Git repository with a Jenkinsfile**  
✔ **Configured Jenkins Multibranch Pipeline**  
✔ **Scanned branches and triggered builds**  
✔ **(Optional) Set up webhooks for auto-triggering**  

This is a **basic lab setup**. You can extend it by adding **unit tests, Docker builds, deployment steps, and notifications**.

Let me know if you need additional configurations! 🚀