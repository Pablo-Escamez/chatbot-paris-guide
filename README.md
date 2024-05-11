# Parisian Expert Chatbot

This Python script utilizes the OpenAI API to create a chatbot that serves as a virtual Parisian expert. It responds intelligently to a set of common questions related to Parisian landmarks and attractions, providing valuable insights for travel planning purposes. The chatbot enhances the travel planning experience by delivering engaging and immersive responses to users' inquiries.

## Usage

1. **Installation**: Before running the script, ensure you have the necessary dependencies installed. You can install them using pip:

    ```bash
    pip install openai
    ```

2. **API Key**: Set up your OpenAI API key as an environment variable named `OPENAI`. You can obtain your API key from the OpenAI website.

3. **Start your code here!**: Insert your Python code into the provided script template. This code initializes the OpenAI client, defines the conversation structure, and queries the chatbot with user questions.

4. **Customize Conversation**: You can customize the conversation by modifying the `user_qs` list. Add or remove questions according to your requirements.

5. **Run the Script**: Execute the script to interact with the Parisian expert chatbot. It will provide responses to the user's questions based on the trained GPT-3.5 model.

## Example Conversation

```python
import os
from openai import OpenAI

# Define the model to use
model = "gpt-3.5-turbo"

# Define the client
client = OpenAI(api_key=os.environ["OPENAI"])
conversation = [{"role": "system", "content": "You are a virtual Parisian expert, delivering valuable insights into the city's iconic landmarks and hidden treasures. You will respond intelligently to a set of common questions, providing a more engaging and immersive travel planning experience for the clientele of Peterman Reality Tours." }]

user_qs = [
    "How far away is the Louvre from the Eiffel Tower (in miles) if you are driving?",
    "Where is the Arc de Triomphe?",
    "What are the must-see artworks at the Louvre Museum?"
]

for q in user_qs:
    print("User:", q)
    user_dict = {"role": "user", "content": q}
    conversation.append(user_dict)

    response = client.chat.completions.create(
        model="gpt-3.5-turbo",
        messages=conversation,
        temperature=0.0,
        max_tokens=100
    )

    assistant_dict = {"role": "assistant", "content": response.choices[0].message.content}
    conversation.append(assistant_dict)

    print("Assistant:", response.choices[0].message.content, "\n")
