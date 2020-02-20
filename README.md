# aws-slack-demo-2
demo for multi-stage deployment
# please follow the following instructions to set-up multi-stage devops pipeline
# Step 1: Slack Set-up
a. Go to api.slack.com/apps
b. Select Create New App
c. Specify app name & and select development workspace name
d. Create a new Channel in slack
e. Create a incoming webhook url
f. Specify the channel name for the webhook
g. Your codepipeline will communicate with slack through this webhook url
h. Use verification token, and slack approvers as input parameters to production CICD stack (Step 3)
i. Store the slack webhook url in SSM parameter store and do a dynamic retrieval in CFN
j. Enable interactive components for your slack app. Enter the interactive message url – this was created when the production codepipeline stack was created
# Step 2: create the CICD pipeline stack for staging account
a. make sure parameters-stg.json has the right parameter values for the staging account
# Step 3: create the CICD pipeline stack for the production account
a. make sure parameters-prd.json has the right parameter values for the staging account
b. for StageAccountId, use the account number for staging account
c. for StageLambdaRole, get the value from the output section of the staging CICD stack
d. add the slack webhook url (from step 1.e) to parameter store, and use that as the dynamic reference in the cfn template
d. use the interactive message url from the output section in step 1.j
# Step 4: update the staging account CICD stack
a. from the output of the production stack, use OutputBucketName as the value for the parameter: ProdBucketName
# Step 5: update github repo with SSH key and webhook URL
a. add the generated SSH key (from the output of the staging CICD stack)
b. add the webhook url (from the output of the staging CICD stack)

