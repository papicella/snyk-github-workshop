<h1 align="center">Snyk GitHub Workshop</h1>

The following workshop is designed to show how Snyk integrates into SCM systems like GitHub and performs various application security scans, what fix/remediation advice is given to secure your applications during different stages of the SDLC, and how you can access them via different interfaces like the web UI, IDE and CLI.

## Prerequisites

* Free GitHub account - https://www.github.com
* Free Snyk account  - https://app.snyk.io 

## Agenda

We will cover the following topics, some live during today's session, and we'll let you explore the others on your own after the session.

<details>
  <summary>Live - Hands-On Session</summary>
  
- [ ] Setting up the SCM integration between GitHub and Snyk
- [ ] Importing a repo into Snyk and scanning in via the SCM integration
- [ ] Opening a PR to fix a Snyk Open Source vulnerability
- [ ] Running Snyk in Codespaces to check out the IDE experience 
    
</details>

<details>
  <summary>Live - Demo</summary>
  
- [ ] Detecting and suggesting fixes for transitive dependencies via the IDE
- [ ] [_Enterprise-only_] Fix Code issues in the IDE using DeepCode AI Fix
- [ ] Prioritization using Risk scores
- [ ] [_Enterprise-only_] Using `Reachability` as an additional parameter to determine risk
- [ ] [_Enterprise-only_] Reporting to provide visibility and facilitate collaboration between Security and Dev teams
- [ ] [_Enterprise-only_] Creating an inventory of code-based assets and setting up policies for security coverage
- [ ] [_Enterprise-only_] Run-time based risk factors to provide better risk assessment for prioritization
    
</details>

<details>
  <summary>Offline</summary>

- [ ] Set up the Snyk CLI
- [ ] Include Snyk scans in your CI/CD pipelines
- [ ] Integrate 3rd party tools like Nightfall AI, GitLeaks, and TruffleHog using GitHub Actions to detect secrets
    
</details>

<h1 align="center">Hands-on Workshop Steps</h1>

_Note: It is assumed you're using a Mac for these steps, but it should also work on Windows or Linux with some minor modifications_

<details>
<summary>Step 1 - Fork our sample repo into your own GitHub account</summary>

#### Sign in to your GitHub account

* Navigate to the following GitHub repo - https://github.com/boosef-snyk/JavaCoffeeShop
* Click on the "**Fork**" button
* Check the "**Owner**" field on the next page to ensure you are forking this repo to your personal GitHub account
* Click done

![](images/GH-workshop-1.png)

</details> 

<details>
<summary>Step 2 - Configure GitHub Integration</summary>

_NOTE: You may have already setup the GitHub integration on Snyk; in that case, go ahead and skip this step_

#### Login to https://app.snyk.io

* Sign up if you haven't already using your existing Google / GitHub / Bitbucket / Azure AD / Docker account
* Use the guided flow to set up the GitHub integration and grant Snyk access to all your public repos
* In Step 3 of the guided flow, you can select and import only the forked repo into Snyk 

![](images/GH-workshop-8.png)

* If you skipped the guided flow, navigate to Integrations -> Source Control -> GitHub

![](images/GH-workshop-5.png)

* Fill in your account credentials to connect your GitHub Account (if prompted).
* Now let's enable Code Scanning - you do that as follows:
  * Select Settings -> Snyk Code -> set "Enable Snyk Code" -> Save Changes

![](images/GH-workshop-3.png)

* Similarly, let's enable IaC Scanning - you do that as follows:
  * Select Settings -> Snyk IaC -> Enable "Detect Configuration files" -> Save Changes

![](images/GH-workshop-9.png)

</details> 

<details>
<summary>Step 2a - Import JavaCoffeeShop Application</summary>

#### Optional

_You can skip this if you followed the guided flow in the previous step._

* Now that Snyk is connected to your GitHub Account, import the repo into Snyk as a Project.
* Navigate to Projects menu option
* Click "**Add Project**" then select "**GitHub**"
* Click on the repo you forked
* The import should take about 3 minutes or so

