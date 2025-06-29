# 🚀 Complete Roadmap: Running Your Advanced CI/CD Pipeline



## 1. **Project & GitHub Setup**

### a. **Prepare Your Project**
- Make sure your Java (Spring Boot/MVC) project has:
  - src directory (source code)
  - pom.xml (Maven build file)
  - ci-pipeline.yaml (the workflow file you posted)

### b. **Push to GitHub**
```sh
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

---

## 2. **Set Up SonarCloud for Static Code Analysis**

### a. **Create a SonarCloud Account & Project**
- Go to [https://sonarcloud.io/](https://sonarcloud.io/) and sign up (use GitHub login for easy integration).
- Click **"+ Create new project"** and link your GitHub repo.
- Note your **SonarCloud organization key** (e.g., `my-org`) and **project key** (usually your repo name).

### b. **Generate a SonarCloud Token**
- In SonarCloud, go to **My Account > Security**.
- Click **"Generate Tokens"**, name it, and copy the token.

### c. **Add SonarCloud Secrets to GitHub**
- Go to your GitHub repo: **Settings > Secrets and variables > Actions > New repository secret**
- Add:
  - `SONAR_TOKEN` = *(paste the token you copied)*
  - `SONAR_ORGANIZATION` = *(your SonarCloud org key, e.g., `my-org`)*

---

## 3. **Set Up JFrog Artifactory for Artifact Management**

### a. **Create a JFrog Account & Maven Repository**
- Sign up at [https://jfrog.com/start-free/](https://jfrog.com/start-free/)
- In the JFrog UI, go to **Administration > Repositories > Repositories > Create repository**
- Choose **Maven** (local), give it a name (e.g., `libs-release-local`), and save.

### b. **Get Your Artifactory Credentials**
- **ARTIFACTORY_URL**:  
  `https://<your-company>.jfrog.io/artifactory/<your-repo-name>`  
  *(e.g., `https://acme.jfrog.io/artifactory/libs-release-local`)*
- **ARTIFACTORY_USER**:  
  Your JFrog username (top right > User Profile)
- **ARTIFACTORY_PASSWORD**:  
  Your JFrog password or API key (generate in User Profile > API Key)

### c. **Add Artifactory Secrets to GitHub**
- In GitHub repo: **Settings > Secrets and variables > Actions > New repository secret**
- Add:
  - `ARTIFACTORY_URL`
  - `ARTIFACTORY_USER`
  - `ARTIFACTORY_PASSWORD`

---

## 4. **(Optional) Set Up Slack Notifications**

- In Slack, create an **Incoming Webhook** ([guide here](https://api.slack.com/messaging/webhooks)).
- Add the webhook URL as a secret:
  - `SLACK_WEBHOOK`

---

## 5. **Configure Your Workflow File**

- Your ci-pipeline.yaml should already include all the steps for:
  - Build, test, code coverage, SonarCloud scan, artifact upload, Artifactory upload, and Slack notification.

---

## 6. **How the Pipeline Works**

1. **On every push, PR, or schedule (Wed/Fri 5PM IST):**
   - Checks out code, sets up Java, caches Maven dependencies.
   - Builds the project and runs tests (publishes test reports even if tests fail).
   - Generates code coverage and uploads the report.
   - Runs SonarCloud static analysis (results in SonarCloud dashboard).
   - Uploads the JAR file as a GitHub Actions artifact and to JFrog Artifactory.
   - If any critical step fails, sends a Slack notification.

---

## 7. **How to View Results**

- **Test Reports:**  
  In the GitHub Actions run summary (look for "Maven Tests" check).
- **Code Coverage:**  
  Download from workflow artifacts or view in JaCoCo HTML report.
- **SonarCloud Analysis:**  
  Go to your project dashboard on [SonarCloud](https://sonarcloud.io/).
- **Artifacts in JFrog:**  
  Log in to your JFrog instance and browse to your repository.
- **Slack:**  
  Check your Slack channel for failure notifications.

---

## 8. **Deploying to EC2 (Bonus)**

### a. **Prepare Your EC2 Instance**
- Launch an EC2 instance (Amazon Linux/Ubuntu).
- Install Java and Maven.
- Set up SSH access (generate a key pair).

### b. **Add EC2 Secrets to GitHub**
- `EC2_HOST` = Public DNS or IP of your EC2 instance
- `EC2_USER` = Username (e.g., `ec2-user` or `ubuntu`)
- `EC2_KEY` = Private SSH key (add as a secret, **never commit to code**)

### c. **Add a Deploy Job to Your Workflow**
```yaml
  deploy-on-ec2:
    runs-on: ubuntu-latest
    needs: build-and-test
    steps:
    - name: Set up SSH key
      run: |
        mkdir -p ~/.ssh
        echo "${{ secrets.EC2_KEY }}" > ~/.ssh/id_rsa
        chmod 600 ~/.ssh/id_rsa
    - name: Deploy to EC2
      run: |
        ssh -o StrictHostKeyChecking=no ${{ secrets.EC2_USER }}@${{ secrets.EC2_HOST }} "
          pkill -f 'java -jar' || true
          rm -rf springboot-app &&
          git clone https://github.com/${{ github.repository }}.git springboot-app &&
          cd springboot-app &&
          mvn clean package -DskipTests &&
          nohup java -jar target/*.jar > app.log 2>&1 &
        "
```

---

## 9. **Summary Table: Secrets to Add**

| Secret Name         | Purpose/Value Example                                              |
|---------------------|--------------------------------------------------------------------|
| SONAR_TOKEN         | SonarCloud user token                                              |
| SONAR_ORGANIZATION  | SonarCloud org key                                                |
| ARTIFACTORY_URL     | https://yourcompany.jfrog.io/artifactory/libs-release-local        |
| ARTIFACTORY_USER    | JFrog username                                                    |
| ARTIFACTORY_PASSWORD| JFrog password or API key                                         |
| SLACK_WEBHOOK       | Slack webhook URL (optional)                                      |
| EC2_HOST            | EC2 public DNS or IP                                              |
| EC2_USER            | EC2 username (e.g., ec2-user, ubuntu)                             |
| EC2_KEY             | Private SSH key for EC2 access                                    |

---

## 10. **Final Checklist**

- [x] Project pushed to GitHub
- [x] SonarCloud project & token set up
- [x] JFrog repository & credentials set up
- [x] All secrets added to GitHub
- [x] Workflow file in ci-pipeline.yaml
- [x] (Optional) Slack webhook and EC2 secrets added

---

## 11. **Trigger the Pipeline**

- Push a commit or open a PR to `develop`, `feature-*`, or `release-*` branches.
- Or wait for the scheduled run (Wed/Fri 5PM IST).
- Watch the Actions tab for progress and results!

---

**You now have a complete, professional CI/CD pipeline with static analysis, artifact management, notifications, and deployment!**  