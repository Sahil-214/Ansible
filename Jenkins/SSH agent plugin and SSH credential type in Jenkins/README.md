# Lab Guide: Using SSH Agent Plugin in a Jenkins Freestyle Job

This guide explains how to configure the SSH Agent Plugin along with an SSH credential (of type "SSH Username with private key") in a Jenkins freestyle job. Follow the steps below to enable your job to run SSH (or SCP) commands on a remote host.

---

## Prerequisites

- **Jenkins Instance:** A running Jenkins server.
- **Permissions:** Administrative rights to install plugins and manage credentials.
- **Remote Host:** A remote SSH-enabled host (e.g., a Linux server).
- **SSH Key Pair:** A generated SSH key pair (e.g., using `ssh-keygen`).

---

## Step 1: Install the SSH Agent Plugin

1. In your Jenkins dashboard, navigate to **Manage Jenkins** → **Manage Plugins**.
2. Under the **Available** tab, search for **SSH Agent Plugin**.
3. Select the plugin and click **Install without restart** (or **Download now and install after restart**).
4. Restart Jenkins if prompted.

_Source: :contentReference[oaicite:0]{index=0}_

---

## Step 2: Add SSH Credentials

1. From the Jenkins dashboard, go to **Manage Jenkins** → **Manage Credentials**.
2. Choose the appropriate domain (for example, **Global credentials (unrestricted)**), then click **Add Credentials**.
3. Configure the credential with the following details:
   - **Kind:** SSH Username with private key
   - **Username:** *(e.g., `jenkins` or your remote login name)*
   - **Private Key:** Select "Enter directly" and paste the contents of your private key (e.g., from `~/.ssh/id_rsa`).
   - **Passphrase:** *(If your key is passphrase-protected)*
   - **ID:** Provide a recognizable ID (e.g., `my-ssh-key`).
   - **Description:** *(Optional, e.g., "SSH credentials for remote deployment")*
4. Click **OK** to save the credential.

_Source: :contentReference[oaicite:1]{index=1}_

---

## Step 3: Create a Jenkins Freestyle Job

1. From the Jenkins dashboard, click **New Item**.
2. Enter a name for your job (e.g., `SSH Agent Lab`) and select **Freestyle project**.
3. Click **OK**.

---

## Step 4: Configure the Job to Use the SSH Agent Plugin

1. In the job configuration page, scroll down to the **Build Environment** section.
2. Check the option **SSH Agent**.
3. From the drop-down list, select the SSH credential you created (e.g., `my-ssh-key`).

This configuration will ensure that the SSH key is loaded into an SSH agent during the build.

---

## Step 5: Add a Build Step to Execute an SSH Command

1. In the **Build** section, click **Add build step** and select **Execute shell**.
2. Enter a command that uses SSH. For example:

    ```bash
    # Optionally disable strict host key checking (for lab/testing purposes)
    ssh -o StrictHostKeyChecking=no user@remote_host "ls -l /path/to/directory"
    ```

    Replace `user@remote_host` with the actual username and hostname/IP of your remote server.
3. Click **Save** to update your job configuration.

---

## Step 6: Run and Verify the Job

1. Click **Build Now** to trigger the job.
2. Open the **Console Output** for the build.
3. Verify that the SSH command executes successfully (e.g., you see a directory listing from the remote host).

---

## Troubleshooting Tips

- **Host Key Verification:**  
  The first SSH connection may prompt for host key verification. In this lab guide, the command uses `-o StrictHostKeyChecking=no` to bypass this prompt. For production environments, manually add the remote host’s key to the `known_hosts` file on the build node.
  
- **SSH Agent Availability:**  
  Ensure that the `ssh-agent` executable is installed on the build node (or controller) where the job is executed.
  
- **Credential Accuracy:**  
  Double-check that the SSH username and private key match the expected values on the remote host.

---

## Additional Resources

- [SSH Agent Plugin Documentation](https://plugins.jenkins.io/ssh-agent/) :contentReference[oaicite:2]{index=2}
- [Managing SSH Credentials - CloudBees Documentation](https://docs.cloudbees.com/docs/cloudbees-ci/latest/cloud-admin-guide/ssh) :contentReference[oaicite:3]{index=3}
- [Stack Overflow: Use SSH credentials in Jenkins Pipeline](https://stackoverflow.com/questions/44377238/use-ssh-credentials-in-jenkins-pipeline-with-ssh-scp-or-sftp) :contentReference[oaicite:4]{index=4}

---

This guide should help you set up and verify a Jenkins freestyle job that uses the SSH Agent Plugin to securely run SSH commands on a remote host.