![](images/GH-workshop-4-2.png)

</details>

<details>
<summary>Step 3 - Review SCM Integration Scan Results</summary>

* Once the import has completed, when you navigate to your Projects tab (from the sidebar), you should see something like this:

![](images/GH-workshop-4.png)

* Let's go ahead and click on pom.xml
* Here you will see all vulnerabilities including a dependency tree of where the vulnerabilities exist, with transitive dependencies also listed 

![](images/GH-workshop-6.png)

![](images/GH-workshop-7.png)

</details> 

<details>
<summary>Step 4 - Create a Pull Request to trigger a PR check</summary>

#### Navigate back to the list of Issues in the pom.xml

* Let's select an issue with a fix available (you should see a green button saying 'Fix this vulnerability')
* Search for "com.thoughtworks.xstream:xstream" and select the RCE vulnerability

![](images/GH-workshop-10.png)
  
* Click on the **Fix this vulnerability** button, and select the option to open a new PR on the next page (you'll need to scroll to the bottom of the page)
* This should take you to a new pull request that has been created in the JavaCoffeeShop repo

![](images/GH-workshop-12.png)

* Scroll to the bottom and you will see the `code/snyk`, `security/snyk`, and `license/snyk` checks running - congratulations, your SCM integration is working as expected!

![](images/GH-workshop-13.png)

* Once the tests complete running, you can click on the "**Details**" button next to them to view the scan report in the Snyk UI  

</details>

<details>
<summary>Step 5 - Find and fix issues in the IDE</summary> 

#### Switch to the Code section of your repository now 

* We are going to use Codespaces for this section of the workshop. Click on the green '**Code**' button and then '**Create codespace on main**"

![](images/GH-workshop-14.png)

* It will take anywhere between 2-5 minutes for the codespace to spin up and be fully set up. When you see the Snyk logo on the Extensions bar on the left, and status messages popping up on the right side of your screen, it is ready. You will be asked to grant **Workspace Trust**, click on OK. 

![](images/GH-workshop-15.png)

* While waiting, switch to your Snyk dashboard, first click on your name in the bottom left of the sidebar, and then '**Account Settings**'
* Under '**General Settings**' you should see a field under '**API Token**' - create your API key and copy it

![](images/GH-workshop-19.png)

* If your Codespace is now ready, open the Command Palette (same as in VS Code - Cmd + Shift + P on Mac; Ctrl + Shift + P on Windows) and type `Snyk`
* Click on "**Snyk: Set Token**" and paste the copied API key when prompted

![](images/GH-workshop-16.png)

* You'll see the Snyk extension expand on the left if authentication is successful

![](images/GH-workshop-17.png)

* Click the "**Rescan**" button in the Snyk extension panel to start the scans - moving forward, scans will run automatically whenever you save changes. If you see the extension panel refresh and populate with results like in the image below, congratultions, you have set Snyk up in the IDE successfully!

![](images/GH-workshop-18_new.png)

</details> 

<h1 align="center">Congratulations - Workshop Completed!!!</h1>

Thanks for attending and completing the live portion of this workshop. :) 

![](images/snyk-logo.png)

## Offline Tasks

Now that you have an idea of how Snyk works, and you have the basic setup completed, you can continue learning about Snyk on your own by trying out the following:

