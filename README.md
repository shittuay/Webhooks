# Webhooks
# Configuring a Webhook for GitHub on Jenkins

## Prerequisites:
1. **Jenkins Setup**: Ensure Jenkins is installed and running.
2. **GitHub Repository**: You have access to the GitHub repository you want to integrate with Jenkins.
3. **Jenkins GitHub Plugin**: Make sure the GitHub plugin is installed in Jenkins. You can check this in Jenkins under **Manage Jenkins > Manage Plugins > Installed**.

## Step-by-Step Configuration:

### 1. Create a Jenkins Job for the GitHub Repository
   - Open your Jenkins instance in a web browser.
   - Click on **New Item** or **New Job**.
   - Enter a name for your job.
   - Select **Freestyle project** or **Pipeline** depending on your requirements.
   - Click **OK** to create the job.

### 2. Configure the Jenkins Job
   - Inside the job configuration:
     - **Source Code Management**: Select **Git**.
       - Enter the **Repository URL**. For example, `https://github.com/username/repo.git`.
       - If necessary, add credentials for accessing the repository.
     - **Build Triggers**: Check **GitHub hook trigger for GITScm polling**.

### 3. Generate Jenkins GitHub Webhook URL
   - Go to **Manage Jenkins > Configure System**.
   - Under **GitHub** section, click **Add GitHub Server**.
     - Give it a name (e.g., `GitHub`).
     - Add credentials (GitHub personal access token).
     - Click **Test connection** to verify the setup.
   - Make note of the **Jenkins URL**. This will be used to configure the webhook in GitHub.

### 4. Set Up the Webhook in GitHub
   - Go to your GitHub repository.
   - Click on **Settings**.
   - From the sidebar, select **Webhooks**.
   - Click on **Add webhook**.
     - **Payload URL**: Enter your Jenkins URL followed by `/github-webhook/`. For example, `http://your-jenkins-url/github-webhook/`.
     - **Content type**: Select `application/json`.
     - **Secret**: You can optionally add a secret to secure the webhook.
     - **Which events would you like to trigger this webhook?**: Select **Just the push event.** or other events depending on your needs.
   - Click **Add webhook**.

### 5. Test the Webhook
   - Make a commit or perform an action in GitHub that should trigger the webhook.
   - Go to your Jenkins job and check the build history to see if a new build has been triggered by the webhook.

## Example Configuration:

Here's a simple example of how your Jenkins job configuration might look:

### Jenkins Job Configuration:
- **Source Code Management**:
  - Git Repository URL: `https://github.com/username/repo.git`
- **Build Triggers**:
  - GitHub hook trigger for GITScm polling
- **Build**:
  - Add your build steps, e.g., Execute Shell, Invoke Gradle Script, etc.

## Troubleshooting:
- **Webhook Delivery**: Check the webhook delivery status in GitHub under **Settings > Webhooks > Recent Deliveries**. This will show if GitHub is successfully sending the payload to Jenkins.
- **Jenkins Logs**: Check the Jenkins logs for any errors related to webhook processing under **Manage Jenkins > System Log**.

This setup ensures that every time there is a push or other specified events in your GitHub repository, a build is triggered in Jenkins through the configured webhook.
