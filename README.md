# ai-based-app
AI generative app


To use the `structured_generator` function from your `helpers` module in another script, you need to ensure that the script has access to the `helpers` module and that the `structured_generator` function is imported correctly. Here's how you can do it:

Assuming your directory structure is something like this:

```
project/
│
├── app.py
├── helpers.py
└── your_script.py
```

1. **helpers.py:**
   Make sure the `structured_generator` function is defined in `helpers.py`.

   ```python
   # Filename: helpers.py

   from openai import OpenAI
   import os
   from dotenv import load_dotenv

   load_dotenv()

   openai_api_key = os.getenv("OPENAI_API_KEY")

   open_ai_client = OpenAI(api_key=openai_api_key)

   def structured_generator(openai_model, prompt, custom_model):
       result: custom_model = open_ai_client.chat.completions.create(
           model=openai_model,
           response_model=custom_model,
           messages=[{"role": "user", "content": f"{prompt}, output must be in json"}]
       )
       return result
   ```

2. **your_script.py:**
   In your script where you want to use `structured_generator`, import it from `helpers`.

   ```python
   # Filename: your_script.py

   from helpers import structured_generator
   from your_custom_model import YourCustomModel  # Make sure to replace with your actual model

   openai_model = "gpt-3.5-turbo"
   prompt = "Your prompt here"

   result = structured_generator(openai_model, prompt, YourCustomModel)
   print(result)
   ```

3. **Installing Dependencies:**
   Ensure that you have the required dependencies installed in your environment. If you haven't installed the `openai` library and other dependencies, you need to do so:

   ```bash
   pip install openai python-dotenv
   ```

Make sure that your `helpers.py` and `your_script.py` are in the same directory or in a structure where Python can find them. If they are in different directories, you might need to adjust your Python path or use relative imports.
