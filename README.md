# n8n Workflow: AI-Powered YouTube Video Summarizer & Analyzer

Instantly transform YouTube videos into comprehensive summaries and structured analyses with this n8n workflow. Automatically extract, process, and analyze video transcripts using AI (GPT-4o-mini) to deliver clear, organized insights without the need to watch the entire video.

Save hours of viewing time while quickly grasping key concepts, arguments, and information presented in video content.

## 🚀 Key Features & Benefits

*   **Instant Summaries:** Provide a YouTube URL and get a structured summary and analysis within seconds.
*   **AI-Driven Insights:** Leverages OpenAI's GPT-4o-mini to intelligently analyze transcript content.
*   **Structured Output:** Organizes information hierarchically with main topics and essential points using clear markdown formatting.
*   **Automated Transcript Extraction:** Automatically fetches the full transcript for supported public YouTube videos.
*   **Flexible URL Handling:** Designed to work with various standard YouTube video URL formats.
*   **Time Efficiency:** Massively reduces time spent on video consumption for research, learning, or analysis.
*   **Optional Notifications:** Includes an optional Telegram notification step to alert you when processing is complete.

## 🧠 Smart Processing Pipeline

1.  **URL Input:** The workflow receives a YouTube video URL via a Webhook trigger.
2.  **Video Details & Transcript:** It interacts with YouTube (potentially via API or dedicated nodes) to fetch video details and extract the full text transcript.
3.  **AI Analysis (GPT-4o-mini):** The extracted transcript is sent to the OpenAI GPT-4o-mini model with a carefully crafted prompt instructing it to:
    *   Identify main topics discussed in the video.
    *   Extract key concepts, arguments, and essential points for each topic.
    *   Structure the analysis logically (e.g., using headings and bullet points).
    *   Maintain technical accuracy while enhancing clarity.
4.  **Formatted Output:** The AI generates a structured summary formatted in Markdown.
5.  **(Optional) Notification:** A message containing the summary (or a link/confirmation) is sent via Telegram.

## Ideal For

*   **📚 Researchers & Students:** Quickly digest lectures, educational videos, and research presentations without full viewing.
*   **💼 Business Professionals:** Efficiently analyze industry talks, competitor presentations, webinars, and training materials.
*   **🎯 Content Creators:** Speed up research, analyze competitor content, and identify key themes within a niche.
*   **🧑‍💻 Anyone Overwhelmed by Video Content:** Get the essence of videos quickly when time is limited.

## Prerequisites

*   **An n8n instance:** Self-hosted or n8n cloud.
*   **OpenAI API Key:** With access to the `gpt-4o-mini` model (or another suitable GPT model).
*   **YouTube Access:** The workflow needs a way to fetch transcripts. This might rely on:
    *   A specific n8n node for YouTube transcripts (check node documentation).
    *   Potentially a YouTube Data API v3 key if using API-based nodes (ensure you have quota).
*   **(Optional) Telegram Bot:** If using the notification feature:
    *   A Telegram Bot Token.
    *   Your Telegram Chat ID.
*   **Configured n8n Credentials:**
    *   OpenAI API Key credential.
    *   (If needed) YouTube API Key credential.
    *   (If needed) Telegram Bot credential.

## Setup Instructions

1.  **Import Workflow:** Import the provided workflow JSON into your n8n instance.
2.  **Configure Credentials:**
    *   **OpenAI Node:** Select your configured OpenAI credential. Ensure the model is set (e.g., `gpt-4o-mini`). Review the prompt for suitability.
    *   **YouTube/Transcript Node:** Configure this node according to its requirements. If it needs an API key, select your YouTube credential.
    *   **(Optional) Telegram Node:** Select your configured Telegram Bot credential and enter your Chat ID in the node's parameters.
3.  **Review Webhook Node:**
    *   Note the Webhook URL (Test or Production).
    *   Understand how it expects the YouTube URL (e.g., in a JSON body like `{"url": "YOUTUBE_URL"}` or as a query parameter). Adjust the workflow nodes accordingly if needed to extract the URL correctly.
4.  **Activate Workflow:** Save the workflow and toggle it to **Active**.

## How to Use

1.  Obtain the **Webhook URL** (Test or Production) from the Webhook node in your n8n workflow.
2.  Send an HTTP request (usually a POST request) to this URL, providing the YouTube video URL in the expected format (e.g., as JSON in the request body).

**Example using `curl` (assuming JSON body):**

```bash
curl -X POST \
  YOUR_WEBHOOK_URL \
  -H 'Content-Type: application/json' \
  -d '{
    "url": "https://www.youtube.com/watch?v=YOUR_VIDEO_ID"
  }'
