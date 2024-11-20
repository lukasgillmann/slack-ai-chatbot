# ChatGPT in Slack

Introducing a transformative app for Slack users, specifically designed to enhance your communication with ChatGPT! This app enables seamless interaction with ChatGPT via Slack channels, optimizing your planning and writing processes by leveraging AI technology.


## Running the App on Your Local Machine

To run this app on your local machine, you only need to follow these simple steps:

* Create a new Slack app using the manifest-dev.yml file
* Install the app into your Slack workspace
* Retrieve your OpenAI API key at https://platform.openai.com/account/api-keys
* Start the app

```bash
# Create an app-level token with connections:write scope
export SLACK_APP_TOKEN=xapp-1-...
# Install the app into your workspace to grab this token
export SLACK_BOT_TOKEN=xoxb-...
# Visit https://platform.openai.com/account/api-keys for this token
export OPENAI_API_KEY=sk-...

# Optional: gpt-3.5-turbo and newer ones are currently supported (default: gpt-3.5-turbo)
export OPENAI_MODEL=gpt-4o
# Optional: Model temperature between 0 and 2 (default: 1.0)
export OPENAI_TEMPERATURE=1
# Optional: You can adjust the timeout seconds for OpenAI calls (default: 30)
export OPENAI_TIMEOUT_SECONDS=60
# Optional: You can include priming instructions for ChatGPT to fine tune the bot purpose
export OPENAI_SYSTEM_TEXT="You proofread text. When you receive a message, you will check
for mistakes and make suggestion to improve the language of the given text"
# Optional: When the string is "true", this app translates ChatGPT prompts into a user's preferred language (default: true)
export USE_SLACK_LANGUAGE=true
# Optional: Adjust the app's logging level (default: DEBUG)
export SLACK_APP_LOG_LEVEL=INFO
# Optional: When the string is "true", translate between OpenAI markdown and Slack mrkdwn format (default: false)
export TRANSLATE_MARKDOWN=true
# Optional: When the string is "true", perform some basic redaction on prompts sent to OpenAI (default: false)
export REDACTION_ENABLED=true
# Optional: When the string is "true", this app shares image files with OpenAI (default: false)
export IMAGE_FILE_ACCESS_ENABLED=true

# To use Azure OpenAI, set the following optional environment variables according to your environment
# default: None
export OPENAI_API_TYPE=azure
# default: https://api.openai.com/v1
export OPENAI_API_BASE=https://YOUR_RESOURCE_NAME.openai.azure.com
# default: None
export OPENAI_API_VERSION=2023-05-15
# default: None
export OPENAI_DEPLOYMENT_ID=YOUR-DEPLOYMENT-ID

# Experimental: You can try out the Function Calling feature (default: None)
export OPENAI_FUNCTION_CALL_MODULE_NAME=tests.function_call_example

python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python main.py
```

## Running the App for Company Workspaces

Confidentiality of information is top priority for businesses.

This app is open-sourced! so please feel free to fork it and deploy the app onto the infrastructure that you manage.
After going through the above local development process, you can deploy the app using `Dockerfile`, which is placed at the root directory.

The `Dockerfile` is designed to establish a WebSocket connection with Slack via Socket Mode.
This means that there's no need to provide a public URL for communication with Slack.

