# 🧠 Challenge Lab: Explore Generative AI with the Gemini API in Vertex AI

Welcome to the solution repository for the **Challenge Lab** from **Badge 5: Mastering the Gemini API with the Gen AI SDK**, part of the Google Cloud Generative AI learning path. This lab brings together advanced techniques in generative AI—including function calling, multimodal input processing, context caching, and batch prediction—using the Gemini model on Vertex AI.

---

## 🚀 Overview

This repository contains the hands-on implementations that complete the final challenge lab in Badge 5. It showcases how to:
- Integrate the Gemini SDK for Python.
- Work with both `gemini-pro` and `gemini-pro-vision` models.
- Perform function calling using Gemini’s tool capabilities.
- Analyze images and videos with multimodal prompts.
- Use context caching and batch prediction for efficiency.

---

## 🧱 Project Structure

📦gemini-challenge-lab
┣ 📁images/ # Screenshots or reference images (if any)
┣ 📁videos/ # Video assets used for multimodal testing
┣ 📜function_calling.py # Gemini function calling example
┣ 📜multimodal_prompt.py # Multimodal image and video analysis
┣ 📜batch_prediction.py # Efficient batch processing with Gemini
┣ 📜context_caching.py # Using context cache for optimized calls
┣ 📜requirements.txt # Python dependencies
┗ 📜README.md # You're here!


---

## 📌 Lab Objectives

1. **Implement Function Calling**
   - Define custom tools and pass them to Gemini to dynamically call based on user prompts.
2. **Leverage Multimodal Input**
   - Analyze images and videos alongside textual prompts using `gemini-pro-vision`.
3. **Optimize With Context Caching**
   - Cache context across multiple requests to reduce tokens and cost.
4. **Handle Batch Prediction**
   - Process multiple prompts efficiently using batch APIs and streaming responses.

---

## 🔧 Installation & Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/gemini-challenge-lab.git
   cd gemini-challenge-lab

2. **Set up your Python environment**
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt

3. **Authentication**
   - Ensure you have access to a Google Cloud project with Vertex AI enabled.
   - Set your environment:
   ``` bash
   PROJECT_ID = "your-gcp-project-id"
   LOCATION = "us-central1"

4. **Enable the Gemini SDK**
   - Use the official SDK to initialize:
   ``` bash
   client = genai.Client(vertexai=True, project=PROJECT_ID, location=LOCATION)

---

## 🔍 Examples

**✨ Function Calling with Gemini**

```bash
from vertexai.generative_models import FunctionDeclaration, Tool, GenerateContentConfig

get_destination = FunctionDeclaration(
    name="get_destination",
    description="Get the destination that the user wants to go to",
    parameters={"type": "OBJECT", "properties": {
        "destination": {"type": "STRING", "description": "Destination the user wants to go to"}
    }},
)

destination_tool = Tool(function_declarations=[get_destination])

response = client.models.generate_content(
    model=MODEL_ID,
    contents="I want to go to Tokyo!",
    config=GenerateContentConfig(tools=[destination_tool], temperature=0.3),
)

print(response.candidates[0].content.parts[0].function_call)
```

**📸 Multimodal Prompt (Image Input)**

``` bash
from PIL import Image
import requests

image = Image.open(requests.get("https://storage.googleapis.com/cloud-samples-data/generative-ai/image/meal.png", stream=True).raw)

response = client.models.generate_content(
    model=MODEL_ID,
    contents=[image, "Write a short and engaging blog post based on this picture."]
)

print(response.text)
```

**🎥 Multimodal Prompt (Video Input)**

``` bash
from vertexai.generative_models import Part

prompt = """
What is shown in this video?
Where should I go to see it?
What are the top 5 places in the world that look like this?
"""

video = Part.from_uri(
    file_uri="gs://github-repo/img/gemini/multimodality_usecases_overview/mediterraneansea.mp4",
    mime_type="video/mp4",
)

contents = [prompt, video]

responses = client.models.generate_content_stream(model=MODEL_ID, contents=contents)

for response in responses:
    print(response.text, end="")
```

---

## 🧠 Learnings & Takeaways

- Gemini SDK offers a powerful abstraction over multimodal and functional LLM applications.
- Multimodal input enables next-level user experiences—understanding visuals alongside text.
- Function calling transforms LLMs from chatbots into dynamic AI agents that act.
- Context caching and batch prediction optimize model usage and make workflows production-ready.

---

## 👤 Author

**Sanjana Nathani**
AI & Data Science Enthusiast | Engineer | Educator | Builder
🔗 Connect on LinkedIn : https://www.linkedin.com/in/sanjana-nathani-26a42727b/

---

## 📄 License

This project is licensed under the MIT License. See the LICENSE file for details.

## 🙌 Contributing

Contributions, ideas, and improvements are always welcome! If this project helped you, consider giving it a ⭐ and sharing it with fellow learners.

## "Stay curious. Stay driven." 💡🔥