<details>
  <summary>Setting up Snyk in the IDE</summary>

  #### This will help you set up Snyk in an IDE of your choice

  * Instructions for installing the Snyk extension on your local IDE are available [here](https://docs.snyk.io/scm-ide-and-ci-cd-integrations/snyk-ide-plugins-and-extensions)
  * If you're using VS Code, the steps involved will be almost identical to what we did during the lab using Codespaces 
</details>

<details>
  <summary>Setting up the Snyk CLI</summary>

  #### This will help you set up Snyk on your local machine 

  * Follow the intructions [here](https://docs.snyk.io/snyk-cli/getting-started-with-the-snyk-cli#install-the-snyk-cli-and-authenticate-your-machine) to install the Snyk CLI on your machine, complete authentication, and run scans locally using the commands provided in the documentation 
</details>

<details>
  <summary>Including Snyk scans in your pipelines using GitHub Actions</summary>

  #### You can run all Snyk scans in your pipelines by first installing the CLI on your runner, and then running the same commands you previously used while using the CLI locally in the previous step
  
  * The repo you forked earlier has GitHub Actions workflows set up to run [Snyk Open Source](https://github.com/boosef-snyk/JavaCoffeeShop/blob/main/.github/workflows/snyk-os.yml) and [Snyk Code](https://github.com/boosef-snyk/JavaCoffeeShop/blob/main/.github/workflows/snyk-code.yml) scans as a part of your CI/CD pipelines.
    * By default, GitHub disables the GitHub Action workflows in forked repositories. To enable GitHub Actions in the repo, click the Actions tab of your forked repository and click "I understand my workflows, go ahead and enable them."
   
    ![image](https://github.com/user-attachments/assets/045b732b-0bcb-4840-bd31-210a90c5fa45)
  * If you use a different CI/CD tool, please refer to some of the sample files we have [here](https://github.com/snyk-labs/snyk-cicd-integration-examples/) 
  
</details>

<details>
  <summary>Integrating 3rd party tools with GitHub Actions to detect secrets</summary>
  <details>
    <summary>Nightfall AI</summary>

  #### Setting up a Nightfall AI account and integrating Secret Scanning in your pipelines
  
  * Sign up for a free Nightfall API account to get your API key [here](https://nightfall.ai/api)
  * The forked repo has Nightfall AI scans set up using GitHub Actions (yml [here](https://github.com/boosef-snyk/JavaCoffeeShop/blob/main/.github/workflows/nightfalldlp.yml)) - you can add commits / open PRs committing secrets to the main branch to test it out 
  * If you'd like to create your own policies / workflows, detailed setup instructions are available [here](https://github.com/nightfallai/nightfall_dlp_action?tab=readme-ov-file)
    
  </details>
  <details>
    <summary>GitLeaks</summary>

  #### Setting up GitLeaks and integrating Secret Scanning in your pipelines

  * Gitleaks is an open source project and you can set up scans without creating an account
  * The forked repo has Gitleaks scans set up using GitHub Actions (yml [here](https://github.com/boosef-snyk/JavaCoffeeShop/blob/main/.github/workflows/gitleaks.yml)) - you can add commits / open PRs committing secrets to the main branch to test it out 
  * If you'd like to create your own configuration, set up pre-commit hooks etc. detailed instructions are available [here](https://github.com/gitleaks/gitleaks)
    
  </details>
  <details>
    <summary>TruffleHog</summary>

  #### Setting up a TruffleHog account and integrating Secret Scanning in your pipelines
 
  * TruffleHog is an open source project and you can set up scans without creating an account; there is also an Enterprise offering 
  * The forked repo has TruffleHog scans set up using GitHub Actions (yml [here](https://github.com/boosef-snyk/JavaCoffeeShop/blob/main/.github/workflows/trufflehog.yml)) - you can add commits / open PRs committing secrets to the main branch to test it out 
  * If you'd like to create your own configuration, set up secret scanning for other assets like S3 buckets, Docker Images, Elasticsearch clusters etc. detailed instructions are available [here](https://github.com/trufflesecurity/trufflehog)
    
  </details>
</details>

## Additional Resources

  * Snyk Official Documentation: https://docs.snyk.io
  * Interactive Learning on Snyk Learn: https://learn.snyk.io/catalog/

<hr />

Pas Apicella [pas at snyk.io] is a Principal Solution Engineer APJ at Snyk <br />
Shilpa Raghunathan [shilpa.raghunathan at snyk.io] is a Staff Partner Solutions Engineer at Snyk <br />
Suganthi Krishnavathi [suganthi.krishnavathi at snyk.io] is a Staff Solutions Engineer at Snyk <br />
