# AI YouTube Automation using n8n

## Overview

This project implements an automated content generation and publishing pipeline using n8n. The system generates short-form video content ideas using an AI agent, retrieves relevant media from free stock APIs, and uploads videos to YouTube Shorts automatically.

The solution is designed to eliminate dependency on paid video generation APIs by integrating free resources while maintaining a scalable and production-ready workflow.

---

## Key Features

* Automated AI-based idea generation
* Dynamic video retrieval using Pexels API
* Automatic generation of **Title**, **Caption**, **Hook Text**, and **Hashtags**
* Randomized content selection to prevent repetition
* End-to-end automation from idea generation to publishing
* Fully functional without paid APIs

---

## Content Generation Components

The AI agent generates structured metadata for each video:

* **Idea** – Core concept of the video (e.g., cute/funny/emotional scenario)
* **Title** – Short, engaging YouTube Shorts title optimized for clicks
* **Caption** – Description text for the video including emotional context
* **Hook Text** – Attention-grabbing text displayed in the first few seconds
* **Hashtags** – SEO-optimized tags (e.g., #cat #kitten #viral #shorts)

---

## Workflow Architecture

The automation pipeline consists of the following steps:

1. **Schedule Trigger**

   * Executes the workflow at predefined intervals

2. **AI Agent**

   * Generates structured output including **Idea**, **Title**, **Caption**, **Hook**, and **Hashtags**

3. **Google Sheets Integration**

   * Stores generated content for tracking and reuse

4. **Pexels API (HTTP Request)**

   * Fetches relevant videos using dynamic queries based on **Idea**
   * Uses pagination and randomness to ensure content diversity

5. **Video Processing (HTTP Request)**

   * Extracts video URL from API response:

     ```
     {{$json.videos[0].video_files[0].link}}
     ```
   * Downloads video as binary data

6. **YouTube Upload**

   * Uploads video automatically
   * Uses generated **Title**, **Caption**, and **Hashtags** as metadata

---

## Technical Implementation

### API Integration

* Integrated Pexels Video API for free video sourcing
* Configured HTTP headers for authentication
* Used dynamic query construction:

  ```
  encodeURIComponent($json.output[0].Idea)
  ```

### Data Extraction

* Parsed nested JSON response using n8n expressions:

  ```
  {{$json.videos[0].video_files[0].link}}
  ```

### Randomization Strategy

* Implemented:

  * Random page selection
  * Multiple results per request
  * Random video selection from results

### Automation Logic

* Fully automated pipeline from idea generation to upload
* No manual intervention required after setup

---

## Technologies Used

* n8n (workflow automation)
* Pexels API (video source)
* YouTube Data API (video publishing)
* Google Sheets (data storage)
* HTTP Request nodes (API communication)

---

## Challenges and Solutions

### Paid API Dependency

Initial approach relied on a paid video generation API.

**Solution:** Replaced with free stock video APIs while preserving automation.

---

### Repetitive Content

Using a single API result caused repeated videos.

**Solution:** Introduced randomness in query pagination and selection.

---

### Incorrect Data Mapping

Errors occurred due to improper JSON path usage.

**Solution:** Corrected expressions such as:

```
{{$json.output[0].Idea}}
```

---

### API Errors

Encountered issues like invalid headers and bad requests.

**Solution:** Properly configured headers and validated request formats.

---

## Conclusion

This project demonstrates how a fully automated AI-driven content pipeline can be built using free tools and APIs. It highlights practical implementation of workflow automation, API integration, and dynamic content generation suitable for scalable digital content systems.
video Link : https://drive.google.com/file/d/1nhV5RKDGB1LbaUhS9S-4vGEsQhr4-oNM/view?usp=sharing
