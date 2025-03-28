---

# AI-Powered Resume & Cover Letter Generator

![Python](https://img.shields.io/badge/Python-3.8%2B-blue) ![LangGraph](https://img.shields.io/badge/LangGraph-0.1.0-green) ![AWS](https://img.shields.io/badge/AWS-S3%20%26%20Lambda-orange) ![License](https://img.shields.io/badge/License-MIT-yellow)

Welcome to the **AI-Powered Resume & Cover Letter Generator**! This project leverages **LangGraph** and an LLM (e.g., Grok from xAI) to create tailored resumes and cover letters based on job descriptions. It’s a multi-agent workflow that analyzes job requirements, optimizes your resume, crafts a compelling cover letter, and ensures a polished final output—all with optional AWS integration for storage and deployment.

## Features
- **Job Analysis Agent**: Extracts key skills, qualifications, and keywords from job descriptions.
- **Resume Optimization Agent**: Enhances your resume to align with job requirements.
- **Cover Letter Agent**: Generates a personalized, professional cover letter.
- **Final Review Agent**: Ensures consistency and readability.
- **AWS Integration**: Store outputs in S3 and deploy via Lambda for scalability.
- **Output**: Text files (with optional PDF conversion).

## Demo
Here’s a sample workflow:
1. Input: "XYZ Tech Solutions is seeking a Machine Learning Engineer to design, develop, and deploy cutting-edge AI models..."
2. Output: A tailored resume and cover letter, saved to AWS S3.

Check the [examples](#usage) section for more!

## Prerequisites
- Python 3.8+
- Git
- An API key for an LLM (e.g., Groq, OpenAI)
- AWS account (optional, for S3/Lambda integration)

## Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/resume-cover-letter-agent.git
cd resume-cover-letter-agent
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```
Requirements file (`requirements.txt`):
```
langchain-groq
langgraph
boto3
reportlab  # Optional, for PDF export
```

### 3. Configure Environment Variables
Create a `.env` file in the root directory:
```
GROQ_API_KEY=your_grok_api_key_here
AWS_ACCESS_KEY_ID=your_aws_access_key  # Optional
AWS_SECRET_ACCESS_KEY=your_aws_secret_key  # Optional
```

### 4. (Optional) Set Up AWS
- **S3**: Create a bucket (e.g., `resume-generator-output`) and update `config.py` with your bucket name.
- **Lambda**: Follow the [AWS Lambda Setup](#aws-lambda-deployment) section.

## Usage

### Running Locally
1. Open `main.py` and update the `job_description` variable with your target job description.
2. Run the script:
```bash
python main.py
```
3. Check the console for outputs or `output/` folder for saved files.

**Example**:
```python
job_description = "XYZ Tech Solutions is seeking a Machine Learning Engineer to design, develop, and deploy cutting-edge AI models..."
result = graph.invoke({"job_description": job_description})
print(result["optimized_resume"])
print(result["cover_letter"])
```

### Sample Output
- **Resume**: A Markdown-formatted resume with tailored skills and experience.
- **Cover Letter**: A professional letter addressing the job’s key points.

## AWS Integration

### AWS S3: Storing Outputs
1. Configure your S3 bucket in `config.py`:
```python
S3_BUCKET = "resume-generator-output"
```
2. The script automatically uploads `resume.txt` and `cover_letter.txt` to S3 after the final review.

### AWS Lambda: Serverless Deployment
1. **Prepare Lambda Package**:
   - Install dependencies in a folder:
     ```bash
     pip install langchain-groq langgraph boto3 -t lambda_package
     ```
   - Copy `lambda_function.py` into `lambda_package`.
   - Zip the folder: `zip -r lambda_function.zip lambda_package`.

2. **Create Lambda Function**:
   - In AWS Console, create a Lambda function (Python 3.9+).
   - Upload `lambda_function.zip`.
   - Set environment variables (e.g., `GROQ_API_KEY`).

3. **Add API Gateway**:
   - Create a `POST` endpoint (e.g., `/generate`) and link it to Lambda.
   - Test with a payload:
     ```json
     {"job_description": "XYZ Tech Solutions is seeking a Machine Learning Engineer..."}
     ```

4. **Response**: JSON with resume and cover letter, plus files saved to S3.

## Project Structure
```
resume-cover-letter-agent/
├── main.py              # Main script to run the agent
├── lambda_function.py   # AWS Lambda handler
├── config.py            # Configuration (e.g., S3 bucket)
├── output/              # Local output folder
├── requirements.txt     # Dependencies
└── README.md            # This file
```

## Extending the Project
- **Add a UI**: Integrate Gradio or Streamlit for a web interface.
- **User Resumes**: Allow users to upload existing resumes for optimization.
- **PDF Export**: Enable `reportlab` in `main.py` for PDF outputs.

## Contributing
Contributions are welcome! Here’s how:
1. Fork the repo.
2. Create a feature branch (`git checkout -b feature/your-feature`).
3. Commit changes (`git commit -m "Add your feature"`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Open a Pull Request.

Please follow the [Code of Conduct](CODE_OF_CONDUCT.md) and report issues via [Issues](https://github.com/yourusername/resume-cover-letter-agent/issues).

## License
This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

## Acknowledgments
- Built with [LangGraph](https://github.com/langchain-ai/langgraph) and [LangChain](https://github.com/langchain-ai/langchain).
- Powered by [Grok](https://xai.ai) from xAI.
- Inspired by job seekers everywhere!

---

## Next Steps
1. Replace `yourusername` in the GitHub URLs with your actual GitHub username.
2. Create the repo:
   ```bash
   git init
   git add .
   git commit -m "Initial commit: AI Resume & Cover Letter Generator"
   git remote add origin https://github.com/yourusername/resume-cover-letter-agent.git
   git push -u origin main
   ```
3. Add additional files (`main.py`, `lambda_function.py`, etc.) based on the tutorial code I provided earlier.
4. Test the README by viewing it in GitHub to ensure formatting looks good.

Let me know if you need help with specific files (e.g., `main.py`) or pushing to GitHub!
