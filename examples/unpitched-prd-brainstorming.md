## Introduction

I'm working on a new project with a senior engineer who has expertise in product development and front-end engineering. I have more expertise in AI engineering and back-end and systems engineering. We are working on a web product called Unpitched. We are in the very early stages of brainstorming this product. Our constraint is that we want to ship it in three weeks. We are both senior, just to remind you. And we want to create a PRD, or project requirements document, for this project.

Here's a rough idea of the product with main thought behind it:

```
Many startup founders stumble when talking to potential customers—defaulting to “pitch mode” instead of learning. The main idea is to operationalise the best practices from The Mom Test book by Rob Fitzpatrick. Our app helps founders prepare for the interviews, check interviews against the best practices, for example detecting founders switching to pitch mode rather than learning about the customer. 

The key enabling technology is to use LLMs to help with the process. LLMs let us provide the "magic" of taking unstructured brain dump and conversation transcripts, and performing tasks that human (e.g. external consultant) would do.

The result? Faster validation cycles, fewer false positives, and a founder team that can talk to users with the same confidence they write code—all because an opinionated workflow makes it impossible to take shortcuts. Stop guessing, start learning, and ship products customers actually need.
```

For now, the task will be to brainstorm details of the project and identify key missing assumptions or unclear ideas behind the product. After going back and forth a few times, we will write down the PRD. I'll give you an example of a PRD from another project that worked really well. You should focus on extracting the style of writing, which is very concise and to the point. The style of planning uses the walking prototype idea in terms of sequencing tasks, and it discusses technology, user flows and all those things. So you should focus on the structure and fine details of the plan, of the PRD. And we would like to emulate this for this new project. You should take note of any other details of the example PRD that you think are important for the new PRD.

This new project is code-named Unpitched for now. Our priority for this PRD and the scope we'll be discussing is to ship a working end-to-end product. The absolute priority is getting the core functionality working, and creating a wow experience for the user. Security, privacy, etc. are not a priority for now. This is due to the time constraint, and PoC nature of the project.

---

We had some brainstorming session already. We tried to figure out "jobs-to-be done" for the product (as addressing users' needs). Here's a dump of the summary of that session:
```markdown
This meeting focused on designing a tool to help with customer interviews and recruitment processes, particularly for technical founders who struggle with conducting effective non-pitching interviews.

### Product Components

- **Pitch Creation**: An internal tool to help articulate hypotheses about what's being built and for whom. Input is an unstructured "braindump" from founders, and output is a structured pitch document with clear hypotheses.
- **Interview Scenario Preparation**: Guiding users through creating an interview structure with best practices. This includes generating questions and providing a step-by-step interview script.
- **Question Analysis**: Evaluating interview questions against best practices and providing feedback on question quality.
- **Interview Analysis**: Providing feedback on conducted interviews, analyzing whether the interviewer pitched instead of listening, balanced speaking time appropriately, and followed the planned structure.
- **Future Features**: Question saturation tracking, collective analysis across interviews, identifying repeatable patterns, and question improvement suggestions, create a "dry run with LLM" feature for practicing interviews

### Development Priorities

- Desktop as the primary target platform, with mobile as secondary
- Create a "walking skeleton" or "tracer bullet" approach to development
- Focus on shipping a working end-to-end product that users can log in and use
- Build an "opinionated software" that guides users through the best practices
```

These are not great but give you some starting points and rough ideas.

## Piggybacking on the Circleback

There's this AI notetaking app called Circleback: http://circleback.ai

It stands out as the best at extracting action items, numeric data, key insights, non-obvious points, etc. from a meeting. It handles audio meetings, has an option to upload audio recordings, and it's excellent at transcribing the meeting.

For Unpithced, we plan to directly integrate with Circleback. It's either a manual integration where users will be asked to manually paste the transcript of the meeting and Circleback-generated summary, or an automatic integration where we will use Circleback's API to get the transcript and summary. This is yet to be decided, probably based on the time required to implement the integration.

## The origin of the idea

I (Grzegorz) recently helped a technical team with their very early stage product development. The first thing I noticed is that they were clearly breaking principles of The Mom Test, especially drifting into pitch mode, and spinning wheels as a result.

Patrick (the other senior engineer) has joined the project and we want to explore the idea of creating the "digital twin" to the Mom Test book.

## Non-priorities

- market evaulation
- competition evaluation
- RWD support for mobile devices
- data privacy and security

We should assume that this is a PoC and a fun project to work on. The go-to-market strategy is not a priority at this stage. A tiny go-to-market strategy is to launch at the Warsaw AI Tinkerers event that is due in four weeks.

## Example PRD

Here's the example of a PRD that worked really well for the project called `store.new`:
``````markdown
# PRD: `store.new` – AI-Powered E-commerce Store Generator

## 1. Overview

`store.new` is a service hosted at `store.new` that enables users to create a functional e-commerce store on the Your Next Store platform by providing a natural language description of their desired store (e.g., "a luxury candle store with a minimalist theme"). An AI agent, powered by GPT-4o, generates a comprehensive JSON description based on the user's input, which is sent to Your Next Store via a single API endpoint to create the store. The Your Next Store API only validates and stores this JSON. The process concludes with a live preview of the generated store displayed in the browser.

This PRD defines the requirements for a proof of concept (PoC) to be completed in 10 days by a team of three senior engineers. The focus is on delivering a minimal, functional end-to-end flow, leveraging the team's expertise to handle implementation details.

**Tech Stack:**
- **Next.js**: Frontend and backend framework.
- **Vercel**: Deployment and hosting platform.
- **AI SDK**: For integrating AI capabilities (by Vercel).
- **TypeScript**: Language for type safety and maintainability.
- **GPT-4o**: AI model for generating store JSON and image descriptions.
- `text-embedding-3-small`: embedding model for image descriptions.

---

## 2. User Flow

1. **User Input:**
   - The user enters a description of their desired store into a text box.
   - The UI provides 2-3 predefined example buttons (e.g., "Fashion Store," "Electronics Store") that prefill the text box with sample prompts.

2. **AI Generation:**
   - Upon clicking "Generate," the AI agent processes the input and generates a JSON object defining the store's structure, content, and theme.

3. **Store Creation:**
   - The JSON is sent to Your Next Store's API, which returns either an error (if invalid) or a domain name for the created store.

4. **Preview:**
   - The store is displayed in an iframe on the right side of the screen, with the user's prompt visible on the left for reference.
   - There's also a separate toggle/switch for preview of the generated JSON code.

**Rationale:**
- A simple, intuitive flow mirrors successful models like `new.email`, ensuring minimal input yields a tangible output.
- Predefined examples guide users, making the tool accessible even for vague or broad inputs.

---

## 3. Functional Requirements

### 3.1 User Interface (UI)
- **Two-Column Layout:**
  - **Left Column:** Text box for user input with 2-3 predefined example buttons below.
  - **Right Column:** Iframe to display the live store preview once generated.
  - **Toggle/Switch:** For preview of the generated JSON code.
- **Input Guidance:**
  - Placeholder text in the input box (e.g., "Describe your store...").
  - Example buttons prefill prompts like "A modern fashion store with minimalist design."

**Rationale:**
- The two-column layout keeps the input visible alongside the result, providing context.
- Predefined examples reduce user friction and ensure functional outputs.

### 3.2 AI Agent
- **Input Processing:**
  - Accepts broad or specific descriptions, using defaults for vague inputs (e.g., generic store name, neutral theme).
- **Output:**
  - Generates a comprehensive JSON object conforming to the Your Next Store structure, including:
    - Store name and description.
    - Theme (from a predefined set).
    - 2-3 categories (e.g., "Men," "Women" for clothing).
    - Full definitions for 6-12 products including names, summaries, prices.
    - Generates **image placeholder URLs** (see Section 4.2.1) for required images (e.g., for HeroSection, FeatureSection, and individual products) instead of direct image URLs.
- **Prompt Engineering:**
  - Uses the provided prototype prompt as a starting point.
  - Ensures valid JSON with OKLCH colors for the global palette and hex colors for section themes.

**Rationale:**
- Defaults ensure functionality with minimal input, aligning with the PoC's feasibility focus.
- The prototype prompt reduces initial engineering effort, though iteration may be needed.

### 3.3 API Integration
- **Backend Processing:**
  - Before sending to Your Next Store, the backend intercepts the AI-generated JSON.
  - It identifies special **image placeholder URLs** (see Section 4.2.1) within the JSON structure.
  - It parses these placeholders to extract the AI-generated description for the desired image.
  - It uses these *specific* descriptions to select appropriate image URLs from a predefined library via in-memory vector similarity search against pre-computed embeddings (associated with the library images' descriptions).
  - It inserts these selected image URLs into the JSON object, replacing the original placeholder URLs.
- **Send JSON to Your Next Store:**
  - POST the **finalized** JSON (with image URLs included) to the Your Next Store API endpoint. The Your Next Store API is solely responsible for validating the structure and content of the submitted JSON; no pre-validation occurs in the `store.new` backend for this PoC.
- **Handle API Response:**
  - Success: Retrieve the domain name and load the store in the iframe.
  - Error: Display a user-friendly message (e.g., "Unable to generate store. Please try again.").

**Rationale:**
- Focusing on the core flow (input → AI → JSON → API → preview) keeps the PoC manageable within 10 days.

### 3.4 Preview
- **Iframe Embedding:**
  - Load the store using the domain name returned by the API.
- **Error Handling:**
  - Display an error message if the API fails or the store cannot load.

### 3.5 Product Images & Layout Images:
  - A library of ~200 categorized images (e.g., fashion, electronics, lifestyle) stored statically within the project repository.
  - Each image has an associated descriptive text (e.g., "Minimalist workspace with laptop and plant", "Close-up of a steaming cup of coffee") stored alongside, likely in a JSON file.
  - Embeddings for these descriptions are pre-computed by a developer using a dedicated script *before* runtime (e.g., during development) and stored as static data (e.g., another JSON file) committed to the repository. This process is *not* part of the automated build pipeline.

**Rationale:**
- Predefined assets simplify AI tasks, ensuring consistency and accelerating development.
- Pre-computing embeddings offline and using in-memory search provides efficient image selection without external dependencies or build-time overhead.

---

## 4. Technical Architecture

### 4.1 Frontend (Next.js)
- **UI Components:**
  - Text input with placeholder and example buttons.
  - Iframe for preview.
- **State Management:**
  - Manage user input, loading states, and error messages.

### 4.2 Backend (Next.js API Routes)
- **AI Integration:**
  - Use AI SDK to call GPT-4o with the user's prompt and prototype prompt.
- **JSON Generation:**
  - AI generates the initial JSON structure, including specially formatted **image placeholder URLs** where final image `src` values are needed. See Section 4.2.1 for details.

#### 4.2.1 Image Placeholder and Selection Strategy

To communicate image requirements from the AI agent to the backend for lookup in the static library, this system uses a specific placeholder URL format embedded directly within the standard `image.src` fields of the generated JSON.

- **Placeholder Format:** The AI agent will be instructed to generate URLs in the following format for any required image:
  `https://yns.img?description=<URL-encoded description>`
  Where `<URL-encoded description>` is the AI's generated textual description of the desired image, properly URL-encoded (e.g., spaces become `%20`).

- **Example within JSON:**
  ```json
  {
    "id": "HeroSection",
    "data": {
      "title": "Artisan Coffee Roasters",
      "description": "Discover expertly roasted beans.",
      "button": { "label": "Explore Blends", "path": "/products" },
      "image": {
        "src": "https://yns.img?description=close-up%20of%20freshly%20roasted%20coffee%20beans%20spilling%20from%20a%20burlap%20sack",
        "alt": "Freshly roasted coffee beans" // AI can still generate alt text
      }
    },
    "theme": { "backgroundColor": "#f5f0e8", "color": "#4a2c2a" }
  }
  ```

- **Rationale:**
  - **Standard Structure:** Leverages the existing `image.src` field, minimizing changes to the JSON schema the AI needs to learn and produce.
  - **Clear Signal:** Provides an unambiguous, machine-parseable signal to the backend that an image lookup and replacement are required for this specific field.
  - **Encapsulation:** Keeps the description of the required image directly associated with the field where the final URL belongs.
  - **Simplified Backend Logic:** Makes it easy for the backend to find all required image lookups by simply scanning for URLs starting with `https://yns.img?`.

- **Backend Image Selection (Implementation):**
  - The backend API route handler intercepts the JSON from the AI.
  - It scans the JSON for `src` fields containing URLs matching the `https://yns.img?description=` pattern.
  - For each match, it extracts and URL-decodes the `description` parameter.
  - It calculates an embedding for this description using `text-embedding-3-small` (via the Vercel AI SDK `embed` function).
  - It performs a simple linear similarity search (calculating cosine similarity) using primitives from the Vercel AI SDK (e.g., `cosineSimilarity` function, see [AI SDK Embeddings Docs](https://sdk.vercel.ai/docs/ai-sdk-core/embeddings#embedding-similarity)) against the pre-computed embeddings of the static image library (see Section 3.5).
  - It selects the URL of the best-matching image from the library based on the highest similarity score.
  - It replaces the original placeholder URL (e.g., `https://yns.img?...`) in the JSON with the selected static image URL (e.g., `/images/library/coffee_beans_close_up.jpg`).
  - Implements fallback logic (e.g., using a default placeholder image URL or logging a warning) if no suitable match is found above a certain similarity threshold.

- **API Call:**
  - Send JSON to Your Next Store's API and process the response.

#### 4.2.2 Hero Section Image Selection Strategy

- **Goal:** To dynamically select hero images from the static library whose visual composition complements the chosen text/content layout (`boxAlignment`) specified in the `HeroSection` data. This aims to improve text legibility by placing text over relatively empty areas of the background image.
- **Mechanism:**
  - **AI Role:** The AI agent generates the `HeroSection` JSON, setting the `data.boxAlignment` field (initially restricted to `"left"` or `"right"` for the PoC based on theme or defaults) and generating a standard semantic placeholder URL (`https://yns.img?description=...`) for `data.image.src`. The AI prompt will be updated to remove the previous exclusion of `HeroSection` images from this placeholder mechanism and to guide the selection of `boxAlignment`.
  - **Backend Role:** The backend API route intercepts the JSON. When processing a `HeroSection`, it parses the semantic `description` from the `image.src` placeholder URL and reads the required `boxAlignment` value directly from the `HeroSection.data`.
  - **Selection Process:** The backend performs a vector similarity search using the extracted `description` against the descriptions of images in the static library. It then filters or prioritizes the semantically relevant matches based on the required `boxAlignment`. This layout matching relies on a filename convention for the hero images stored in the library:
    - Images suitable for `boxAlignment: "left"` should have filenames ending in `-left.jpg` (or similar extension).
    - Images suitable for `boxAlignment: "right"` should have filenames ending in `-right.jpg` (or similar extension).
    - The backend logic will check the filename of candidate images after the semantic search.
  - **Fallback:** If no image satisfies both the semantic and layout requirements (e.g., no `*-left.jpg` matches the description well enough), the backend should implement a fallback, such as selecting the best semantic match regardless of filename convention or using a predefined default hero image.
- **Image Library Requirements:**
  - Hero images added to the library must follow the filename convention (`*-left.jpg`, `*-right.jpg`) to indicate their intended layout suitability.
- **Alternatives Considered:** An alternative was adding an `&align=` parameter to the placeholder URL itself. Using the existing `boxAlignment` field in the JSON was preferred to avoid redundancy and keep the URL format consistent with product images.
- **PoC Scope:** The initial implementation focuses on `"left"` and `"right"` alignments using a limited set of foundational hero images (e.g., the Quark examples). Support for `"center"` alignment and a broader semantic range of hero images are deferred post-PoC. Filename convention is used for simplicity; a more robust metadata system could be adopted later.

### 4.3 Assets
- **Predefined Themes:**
  - 3-5 themes (e.g., minimalist, vibrant, classic) with OKLCH color palettes.
- **Product Images:**
  - Categorized images (e.g., fashion, electronics) stored in a static JSON file or codebase. Images will be stored along with AI-generated English descriptions that will be used by the AI agent to select the right product images.

**Rationale:**
- Predefined assets simplify AI tasks, ensuring consistency and accelerating development.

---

## 5. Assumptions and Constraints

### 5.1 Assumptions
- **Static Store Structure:**
  - Fixed paths: `/`, `/products`, `/products/[slug]`, `/collection/[slug]`. *(Note: `/collection/[slug]` is included but its necessity might be re-evaluated during development).*
  - No layout customization in v0.
- **Predefined Themes and Images:**
  - Themes are selected from a predefined set.
  - Images (layout and product) are selected by the backend from a predefined library using **AI-generated descriptions embedded in placeholder URLs** (see Section 4.2.1) via vector search.
- **AI Output:**
  - Generates 2-3 categories and full definitions for 6-12 products (excluding final image URLs).
  - Provides **image placeholder URLs** containing descriptive text for all required images.
- **API Response:**
  - Returns a domain name or an error message.

**Rationale:**
- A static structure focuses the AI on content generation, simplifying the PoC.
- Predefined assets ensure consistency and reduce complexity.

### 5.2 Constraints
- **Timeline:** 10 days with three senior engineers.
- **No Product Variants:** Products lack variants (e.g., size, color).
- **Minimal Error Handling:** Prioritizes core flow; edge cases are deferred.
- **Static Image Embeddings:** Image description embeddings are generated offline by developers and committed; they are not generated dynamically or during the build.
- **Image Description Format:** AI must generate image requirements using the specific placeholder URL format defined in Section 4.2.1.
- **JSON Validation:** For the PoC, JSON validation is intentionally deferred to the receiving Your Next Store API. No separate validation layer will be built within the `store.new` backend.
- **Detailed Error Handling:** Specific strategies for handling various error conditions (e.g., AI failures, image search fallbacks, API errors) will be defined during development.

**Areas for Further Investigation:**
- **Minimal Set of Paths:** Validate if `/collection/[slug]` is essential for the core PoC functionality or can be deferred.
- **Image Descriptions and Matching Quality:** Ensure high-quality image descriptions in the static library and test the effectiveness of matching them against AI-generated descriptions extracted from placeholder URLs.
- **AI Prompt Refinement:** Test and iterate the prototype prompt for consistent, valid JSON outputs, including correctly formatted image placeholder URLs with effective descriptions suitable for vector search.
- **Error Handling:** Explore edge cases (e.g., invalid inputs, API downtime, image search fallback logic) during development. Detailed error handling strategies beyond the basic success/failure paths will be clarified during the implementation phases.

---

## 6. Implementation Plan

The PoC will be delivered in four phases over 10 days:

### Phase 1: Core Infrastructure and AI Integration (Days 1-3)
- [x] Set up Next.js project with Vercel deployment, based on the Chat SDK by Vercel: https://github.com/vercel/ai-chatbot
- [x] Cleanup the initial project structure
  - [x] Disable auth protection for the routes and pages for faster development. We might want to add the auth protection back in the future.
  - [x] Add `/` route that serves a homepage with a form for prompt input.
- [x] Integrate AI SDK and GPT-4o for JSON generation (initially without image placeholder urls).
- [x] Implement the prototype prompt and test initial JSON structure outputs.
  - [x] Add a simple POST call to YNS API to send the JSON and get a domain name in return.
- [x] **Develop Image Library and Embedding Script:** Create the initial image library (~50-100 images) with descriptions in a JSON file. Develop and run the script to pre-compute and store embeddings for these descriptions (`text-embedding-3-small`). Commit image files and JSON data (descriptions, embeddings) to the repository.
  - [x] Download the initial images from the toy image scratchpad and store them in the `./public/images/library/` folder.
  - [x] Create a script to generate textual descriptions for the images and pre-compute and store embeddings for the image descriptions based on image files stored in the Git repo, at `./public/images/library/`.
  - [x] Commit the image files and JSON data (descriptions, embeddings) to the repository.
  - [x] Move image storage to Vercel Blob Storage.


### Phase 2: UI, User Flow, and Image Placeholder Generation (Days 4-5)
- [x] Build the two-column UI (prompt input with examples on the left, iframe preview on the right).
- [x] Add predefined example buttons (e.g., "Fashion Store").
- [x] Implement basic form validation and error handling.
- [x] Refine AI prompt to generate **image placeholder URLs** (as defined in Sec 4.2.1) for **product images** (`products[].imageUrl`).

### Phase 3: Backend Image Selection and API Integration (Days 6-7)
- [x] Implement backend logic to parse **image placeholder URLs**, load static embeddings, generate query embeddings using the Vercel AI SDK (`embed`), perform linear vector search using Vercel AI SDK primitives (`cosineSimilarity`), select the best match, and inject final image URLs into the JSON object (as defined in Sec 4.2.1). Implement basic fallback logic.
- [x] Integrate with Your Next Store's API to send the finalized JSON and retrieve the store domain.
- [x] Add initial hero images (e.g., Quark examples) to `./public/images/library/` following the layout filename convention (`*-left.jpg`, `*-right.jpg`) as described in Section 4.2.2.
- [x] Refine AI prompt (`app/api/generate/gen-store-json-prompt.md`) to generate `boxAlignment` (left/right only) as detailed in Section 4.2.2, and the backend to always select hero image from the quark example. There won't be any placeholder URLs for the hero image at this stage.

### Phase 4: Testing and Refinement (Days 8-10)
- [x] Test end-to-end flow with various inputs (broad and specific).
- [x] Refine the AI prompt based on output quality.
  - [x] Make hero text box colors consistent with the assumed white background of the hero images.
- [x] Ensure the preview loads correctly and the store is functional.
- [x] Refine AI prompt (`app/api/generate/gen-store-json-prompt.md`) to include `HeroSection.data.image.src` in the placeholder URL mechanism and generate `boxAlignment` (left/right only) as detailed in Section 4.2.2.
- [x] Update backend image selection logic to handle `HeroSection` images, using `boxAlignment` from JSON and filename convention (`*-left.jpg`, `*-right.jpg`) for layout filtering, as detailed in Section 4.2.2.
- [ ] Refine AI prompt to generate **image placeholder URLs** (as defined in Sec 4.2.1) for **logo, ogimage, and section images** (e.g., FeatureSection). *(Note: This task might need adjustment based on HeroSection implementation)*.
- [x] Test the Hero Section image selection flow end-to-end, ensuring correct image selection based on description and `boxAlignment`.

**Rationale:**
- Phased development prioritizes critical components (AI and infrastructure), and getting end-to-end flow working early, allowing iterative refinement later.

---

## 7. Prototype Prompt for AI Agent

Below is an example of a prototype of the prompt to the AI agent; it should serve as a starting point, and illustration but it's not the final prompt by any means. It defines the JSON structure, section types, and color rules, and illustrates some detailed concepts and ideas how to prompt the AI agent.

`````markdown
## Prompt for AI Agent

You are an AI agent tasked with generating a JSON description for an e-commerce store on the Your Next Store platform based on a user's natural language prompt describing their store. Your output must conform to the platform's JSON structure, which includes "paths" for page layouts and "settings" for global configurations. Below are the guidelines and structure you must follow.

---

### JSON Structure Overview

- **"paths"**: An object where each key is a route (e.g., "/", "/products", "/products/[slug]") and each value is an array of sections defining the page content. Includes a special "%layout" key for the global layout applied to all pages.
- **"settings"**: An object containing global store configurations like logo, colors, and store name.

---

### Available Sections and Their "data" Structures

Here are the section types you can use, along with the structure of their "data" fields and available "theme" properties:

- **HeroSection**: A prominent banner.
  - **"data"**:
    ```json
    {
      "title": string,
      "description": string,
      "button": { "label": string, "path": string },
      "image": { "src": string | null, "alt": string }
    }
    ```
  - **"theme"**: Customize with these properties (use hex color format, e.g., "#ffffff"):
    - `"backgroundColor"`: Background color.
    - `"color"`: Text color.
    - `"buttonBackgroundColor"`: Button background color.
    - `"buttonTextColor"`: Button text color.
    - `"buttonHoverBackgroundColor"`: Button background color on hover.
  - **Example**:
    ```json
    {
      "id": "HeroSection",
      "data": { "title": "Welcome", "description": "Discover our products", "button": { "label": "Shop Now", "path": "/products" }, "image": { "src": "hero.jpg", "alt": "Hero Image" } },
      "theme": { "backgroundColor": "#f0f0f0", "color": "#333333" }
    }
    ```

- **ProductGrid**: A grid of products.
  - **"data"**:
    ```json
    { "first": number, "collection": string | null }
    ```
  - **"theme"**: Set to `{}` to inherit from the global palette. No specific theme properties are available.

- **CollectionGrid**: A grid of collections.
  - **"data"**:
    ```json
    { "collections": Array<{ "slug": string }> }
    ```
  - **"theme"**: Set to `{}` to inherit from the global palette. No specific theme properties are available.

- **Nav**: Navigation bar (required in "%layout").
  - **"data"**:
    ```json
    { "title": string | null, "links": Array<{ "label": string, "href": string }>, "searchBar": { "show": boolean } }
    ```
  - **"theme"**: Customize with these properties (use hex color format):
    - `"backgroundColor"`: Background color.
    - `"hoverBackgroundColor"`: Background color of links on hover.
    - `"color"`: Text color of the links.
  - **Example**:
    ```json
    {
      "id": "Nav",
      "data": { "title": "My Store", "links": [{ "label": "Home", "href": "/" }], "searchBar": { "show": true } },
      "theme": { "backgroundColor": "#ffffff", "color": "#007bff" }
    }
    ```

- **Footer**: Footer (required in "%layout").
  - **"data"**:
    ```json
    { "sections": Array<{ "header": string, "links": Array<{ "label": string, "href": string }> }>, "name": string | null, "tagline": string | null, "credits": boolean }
    ```
  - **"theme"**: Customize with these properties (use hex color format):
    - `"backgroundColor"`: Background color.
    - `"color"`: Text color.
  - **Example**:
    ```json
    {
      "id": "Footer",
      "data": { "sections": [{ "header": "Company", "links": [{ "label": "About Us", "href": "/about" }] }], "name": "My Store", "credits": true },
      "theme": { "backgroundColor": "#333333", "color": "#ffffff" }
    }
    ```

- **Children**: Placeholder for page content (required in "%layout").
  - **"data"**: `{}`
  - **"theme"**: Set to `{}` to inherit from the global palette.

- **Title**: Page title.
  - **"data"**:
    ```json
    { "title": string }
    ```
  - **"theme"**: Set to `{}` to inherit from the global palette.

- **Markdown**: Text content in TipTap format.
  - **"data"**:
    ```json
    { "content": object }
    ```
  - **"theme"**: Set to `{}` to inherit from the global palette.

- **ProductDetails**: Product details (for dynamic routes).
  - **"data"**: `{}`
  - **"theme"**: Customize with these properties (use hex color format):
    - `"color"`: Text color.
    - `"buttonBackgroundColor"`: Button background color.
    - `"buttonHoverBackgroundColor"`: Button background color on hover.
    - `"buttonTextColor"`: Button text color.

- **ProductDescription**: Product description (for dynamic routes).
  - **"data"**: `{}`
  - **"theme"**: Set to `{}` to inherit from the global palette.

- **RelatedProducts**: Related products (for dynamic routes).
  - **"data"**: `{}`
  - **"theme"**: Set to `{}` to inherit from the global palette.

- **ReviewList**: Customer reviews (for dynamic routes).
  - **"data"**: `{}`
  - **"theme"**: Set to `{}` to inherit from the global palette.

- **FeatureSection**: Highlighted feature with text and image.
  - **"data"**:
    ```json
    { "title": string, "description": string, "image_alt": string, "image_src": string | null, "image_position": "left" | "right" }
    ```
  - **"theme"**: Set to `{}` to inherit from the global palette.

- **CountdownWidget**: Countdown timer.
  - **"data"**:
    ```json
    { "text": string, "targetDate": string | null }
    ```
  - **"theme"**: Customize with these properties (use hex color format):
    - `"backgroundColor"`: Background color.

For all sections:
- Set `"scope"`: "global"
- Set `"theme"`: `{ ... }` with properties customized for the section based on the design you envision, or `{}` if no custom theme is needed. Use hex color format for all color properties in section themes.

---

### Instructions

#### 1. Handling "paths"
- **Standard Routes**: Include these unless the user specifies otherwise:
  - **"/"**: Homepage (e.g., HeroSection, ProductGrid).
  - **"/products"**: Product listing page (e.g., ProductGrid with "first": 12).
  - **"/products/[slug]"**: Individual product page (e.g., ProductDetails, ProductDescription).
  - **"/collection/[slug]"**: Collection page (e.g., ProductGrid with "first": 6).
- **Custom Routes**: Add static pages (e.g., "/about") if mentioned by the user, using sections like Title and Markdown.
- **Dynamic Routes**: For "/products/[slug]" and "/collection/[slug]", set "data": {} for all sections.
- **Global Layout ("%layout")**: Always include:
  - "Nav" (with links based on user input).
  - "Children" (with "data": {}).
  - "Footer" (with sections based on user input).
- Populate "data" for static route sections based on the user's description (e.g., titles, links).

#### 2. Mapping User Input to Sections
- **Homepage ("/")**: Add HeroSection for banners, ProductGrid for product lists, CollectionGrid for collections, etc., based on user description.
- **Navigation ("Nav")**: Include links to pages/collections mentioned (e.g., "Home" to "/", "Products" to "/products").
- **Footer**: Create sections (e.g., "Shop", "Company") with links derived from the user's prompt.
- **Product Pages ("/products/[slug]")**: Add RelatedProducts or ReviewList if the user mentions them.
- **Custom Pages**: For pages like "/about", use Title and Markdown with content from the user's description.
- Generate text (titles, descriptions, button labels) creatively based on the store's theme and user input.

#### 3. Handling "settings"
- **Hardcoded Values**: Use these exactly as provided:
  - `"logo"`: { "width": 1024, "height": 1024, "imageUrl": "https://yns.app/icon.png" }
  - `"ogimage"`: "https://yournextstore.com/opengraph-image.png"
- **Generated Values**:
  - `"colors"`: Generate a `"palette"` object based on the user's description of their store. Include keys such as `"theme"`, `"theme-nav"`, `"theme-button"`, `"theme-footer"`, and `"theme-primary"`, each with sub-properties like `"DEFAULT"` and `"background"`. Assign OKLCH color values (e.g., "50% 0.1 120") that reflect the store's theme (e.g., modern, vintage). If no design preference is specified, use a default neutral palette.
  - `"storeName"`: Extract from the user's prompt (e.g., "Tech Gadgets"); default to "Your Store" if not specified.
  - `"storeDescription"`: Generate a brief description from the prompt (e.g., "Discover the best in electronics").
  - `"fontFamily"`: Set to "merriweather" (default).

#### 4. Defaults and Assumptions
- If the user doesn't specify:
  - Navigation: Include links to "/", "/products", and any mentioned collections.
  - Footer: Include a section with the store name and "credits": true.
  - ProductGrid: Set "first": 12.
- For images (e.g., HeroSection), use "src": "https://stripe-camo.global.ssl.fastly.net/cd09e4877d3e3e8aa26b05d8778f75f8a814c1660e0de4fe443c76ca2ee07aae/68747470733a2f2f66696c65732e7374726970652e636f6d2f6c696e6b732f4d44423859574e6a644638785433426165473547536d4e57625668366255527366475a735833526c633352666258425856477445515538784e6a68355a575257574852336155396d526a526f3030336e67523942526a".

#### 5. Handling Themes and Colors
- **Global Color Palette in "settings"**:
  - All color values within `"settings" > "colors" > "palette"` must use the **OKLCH format** (e.g., "50% 0.1 120").
  - This palette defines the store's overall color scheme.
  - **Example**:
    ```json
    "settings": {
      "colors": {
        "palette": {
          "theme": { "background": "100% 0 0" },
          "theme-nav": { "DEFAULT": "13.63% 0.0364 259.2", "background": "100% 0 0" },
          "theme-button": { "DEFAULT": "50% 0.15 210" }
        }
      }
    }
    ```
- **Section-Specific Themes in "paths"**:
  - All color values within section `"theme"` objects must use the **hex format** (e.g., "#ffffff").
  - Use sparingly to maintain cohesion with the global palette.
  - **Example**:
    ```json
    "paths": {
      "/": [
        { "id": "HeroSection", "data": { ... }, "theme": { "backgroundColor": "#f0f0f0", "color": "#333333" } }
      ]
    }
    ```
- **Key Rule**:
  - Use **OKLCH format only in "settings" > "colors" > "palette"**.
  - Use **hex format for all colors in section "theme" objects**.
- **Consistency**: Ensure section themes complement the global palette.

---

### User Prompt

```
{user_prompt}
```

---

### Your Task
Based on the user's natural language prompt:
1. Generate a complete JSON object following the structure and rules above.
2. Use the hardcoded values for "logo" and "ogimage" as specified.
3. Generate "colors" in OKLCH format for the global palette and use hex format for section themes.
4. Extract "storeName" and "storeDescription" from the prompt, defaulting to "Your Store" and a generic description if not provided.
5. Populate "paths" with appropriate sections and data based on the user's description.
6. Ensure the JSON is syntactically correct and includes all required fields.
7. Output only the JSON object as your response.
`````

This prompt has several simplifications (e.g. the hardcoded logo/ogimage URLs) that will be addressed during the development of this project, following the image selection strategy outlined in Section 4.2.1 (backend selecting images from a static library based on *AI-generated descriptions extracted from placeholder URLs*, matched against *pre-computed descriptions* in the library).

**Areas for Further Investigation:**
- Test the prompt with diverse inputs and refine it to ensure consistent, valid JSON outputs, including useful and correctly formatted image placeholder URLs suitable for the vector search matching process.
- Evaluate the effectiveness and performance of the in-memory vector search implementation for matching AI descriptions (from placeholders) to library descriptions.

## External resources

- https://yns.app/admin/ai-test - UI (textbox input) for testing the JSON representation of a store.
- https://yns.app/admin/ai-test/schema.json - JSON schema for the store's JSON representation.
- https://yns.app/admin/ai-test/store.json - a dump of JSON object representing a store currently in the Your Next Store database.

---

## 8. Post-PoC Feature Development

With the successful completion of the initial 10-day PoC (Proof of Concept), the following features are planned for the next phase of development. These features build upon the PoC infrastructure and address key areas for improvement and expansion.

### 8.1 Image Library Migration to PostgreSQL/pgvector

**Goal:** Migrate the image library storage from the static `library.json` file and in-memory search to a persistent PostgreSQL database using the `pgvector` extension. This provides scalability and enables real-time updates necessary for integrating newly generated images.

**Rationale:**
- The static JSON approach, while sufficient for the PoC, does not allow for dynamic additions to the image library (e.g., saving user-generated images via `getimg.ai`).
- A database solution provides a robust and scalable foundation for managing a growing image library.
- `pgvector` enables efficient vector similarity searches directly within the database, replacing the in-memory search logic.

**Technical Implementation:**
- **Database Setup:**
  - Provision a PostgreSQL database instance using Neon ([https://neon.tech](https://neon.tech)).
  - Enable the `pgvector` extension within the Neon database.
  - Define a database schema for a unified `images` table. A single table approach is chosen for simplicity in querying and application logic, accommodating different image types (product, hero, etc.) within one structure. Specific metadata like layout hints will be stored in nullable columns. The schema includes:
    - `id` (UUID, Primary Key, default `gen_random_uuid()`): Unique identifier.
    - `blob_url` (TEXT NOT NULL): URL to the image file in Vercel Blob.
    - `description` (TEXT NOT NULL): Textual description/prompt.
    - `embedding` (VECTOR(1536) NOT NULL): Embedding vector from `text-embedding-3-small`.
    - `hash` (TEXT NOT NULL): SHA256 hash of the image file content, used for incremental updates.
    - `filename` (TEXT, nullable): Original filename for reference.
    - `shortName` (TEXT, nullable): A short (3-5 word) title/name for the image generated by AI.
    - `blob_pathname` (TEXT NOT NULL): The storage path used within Vercel Blob.
    - `layout_hint` (TEXT, nullable, CHECK (`left`, `right`, `center`)): Layout suitability hint, primarily for hero images.
    - `source` (TEXT NOT NULL): Origin ('static' or generation service name like 'getimg.ai').
    - `created_at` (TIMESTAMP WITH TIME ZONE NOT NULL, default `CURRENT_TIMESTAMP`): Creation timestamp.
- **Data Migration Script:**
  - Develop a one-time script **adapted from `scripts/rebuild-image-library-index.ts`** to:
    - **Retain the core incremental processing logic:** Connect to the database to load existing image records (including `hash` and `blob_pathname`). Scan the local image directory, calculate hashes, and compare against stored data.
    - Only perform Vercel Blob uploads, AI description/embedding generation, and database operations (`INSERT`, `UPDATE`, `DELETE`) for new, modified, moved, or deleted images.
    - Read the existing image metadata (descriptions, filenames, potentially pre-computed embeddings) from the source (`library.json` or original image files/descriptions).
    - Connect to the Neon database.
    - Insert the static library image data into the new `images` table, populating all relevant fields, including generating embeddings if necessary using `text-embedding-3-small`. Ensure `source` is set to 'static'.
  - **Image Library Synchronization Script (`scripts/rebuild-image-library-index.ts`):**
    - Modify the existing script (`scripts/rebuild-image-library-index.ts`) to interact with the PostgreSQL database instead of the `data/lib/image-library.json` file.
    - **Retain Incremental Logic:** The script must continue to use its incremental processing capabilities. It should:
      - Connect to the database to load existing image records (including `hash` and `blob_pathname`).
      - Scan the local image directory (`public/images/library`), calculate hashes for each file.
      - Compare local files/hashes against database records to identify new, modified, moved, or deleted images.
      - Only perform Vercel Blob uploads, AI description/embedding generation, and database operations (`INSERT`, `UPDATE`, `DELETE`) for the identified changes.
    - **Initial Run:** The first execution of this modified script will serve as the one-time data migration, populating the `images` table from the local file system and setting `source` to 'static' for these initial records.
- **Backend Logic Update:**
  - Refactor the backend API route (`/api/generate`) responsible for image selection (Sections 4.2.1 & 4.2.2).
  - Replace the `library.json` loading and in-memory search logic with database operations:
    - Use a PostgreSQL client library (e.g., `node-postgres`/`pg`, **no ORM** will be introduced initially) to connect to the Neon database.
    - Generate an embedding for the incoming description from the image placeholder URL (`https://yns.img?description=...`).
    - Execute a SQL query using `pgvector` operators (e.g., `<=>` for cosine similarity) to find the most similar image embeddings in the `images` table.
    - Apply necessary filtering (e.g., `layout_hint` based on `boxAlignment` for hero images).
    - Retrieve the `blob_url` of the best-matching image.
- **Environment Configuration:**
  - Add database connection string and credentials as secure environment variables (e.g., `POSTGRES_URL`).

**Considerations:**
- Ensure appropriate indexing (e.g., HNSW index on the `embedding` column) is created in PostgreSQL for efficient vector search performance.

### 8.2 On-Demand Product Image Generation (getimg.ai)

**Goal:** Provide users the option to generate unique product images on-demand using a text-to-image service (`getimg.ai`), instead of relying solely on the image library. Generated images will be added to the persistent library.

**User Flow & Experience:**
- A toggle or selection mechanism will be added to the UI allowing users to choose between:
  - "Use Stock Images" (current behavior: static library lookup via vector search).
  - "Generate New Images" (new behavior: `getimg.ai` generation).
- Image generation applies **only to product images** (`products[].imageUrl`). Hero images, logos, section images, etc., will continue to use the existing placeholder and **database** lookup mechanisms.
- The store generation process will **block** UI interaction until both JSON generation and product image generation (if selected) are complete. Latency will increase compared to the static library path.
- **No user controls** for re-generating images or modifying prompts are planned for the initial version (KISS principle).
- Basic error handling will be implemented (e.g., displaying a message if `getimg.ai` fails).
- *(Optional/Stretch Goal)*: Stream status updates to the frontend indicating the current phase (e.g., "Generating JSON...", "Generating product images...").

**Technical Implementation:**
- **Conditional Backend Logic:** The `/api/generate` backend route will contain conditional logic based on the user's UI selection.
- **Generation Path:**
  - The AI agent will still generate JSON containing `https://yns.img?description=...` placeholder URLs for product images.
  - If "Generate New Images" is selected, the backend intercepts the JSON.
  - For each product image placeholder:
    - Extract the URL-decoded `description`. *(Note: Investigate if these descriptions need refinement to serve as effective text-to-image prompts)*.
    - Call the `getimg.ai` text-to-image API using the description. Parallelize API calls for efficiency, respecting potential `getimg.ai` concurrency limits. A fixed image size (e.g., 1024x1024) will be requested.
    - Handle API responses, including potential errors (e.g., rate limits, content flags). *(Note: Detailed error handling strategies need further investigation)*.
    - Download the generated image from the `getimg.ai` URL.
    - Upload the downloaded image to Vercel Blob storage (e.g., under `/images/generated/<unique_id>.png`).
    - Store the original generation `description` (prompt) as metadata associated with the image file in Vercel Blob.
    - **Persist Generated Image:** Insert the details of the newly generated image into the **PostgreSQL `images` table**, including its Vercel Blob URL, the original description, its generated embedding (using `text-embedding-3-small`), and setting the `source` to 'generated'.
    - Replace the original placeholder URL in the JSON with the new Vercel Blob URL for the generated image.
- **Library Lookup Path:** If "Use Stock Images" is selected, the **database lookup logic** (vector search on the `images` table based on placeholder description, as defined in Section 8.1) is used.
- **Final JSON:** The finalized JSON (with either static or generated product image URLs) is sent to the Your Next Store API.
- **Security & Cost:** The `getimg.ai` API key will be stored securely (env vars). Basic rate limiting or usage caps will be configured on the `getimg.ai` service side to manage costs.

**Considerations:**
- **Prompt Quality:** Descriptions optimized for similarity search might not be optimal for image generation. Prompt refinement or adaptation might be needed.
- **Error Handling:** Define robust handling for `getimg.ai` API errors and upload failures.
- **Latency:** Parallelizing calls is crucial to manage the added latency.
- **Stylistic Consistency:** Ensure generated images align reasonably with the store's theme (may require prompt engineering).
- **Embedding Consistency:** Ensure embeddings generated for new images use the same model (`text-embedding-3-small`) and process as those for the initial static library migration.

**Technical Reference: Example `getimg.ai` API Interaction (Bash Script)**

*Note: This script demonstrates the basic API call flow for generating images based on prompts from a JSON file. It serves as a starting point for implementing the backend logic.*

```bash
#!/bin/bash

# Replace with your actual API key stored securely (e.g., environment variable)
API_KEY="YOUR_GETIMG_API_KEY_HERE"
ENDPOINT="https://api.getimg.ai/v1/flux-schnell/text-to-image"
OUTPUT_DIR="outputs"
mkdir -p "$OUTPUT_DIR"

INPUT_FILE="$1"

if [[ -z "$INPUT_FILE" ]]; then
  echo "❌ Usage: ./generate.sh input_prompts.json"
  exit 1
fi

if [[ ! -f "$INPUT_FILE" ]]; then
  echo "❌ File '$INPUT_FILE' does not exist."
  exit 1
fi

# Extract base filename without extension to use as prefix
FILE_PREFIX=$(basename "$INPUT_FILE" .json)

# Simple list of common English stopwords
STOPWORDS="a|the|with|and|of|to|in|on|for|from|is|as|at|an|by|this|that|be|must|no"

# Read prompts from a JSON array like: [{"prompt": "..."}, ...]
jq -c '.[]' "$INPUT_FILE" | nl -v 1 | while read -r index line; do
  prompt=$(echo "$line" | jq -r '.prompt')

  # Generate a simple filename based on keywords (first 6 non-stopwords)
  keywords=$(echo "$prompt" | \
    tr 'A-Z' 'a-z' | \
    tr -cd 'a-z0-9 \n' | \
    tr ' ' '\n' | \
    grep -v -E "^($STOPWORDS)$" | \
    head -n 6 | \
    paste -sd '-' -)

  # Handle cases with no suitable keywords
  if [[ -z "$keywords" ]]; then
      keywords="image"
  fi

  filename="${FILE_PREFIX}_${index}_${keywords}.png"
  filepath="$OUTPUT_DIR/$filename"

  echo "⏳ Generating image for prompt ${index}: ${prompt:0:50}..."

  # Make the API call
  response=$(curl -s --request POST \
    --url "$ENDPOINT" \
    --header 'accept: application/json' \
    --header "authorization: Bearer $API_KEY" \
    --header 'content-type: application/json' \
    --data "{\"prompt\": \"$(echo $prompt | sed 's/"/\\"/g')\", \"width\": 1024, \"height\": 1024, \"response_format\": \"url\"}") # Ensure prompt JSON is escaped

  # Extract the image URL (adjust selectors based on actual API response structure)
  image_url=$(echo "$response" | jq -r '.imageUrl // .url // .images[0].url // empty')

  if [[ -n "$image_url" ]]; then
    # Download the image
    curl -s "$image_url" -o "$filepath"
    if [[ $? -eq 0 ]]; then
        echo "✅ Saved: $filepath"
    else
        echo "❌ Failed to download image for prompt ${index}."
    fi
  else
    echo "⚠️  Failed to get image URL for prompt ${index}: ${prompt:0:50}..."
    echo "   Response: $response"
    # Save error response for debugging
    echo "$response" > "$OUTPUT_DIR/${FILE_PREFIX}_error_${index}.json"
  fi
done
```

### 8.3 Internal Image Library Viewer

**Goal:** Provide an internal tool for the development team to easily browse, search, and understand the contents of the **image library stored in the PostgreSQL database and Vercel Blob storage**.

**Features (MVP):**
- **Location:** A new page within the application, accessible via a dedicated route (e.g., `/dev/image-library`). Access control will be added using the existing authentication mechanism, gating access to authorized users.
- **UI:** A simple web interface (React component) displaying:
  - Thumbnails of images from the **database** (loaded from Vercel Blob URLs stored in the DB).
  - The associated description, filename, source, and other relevant metadata for each image.
- **Search:** Basic, case-insensitive text search filtering images based on keywords in their **descriptions and/or filenames stored in the database**.
- **Pagination:** Implement simple pagination for the results, querying the database with appropriate LIMIT/OFFSET clauses.

**Technical Implementation:**
- **Backend API Route:** A Next.js API Route (e.g., `app/api/dev/image-library/search/route.ts`) will handle search requests. This is preferred over Server Actions for easier standalone debugging/testing.
- **Data Loading:**
  - The API route will connect to the **Neon PostgreSQL database**.
  - It will query the `images` table based on the text query parameter (using `ILIKE` for case-insensitive text search) and pagination parameters (LIMIT/OFFSET).
  - The API returns the filtered list of matching image metadata (Blob URL, description, filename, etc.) to the frontend. No large static file loading is required.
- **Frontend:**
  - The React component for the viewer page makes `fetch` requests to the backend API route on search input changes (with debouncing) and for pagination.
  - Renders the list of images and their details fetched from the API.
- **Data Freshness:** The viewer will reflect the current state of the `images` table in the database relatively close to real-time (depending on caching strategies, if any are added later).

**Features (Stretch Goals):**
- **Similarity Search:** Add functionality to search for images based on semantic similarity to a text query. This would require:
  - Generating an embedding for the user's query (using Vercel AI SDK `embed`).
  - Performing a `pgvector` similarity search against the `embedding` column in the `images` table.
- **Advanced Filtering/Sorting:** Add options to filter by `source` ('static'/'generated'), `layout_hint`, or sort results by `created_at`, etc., by adding corresponding query parameters and `WHERE`/`ORDER BY` clauses to the backend SQL.

**Considerations:**
- **Database Performance:** Monitor query performance, especially for text searches and potential similarity searches. Ensure appropriate database indexes are in place (standard indexes for text columns, HNSW for vector column).
- **UI Scalability:** Ensure the frontend handles rendering potentially large numbers of search results efficiently (pagination helps initially).

---

### 8.4 Implementation Plan (Post-PoC)

This plan outlines the development tasks for the Database Migration, On-Demand Image Generation, and Internal Library Viewer features. The migration is a prerequisite for the other two.

#### 8.4.1 Image Library Migration to PostgreSQL/pgvector
- [x] Provision Neon PostgreSQL database and enable `pgvector`.
- [x] Define and create the `images` table schema.
- [x] Add database connection details to environment variables.
- [x] Modify `scripts/rebuild-image-library-index.ts` to interact with the PostgreSQL database instead of `image-library.json`, preserving incremental logic (hash comparison, etc.).
- [x] Run the modified `scripts/rebuild-image-library-index.ts` script for the initial data migration, populating the `images` table from the current local library.
- [x] Refactor the `/api/generate` route's image selection logic to query the database using `node-postgres` and `pgvector` instead of loading `library.json`.
- [x] Test the existing image selection flow thoroughly to ensure it works correctly with the database backend.
- [x] **Migrate image type identification from convention to explicit DB column**
    - **Context:** Our debugging revealed that identifying images as 'product' or 'hero' currently relies on fragile string matching within file paths (`blob_pathname LIKE 'library/%/products/%'`) or filenames (`filename LIKE '%-hero-%'`). This required fixes in the querying logic (`/api/generate/route.ts`) and makes the system less robust and harder to maintain.
    - **Goal:** Introduce an explicit `image_type` column (e.g., TEXT) to the `images` table to store whether an image is intended as a 'product' or 'hero' image (or potentially other types in the future). This will make querying more direct and less error-prone.
    - **Subtasks:**
        - [x] Add `image_type TEXT` column to the `images` table schema in PostgreSQL. (Consider adding a `CHECK (image_type IN ('product', 'hero'))` constraint).
        - [x] Modify `scripts/rebuild-image-library-index.ts`:
            - When processing an image, determine its type based on the *current* conventions (e.g., if `blob_pathname` matches `library/%/products/%` -> 'product', if `filename` contains `-hero-` -> 'hero', default could be 'product' or null/other).
            - Store the determined type in the new `image_type` column during the `INSERT` or `UPDATE` (UPSERT) operation.
        - [x] Re-run `scripts/rebuild-image-library-index.ts` to populate the `image_type` for all existing images in the database.
        - [x] Refactor `/api/generate/route.ts` (`findImageInDB` function):
            - Remove the `LIKE` clauses on `blob_pathname` and `filename` used for type detection.
            - Instead, filter using the new column: `WHERE image_type = 'product'` or `WHERE image_type = 'hero'`.
            - The `layout_hint` check will still be needed for hero images.
        - [x] Test the end-to-end `/api/generate` flow to ensure product and hero images are correctly identified and selected using the new `image_type` column.
- [x] Create necessary database indexes (e.g., HNSW on embeddings).

#### 8.4.2 On-Demand Product Image Generation (getimg.ai)
- [ ] *(Prerequisite: 8.4.1 Complete)*
- [x] Create prototype route (/api/dev/test-getimg) to validate getimg.ai API interaction and key setup.
- [x] Add UI toggle/selector on the frontend to choose between "Stock Images" (DB Lookup) and "Generate New Images".
- [x] Implement basic conditional logic scaffolding in `/api/generate` based on the UI selection.
- [x] Securely configure `getimg.ai` API key (env var).
- [x] Implement the backend logic within `/api/generate` for the "Generate New Images" path:
  - Extract descriptions from product image placeholders.
  - Implement parallelized API calls to `getimg.ai` text-to-image endpoint.
  - Handle `getimg.ai` API responses (success and basic errors).
- [x] Implement image download from `getimg.ai` URL.
- [x] Implement image upload to Vercel Blob, including storing the prompt as metadata.
- [x] Incorporate getimg.ai returned image URL into the store JSON representation using the Vercel Blob URL.
- [x] **Implement logic to generate embedding and insert the new image record (Blob URL, prompt, description, embedding, source='generated') into the PostgreSQL `images` table.**
- [x] Test the end-to-end flow for on-demand image generation with various prompts, verifying database insertion.
- [x] Refine error handling for `getimg.ai` integration and database insertion based on testing.
- [x] Refine the prompt engineering for `getimg.ai` to improve image quality and relevance to the store.
  - [x] Refine the prompt to prevent image generation from outputting unclean background.
  - [x] Generated product should be centered in the image. It should be a central focus of the image.
  - [x] There should be no text except on labels on the product.
- [x] Persist Generation Prompt:
    - [x] Add a new nullable `generation_prompt TEXT` column to the `images` table schema in PostgreSQL (definition updated in `docs/db_schema.sql`).
    - [x] **Manually alter live database:** Ran `ALTER TABLE images ADD COLUMN generation_prompt TEXT NULL;` against Neon DB.
    - [x] Modify the database insertion logic (e.g., in `insertImageRecord` in `app/lib/image-generation.ts`) to store the `modifiedPrompt` used for `getimg.ai` in the new `generation_prompt` column. This column should only be populated for images where `source` is 'getimg.ai'.
    - [x] Display `generation_prompt` in the internal image library viewer.
- [ ] *(Optional)* Implement status streaming for the generation process.

#### 8.4.3 Internal Image Library Viewer
_An internal tool in the spirit of admin UI like in Django or Rails._

- [x] *(Prerequisite: 8.4.1 Complete)*
- [x] Create the backend API route (`app/api/dev/image-library/search/route.ts`).
- [x] Implement database connection logic in the API route.
- [x] Implement API logic to query the `images` table based on text search and pagination parameters.
- [x] Create the frontend page component for the viewer (`/dev/image-library/page.tsx`).
- [x] Implement UI elements: search bar, image grid/list display, pagination controls.
- [x] Implement frontend logic to call the search API route (with debouncing) and display results.
- [x] Implement pagination logic on the frontend.
- [x] Integrate access control using the existing auth mechanism to restrict the page to authorized users.
- [ ] Test the library viewer functionality, including search and pagination, verifying it correctly displays data from the database (both static and potentially generated images if 8.4.2 is also complete).
- [ ] *(Optional)* Implement similarity search for the library viewer.
- [ ] *(Optional)* Implement advanced filtering/sorting.

### 8.5 Image Generation Enhancements

#### 8.5.1 Goals & Overview

This workstream focuses on expanding image generation capabilities beyond the initial `getimg.ai` integration. Key goals include:
- Integrating additional text-to-image generation models (`fal.ai` Flux 1 Pro, OpenAI `gpt-image-1`) as alternatives.
- Experimenting with techniques (reference images, richer prompts) to improve stylistic consistency across multiple generated product images.
- Enabling on-demand generation for hero images, addressing layout alignment challenges.

#### 8.5.2 Design Considerations & Rationale

- **Alternative Engines:** Explored `fal.ai` and OpenAI `gpt-image-1` as potential providers offering different capabilities, including potential text+image input support needed for reference images [[1]](https://fal.ai/models/fal-ai/flux-pro/v1.1/api).
- **Consistency Strategies:** The primary challenge is ensuring stylistic consistency for multiple product images generated for a single store. Two main strategies were identified:
    - *Reference Images:* Provide a reference image (initially hardcoded) primarily for *stylistic* guidance (lighting, mood, composition), alongside a text prompt describing the desired *product*. Relies on model capabilities (e.g., `fal.ai`'s `image_url` + `image_prompt_strength`; OpenAI `gpt-image-1`'s image input via edit/generations endpoints). Risk: Model might overfit to the reference image's *subject* instead of just its style.
    - *Richer Prompts:* Replace the current simple prompt structure (basic description + boilerplate style) with a significantly more detailed, structured text prompt. This aims to provide enough explicit textual detail about visual elements, lighting, and composition to achieve consistency without a reference image.
      - *Current Prompt Structure Example (for `getimg.ai`):*
        ```
        Product photo:
A jar of rejuvenating night cream with retinol and peptides, in a soft pastel and gold design.

Style: suitable for ecommerce site, clean, white background, centered product shot, no text.
        ```
      - *Richer Prompt Example (Tested with Flux 1.1 Pro):*
        ```
A minimalist, low-top casual sneaker displayed in perfect profile against a plain, light gray or off-white studio background. The shoe is lavender in color with a smooth, tightly woven knit textile upper and a matte finish. It has a clean, seamless silhouette with no logos or decorative elements, emphasizing simplicity and modern design.

The sneaker features black metal eyelets and matching lavender-colored laces, with a soft, slightly padded tongue integrated smoothly into the upper. The sole is thick, rounded, and made from smooth white rubber or EVA, curving gently at the toe and heel for a contemporary, ergonomic look.

The shoe is the only object in the frame, centered horizontally, with soft, diffused lighting that casts a gentle shadow beneath it. The visual style is clean, calm, and modern — ideal for premium ecommerce display.
        ```
      - *(Note: The richer prompt example showed promising results in initial tests with Flux 1.1 Pro, but further evaluation is needed across different products and models.)*
- **Iterative Approach ("Walking Skeleton"):** To manage complexity and risk, development will proceed iteratively:
    1.  Integrate new engines (`fal.ai`, OpenAI) for basic text-to-image generation for *products* only.
    2.  Explicitly test and compare the two consistency strategies (Reference Images vs. Richer Prompts) for *product* images.
    3.  Address hero image generation, including alignment challenges, *after* product generation and consistency are better understood.
- **UI:** For initial development and testing, the UI will be updated to provide explicit selection between the four modes (Stock, `getimg.ai`, `fal.ai`, OpenAI), controlling generation for applicable image types (initially products, later heroes). A more refined UI is deferred.

#### 8.5.3 Implementation Plan

*(Phases focus on iteratively building end-to-end functionality and testing hypotheses)*

**Phase 1: Walking Skeleton - Add New Engines for *Product* Images (Text-to-Image)**
- [x] Task: Extend the existing UI for Generation Mode Selection (4 modes: Stock, getimg, falai, openai). *(Frontend change)*
- [x] Task: Integrate `fal.ai` API (Backend for **Text-to-Image Only**).
    - [x] Install `fal.ai` client, configure keys according to https://fal.ai/models/fal-ai/flux-pro/v1.1/api
    - [x] Implement function `callFalAiTextToImage(prompt: string)`.
- [x] Task: Integrate OpenAI (`gpt-image-1`) API (Backend for **Text-to-Image Only**).
    - [x] Implement function `callOpenAiTextToImage(prompt: string)` using the OpenAI Images API (`/v1/images/generations`) with the `gpt-image-1` model.
- [x] Task: Adapt Backend Logic for *Product* Image Generation Modes.
    - [x] Modify image processing logic (e.g., `processSinglePlaceholder`) based on UI mode.
    - [x] Construct current-style prompt from `placeholder.description`.
    *   [x] Call respective API function (`callGetImgApi`, `callFalAiTextToImage`, `callOpenAiTextToImage`).
    *   [x] Ensure response handling, fallbacks, persistence for products.

**Phase 2: Product Image Consistency Experiments**
- [ ] Task: Implement Reference Image Handling for `fal.ai` & OpenAI (Products Only).
    - [ ] Add logic for hardcoded reference image (read/upload/encode).
    - [ ] Create new API call functions (`callFalAiWithReference`, `callOpenAiWithReference`) using text+image parameters.
    - [ ] Adapt backend logic to use these functions in 'falai'/'openai' modes for products.
- [ ] Task: Richer Prompt Generation Strategy (Products Only).
  - [x] Stage A — Deterministic Template Expansion (baseline, _must-have_)
    - [x] Backend: replace the hard-coded `Product photo:` template in `app/lib/image-generation.ts` with a three-sentence scaffold:
      1. `<concise description>` (from placeholder)
      2. composition & lighting sentence (“Displayed in perfect profile against a plain light-grey studio background, centred, soft diffused lighting”)
      3. style sentence (“Clean, calm, modern — ideal for premium e-commerce display.”)
    - [x] Prompt tweak: in `gen-store-json-prompt.md` tell the AI to output **one factual sentence**; update the example. Replace `The <description> part should be a detailed, objective description (ideally 2-3 sentences) …` with `The <description> must be a single, concise factual sentence that names the product, colour(s), material and one or two key features. Do NOT mention background lighting, camera angle or style words (those will be added later by the backend template).`
    - [x] Prompt tweak: in `gen-store-json-prompt.md` update the example to use the new prompt structure. Replace `"A sleek, minimalist low-top sneaker in deep blue with a smooth texture, featuring black laces and eyelets and a clean white sole, offering a modern versatile look."` with `   "A deep-blue low-top leather sneaker with black laces, black eyelets and a clean white sole."`
    - [x] Prompt tweak: in `gen-store-json-prompt.md` same one-sentence guidance for the hero-image placeholders (section 8 of the prompt).
    - [x] Test whether tweaked prompts lead to better consitency and better quality of product images. The result of testing: short, narrowly-focused products descriptions led to generic, soulless product images. We will not use this approach, and we switched to the richer descriptions (3-5 detailed sentences) that suffer from less consistency, though.
  - [x] Stage B — Global Style Emission (_optional_)
    - [x] Prompt spec: introduce optional `settings.imageStyle` (2-3 sentences, ≤240 chars).
    - [x] Backend: use `settings.imageStyle` to replace the hard-coded style sentence; fallback to default if missing.
  - [ ] Stage C — LLM-based Prompt Expansion (_exploratory_)
    - [ ] Prototype a single GPT-3.5 call that combines `[concise description, imageStyle]` into a 3-5-sentence rich prompt; batch per store.
    - [ ] Measure added latency/cost; A/B compare image quality with Stage A.
  - [ ] Stage D — Evaluation & Tuning
    - [ ] Script to generate ~20 products in three modes (current, Stage A, Stage C) and collect designer ratings.
    - [ ] Choose default generation path based on results; document decision.
- [ ] Task: Test & Evaluate Product Image Consistency.
    - [ ] Generate stores comparing baseline, reference image, and richer prompt approaches.
    - [ ] Evaluate stylistic consistency. Document findings and decide on preferred strategy.

**Phase 3: Hero Image Generation**
- [x] Task: Enable Text-to-Image Generation for Hero Images.
    - [x] Adapt image processing logic to handle hero placeholders based on UI mode.
    - [x] Construct appropriate text prompts for hero images.
    - [x] Call basic text-to-image functions for selected engine.
- [x] Task: Experiment with Hero Image Alignment (Prompt Engineering).
    - [x] Focus on modifying text prompts to encourage correct composition (left/right empty space). Test across engines.
    - Result: OpenAI `gpt-image-1` was the only engine that could generate hero images with the right composition.
- [ ] Task: Implement Hero Image Fallback & Persistence.
    - [ ] Handle errors/poor alignment (e.g., fallback to DB stock).
    - [ ] Integrate persistence (upload, hash, embed, DB insert), consider `layout_hint`.
- [ ] Task: *(Optional/If Needed)* Apply Consistency Strategy to Hero Images.
    - [ ] Implement chosen product consistency strategy (Reference/Rich prompts) if needed for heroes.

### 8.6 Predetermined Color Palettes

#### 8.6.1 Goals & Overview

This workstream aims to improve the reliability and maintainability of store color theme application by replacing dynamic LLM color generation with a predefined set of palettes.

#### 8.6.2 Design Considerations & Rationale

- **Problem:** The current approach requires the LLM to generate colors in two different formats (OKLCH for global settings, hex for section themes) and apply them consistently, which is complex, error-prone, and makes the prompt brittle.
- **Chosen Approach (Backend Injection):** To ensure correctness and simplify the LLM's task, the LLM will only be asked to output the *name* of a desired palette (from a predefined list). Backend code will then look up the corresponding color definitions (stored in `.ts` code) and inject the correct OKLCH and hex values into the final JSON structure. This approach prioritizes reliability and maintainability over maximizing LLM responsibility.
- **Implementation:** Will be done in two steps: first, refactor the prompt and backend to handle a default theme via injection, then introduce the named palettes and selection mechanism.

#### 8.6.3 Implementation Plan

*(This workstream is deferred until Image Generation Enhancements are further along)*

- [x] **Task: Refactor Prompt & Backend for Colors (Default Injection)**
    - [x] Simplify `gen-store-json-prompt.md` by removing detailed color generation rules.
    - [x] Modify backend (`/api/generate/route.ts`) to inject a hardcoded *default* theme (OKLCH & hex values) with colors and values taken from the prompt (if we find them there).
- [x] **Task: Implement Predefined Color Palettes (Named Palettes)**
    - [x] Define 1-2 named palettes (OKLCH/hex values) in code (e.g., `constants/palettes.ts`).
    - [x] Update the (simplified) prompt to instruct the LLM to output a `settings.chosenPaletteName`.
    - [x] Enhance backend logic to read the chosen name, look up the palette, and inject the specific colors.
    - [x] Add named color palete with vibes like "Eco-friendly, wholesome, appealing to health-conscious consumers".

### 8.7 Showcase of Generated Stores

This workstream introduces features for users to track their generated stores and for the community to discover and interact with stores created on the platform. The initial scope will be minimal, focusing on delivering core user-facing functionality iteratively.

#### 8.7.1 Goals
-   Allow users to easily find and revisit their previously generated stores, with an option to mark favorites.
-   Provide a public gallery of generated stores where logged-in users can view and vote on them.

#### 8.7.2 Features

1.  **Personal Store Library ("My Stores"):**
    *   Core Functionality: A private page for a logged-in user to view a list of stores they have generated. Each store entry will display a preview (hero image), the original prompt, a link to the live store, and the creation timestamp. Users can "star" or "unstar" stores, and filter their list to see only starred items.
    *   Key Data Points: `user_id`, `prompt_text`, `store_url`, `hero_image_url`, `is_starred`, `created_at`.

2.  **Public Store Showcase ("Explore"):**
    *   Core Functionality: A public page displaying a gallery of generated stores. Initially, all successfully generated stores are eligible. Each store entry will display a preview (hero image), a link to the live store, and its net vote count. Logged-in users can upvote or downvote each store.
    *   Key Data Points: `store_url`, `hero_image_url`, `user_id` (for voter), `vote_type`.

#### 8.7.3 Database Schema

1.  **`generated_stores` Table:**
    *   `id` (UUID, PK)
    *   `user_id` (TEXT NOT NULL, identifies the creator)
    *   `user_email` (TEXT, nullable, email of the creator for easier debugging)
    *   `prompt_text` (TEXT NOT NULL)
    *   `store_url` (TEXT NOT NULL, from YNS)
    *   `hero_image_url` (TEXT, extracted from `finalJson` for preview)
    *   `is_starred` (BOOLEAN, default `false`, for "My Stores")
    *   `created_at` (TIMESTAMP WITH TIME ZONE, default `CURRENT_TIMESTAMP`)

2.  **`store_votes` Table:**
    *   `id` (UUID, PK)
    *   `store_id` (UUID, FK to `generated_stores.id`)
    *   `user_id` (TEXT NOT NULL, identifies the voter)
    *   `user_email` (TEXT, nullable, email of the voter for easier debugging)
    *   `vote_type` (TEXT, e.g., 'up' or 'down')
    *   `created_at` (TIMESTAMP WITH TIME ZONE, default `CURRENT_TIMESTAMP`)
    *   *Constraint: Unique on (`store_id`, `user_id`)*

#### 8.7.4 API Endpoints

*   **`/api/generate/route.ts` (Modifications):**
    *   Logic to extract `hero_image_url` from `finalJson`.
    *   Logic to save new record to `generated_stores` table.
*   **`GET /api/me/stores`:**
    *   Fetches stores for the authenticated user.
*   **`PATCH /api/me/stores/{store_id}/star`:**
    *   Toggles `is_starred` status for a user's store.
*   **`GET /api/showcase/stores`:**
    *   Fetches stores for public showcase (paginated, sorted, with net vote counts).
*   **`POST /api/showcase/stores/{store_id}/vote`:**
    *   Records a vote for an authenticated user.

#### 8.7.5 Implementation Plan

**Workstream 1: "My Stores" - Personal Library & Starring**
*   **Goal:** Allow a user to see a list of their generated stores and star their favorites.
*   **Tasks:**
    - [x] **1.1: Database - Initial Schema & Persistence:**
        - [x] Define and create the minimal `generated_stores` table.
        - [x] Modify `/api/generate/route.ts` to extract `hero_image_url` and save essential store data to `generated_stores`.
    - [x] **1.2: Backend - "My Stores" API Endpoints:**
        - [x] Create `GET /api/me/stores`.
        - [x] Create `PATCH /api/me/stores/{store_id}/star`.
    - [x] **1.3: Frontend - "My Stores" Page:**
        - [x] Develop the `/my-stores` page: list user's stores with details, preview, link, and star button. Implement starred filter.

**Workstream 2: "Explore" - Public Showcase & Voting**
*   **Goal:** Allow users to browse a public feed of generated stores and vote on them.
*   **Tasks:**
    - [x] **2.1: Database - Voting Schema:**
        - [x] Define and create the minimal `store_votes` table.
    - [x] **2.2: Backend - "Explore" API Endpoints:**
        - [x] Create `GET /api/showcase/stores` (fetch all eligible stores, paginated, calculate net votes).
        - [x] Create `POST /api/showcase/stores/{store_id}/vote` (record votes for logged-in users).
    - [x] **2.3: Frontend - "Explore" Page:**
        - [x] Develop the `/explore` page: display gallery of stores with preview, link, vote counts, and voting buttons.

#### 8.7.6 Key Considerations
-   **Hero Image Extraction:** Backend logic in `/api/generate` needs to reliably parse `finalJson` for a suitable `hero_image_url` (e.g., from `HeroSection.data.image.src` or `HeroSection.data.slides[0].image.src`).
-   **Voting Scope:** Initially restricted to logged-in users.
-   **Vote Calculation:** Net votes for the showcase will be calculated on-the-fly by querying/aggregating data from the `store_votes` table.
-   **Voting Mechanism & State Management:**
    *   **States:** A user's vote for a store can be `upvoted`, `downvoted`, or `neutral`.
    *   **Database Representation:** In the `store_votes` table, `vote_type` will store `'up'` or `'down'`. A `neutral` state is represented by the absence of a row for the specific `(store_id, user_id)` pair.
    *   **API Interaction (`POST /api/showcase/stores/{store_id}/vote`):** The client sends the user's intended vote action, e.g., `{ "vote": "up" }` or `{ "vote": "down" }`.
    *   **State Transitions & Backend Logic:**
        *   If a user votes (e.g., sends `{ "vote": "up" }`) and their current vote is the same (already 'up'), the vote is neutralized (row deleted).
        *   If their current vote is different (e.g., 'down' or neutral), the vote is set/updated to the new type ('up') (row inserted/updated).
        *   The `store_votes.created_at` timestamp is updated upon each successful vote action (insert or update) to reflect the time of the latest interaction.


### 8.8 Progressive Store-Generation Feedback

This work-stream adds near-instant visual feedback while a store is being generated by splitting the backend work into checkpoints and letting the browser poll for them.

#### 8.8.1 Goals
- Show a meaningful preview (Hero banner) within ~5 seconds of the user clicking “Generate”.
- Keep the implementation “serverless-simple”: no external queue, no new infra, plain Postgres for state, HTTP polling from the browser.
- Preserve today’s single serverless function as the execution engine; only its inner logic becomes two LLM turns, with intermediate status updates for image processing.

#### 8.8.2 Flow Overview

1.  **Client request**
    The browser generates a `jobId` (e.g., NanoId) and includes it in the request:
    ```json
    { "jobId": "<nanoid>", "prompt": "...", "imageGenerationMode": "stock" }
    ```
    Immediately after sending the `POST` request, the browser starts a polling loop (e.g., every 1 second):
    `GET /api/generate/<jobId>/status`.

2.  **Long-lived worker (within the same `/api/generate` route)**
    The `/api/generate` route handler performs the following:
    - Inserts an initial row into a new `generation_jobs` table with `status = 'queued'`.
    - Executes the store generation pipeline, which involves two LLM turns and image processing steps.
    - Updates the corresponding `generation_jobs` row in the database after each significant step:

    | Stage                      | Action                                                                     | DB `status` update          | Relevant Data Stored in DB (`generation_jobs`)                         |
    |----------------------------|----------------------------------------------------------------------------|-----------------------------|------------------------------------------------------------------------|
    | `queued`                   | Initial row inserted upon request receipt                                  | `'queued'`                  | `jobId`, `user_id`, `created_at`, `updated_at`                         |
    | `hero_json_ready`          | LLM Turn 1 (Hero section JSON with placeholders) finishes                  | `'hero_json_ready'`         | `hero_json` (placeholders), `updated_at`                               |
    | `store_skeleton_ready`     | LLM Turn 2 (Full store JSON with placeholders) finishes                    | `'store_skeleton_ready'`    | `full_json` (placeholders), `updated_at`                               |
    | `image_processing`         | (Optional) Image generation/selection begins for placeholders in `full_json` | `'image_processing'`        | `updated_at`                                                           |
    | `images_resolved`          | All image placeholders in `full_json` replaced with final URLs             | `'images_resolved'`         | `full_json` (final image URLs), `updated_at`                           |
    | `store_ready`              | YNS API sync complete for the final `full_json`                            | `'store_ready'`             | `store_url`, `updated_at` (final `full_json` is already set)           |
    | `failed`                   | Any unhandled error during the process                                     | `'failed'`                  | `error_msg`, `updated_at`                                              |

    The original `POST` request remains open while these operations occur. Once the entire process is complete (reaches `store_ready` or `failed`), the `POST` request returns a final response, similar to the current implementation (e.g., `{storeUrl, storeJson, generationTimeMs}`).

3.  **Client rendering via polling**
    - On receiving a polling response with `status = 'hero_json_ready'`, the UI renders the Hero section content (e.g., title, description from `hero_json`) and may display a progress indicator like "Generating store details...".
    - On `status = 'store_skeleton_ready'`, the UI can indicate "Finalizing content structure...". The client *could* parse `full_json` (with placeholders) for a more detailed preview if desired.
    - On `status = 'image_processing'`, the UI can show "Generating images...".
    - On `status = 'images_resolved'`, the UI can show "Preparing your store preview...".
    - On `status = 'store_ready'`, the client loads the live store (e.g., in an iframe or by redirecting to `store_url`) and stops the polling loop.
    - On `status = 'failed'`, the UI displays an appropriate error message.

#### 8.8.3 Database Schema

A new table will be introduced to track the status of generation jobs:

```sql
CREATE TABLE generation_jobs (
  id            UUID PRIMARY KEY,
  user_id       TEXT NOT NULL,          -- Identifies the user initiating the request
  status        TEXT NOT NULL,          -- e.g., 'queued', 'hero_json_ready', 'store_skeleton_ready', 'image_processing', 'images_resolved', 'store_ready', 'failed'
  hero_json     JSONB,                  -- Stores the JSON for the Hero section (nullable, ~1–2 KB)
  full_json     JSONB,                  -- Stores the complete store JSON (nullable, ~1 MB)
  store_url     TEXT,                   -- URL of the generated store (set at 'store_ready', nullable)
  error_msg     TEXT,                   -- Error message if status is 'failed' (nullable)
  created_at    TIMESTAMPTZ DEFAULT now(),
  updated_at    TIMESTAMPTZ DEFAULT now() -- Should be updated on each status change
);
-- A simple daily cron job will be set up to delete rows older than 7 days to manage table size.
```

#### 8.8.4 API Endpoints

1.  **`POST /api/generate`** (Modified)
    -   The request body *must* include the client-generated `jobId`.
    -   **Logic:**
        -   Inserts a new row into `generation_jobs` with `status = 'queued'`.
        -   Executes the two-turn LLM pipeline, followed by image processing, and then YNS API sync.
        -   Performs `UPDATE` operations on the `generation_jobs` row for that `jobId` at each stage (`hero_json_ready`, `store_skeleton_ready`, `image_processing`, `images_resolved`, `store_ready`, `failed`).
        -   The long-lived request eventually returns the final outcome (e.g., `{ storeUrl, ... }`), consistent with the current API contract.

2.  **`GET /api/generate/{jobId}/status`** (New)
    -   Path parameter: `{jobId}` (UUID v4).
    -   **Logic:**
        -   Queries the `generation_jobs` table for the given `jobId`.
        -   Returns `404 Not Found` if the `jobId` does not exist.
        -   Otherwise, returns a JSON object with the current status and relevant data:
            `{ status: string, hero_json?: object, full_json?: object, store_url?: string, error_msg?: string }`.
            (Note: `hero_json` is relevant at/after `hero_json_ready`. `full_json` (with placeholders) is relevant at `store_skeleton_ready`. `full_json` (with resolved URLs) is relevant at `images_resolved` and `store_ready`. `store_url` is relevant at `store_ready`.)
    -   Authentication: No specific auth is required for this endpoint as the `jobId` is unguessable and only provides status for a specific job.

#### 8.8.5 Prompt & LLM Interaction

The existing single main prompt file will be used, with a specific instruction appended to manage the two-turn interaction:

> Appended to current prompt:
> "There are two tasks for our interaction:
> 1️⃣ First, you will generate ONLY the JSON for the HeroSection of the store, including any necessary 'settings' like storeName and storeDescription.
> 2️⃣ Second, after I confirm the HeroSection, you will generate the complete JSON for the entire store, reusing the HeroSection details you provided in the first task.
> Please respond ONLY with the JSON for task 1 in this current turn."

-   **Turn 1:** The backend sends the full prompt (with the epilogue) to the LLM. The LLM is expected to return JSON containing only the HeroSection and essential settings.
-   **Backend after Turn 1:** The received `hero_json` is saved to the database (triggers `status = 'hero_json_ready'`).
-   **Turn 2:** The backend sends a new message to the LLM (as part of the same conversation history) like:
    > "Thank you for the HeroSection JSON. It has been noted. Now, please proceed with task 2 and generate the complete store JSON, ensuring you reuse the HeroSection content from your previous response verbatim."
-   The LLM then generates the full store JSON (this will be `full_json` with image placeholders).
-   **Backend after Turn 2:** The `full_json` (with placeholders) is saved to the database (triggers `status = 'store_skeleton_ready'`). Image processing then begins.
-   **Safety Net:** The backend will still programmatically splice the `hero_json` from Turn 1 into the final `full_json` from Turn 2 to ensure consistency, regardless of the LLM's adherence to the reuse instruction. This merged JSON (still with placeholders for other images) becomes the `full_json` for the `store_skeleton_ready` state.

#### 8.8.6 Implementation Plan

- [x] **Task 1: Database Setup**
    - Define and execute the SQL migration to create the `generation_jobs` table.
- [x] **Task 2: Prompt Engineering**
    - Update the main store generation prompt file (`gen-store-json-prompt.md`) to include the two-task epilogue.
    - Add a strong system-level instruction (if not already present) to enforce single-task responses per turn.
    - Adapt the LLM interaction logic for the two-turn conversation (but only log intermediate results for now):
      - Execute LLM Turn 1 (Hero section).
      - Log the `hero_json` to the console.
      - Execute LLM Turn 2 (Full store JSON), incorporating Hero from Turn 1.
      - Log the `full_json` to the console.
      - Perform theme injection, image placeholder replacement, and YNS API call as currently done.
- [x] **Task 3: Client-side Job ID & Backend Route Refactor (`POST /api/generate`)**
    - Generate a client-side `jobId` (e.g., using `crypto.randomUUID()`) before making the `POST /api/generate` call.
    - Modify the route to accept `jobId` in the request body.
    - Implement the initial `INSERT` into `generation_jobs` with `status = 'queued'`.
    - Add job state updates to the LLM interaction logic for two-turn conversation:
        - Execute LLM Turn 1 (Hero section).
        - `UPDATE` `generation_jobs` to `status = 'hero_ready'` with `hero_json`.
        - Execute LLM Turn 2 (Full store JSON), incorporating Hero from Turn 1.
        - Perform theme injection, image placeholder replacement, and YNS API call as currently done.
        - `UPDATE` `generation_jobs` to `status = 'full_ready'` with `full_json` and `store_url`, or to `status = 'failed'` with `error_msg` if errors occur. (Note: original PRD used `full_ready` for the final state before YNS sync, this task completed it as such).
- [x] **Task 3a: Extend job tracking status set to include intermediate generation steps**
    - **Objective:** Modify the backend logic (primarily within the `/api/generate` route handler after Task 3's work) to introduce and update new, more granular statuses in the `generation_jobs` table. This task specifically adds `store_skeleton_ready`, `image_processing`, and `images_resolved`. The final success status will be `store_ready`.
    - **Detailed Steps:**
        - After LLM Turn 2 completes and the `full_json` (with image placeholders, potentially merged with `hero_json`) is available:
            - `UPDATE` `generation_jobs` table: set `status = 'store_skeleton_ready'`, save `full_json` (with placeholders).
        - Before initiating image generation/selection for the placeholders in `full_json`:
            - (Optional but recommended for UI) `UPDATE` `generation_jobs` table: set `status = 'image_processing'`.
        - After all image placeholders in `full_json` have been processed and replaced with their final URLs (either from generation or DB lookup):
            - `UPDATE` `generation_jobs` table: set `status = 'images_resolved'`, save the updated `full_json` (with final image URLs).
        - After the YNS API sync is successfully completed using the `full_json` (with final image URLs):
            - `UPDATE` `generation_jobs` table: set `status = 'store_ready'`, save `store_url`. (This replaces the previous use of `full_ready` as the terminal success state).
        - Ensure existing error handling updates `status = 'failed'` and stores `error_msg`.
- [x] **Task 4: New Status Endpoint (`GET /api/generate/{jobId}/status`) and minimal frontend integration**
    - Create the new Next.js API route.
    - Implement the database query to fetch job status by `jobId`.
    - Return the status and relevant data as JSON.
    - Implement the polling loop to call the `/status` endpoint.
    - Add a simple frontend component to test the new endpoint. Perhaps a simple component that displays the current status? Some kind of label or a progress bar?
- [x] **Task 5: Frontend Integration**
    - Update UI based on polled status:
        - Render Hero section content when `status = 'hero_json_ready'` (using `hero_json`).
        - Display a progress bar or status messages for `store_skeleton_ready`, `image_processing`, and `images_resolved`. (Client could optionally use `full_json` from `store_skeleton_ready` or `images_resolved` for richer previews if desired).
        - Load the final store using `store_url` or show an error message upon `store_ready` or `failed`.
        - Stop polling on terminal states.
- [x] **Task 6: Fast-track Hero Image**
  Extend turn 1 of the prompt to include a description of the hero image we want to generate. This will be used to lookup stock hero image using a fast
  embedding-based lookup. We'll have a fast-tracked candidate for hero image that we'll display in the preview.
    - Modify the prompt to instruct the LLM to generate a hero image description.
    - Use the hero image description to lookup a stock image using a fast embedding-based lookup.
    - Return hero image URL in the polling response.
- [ ] **Task 7: Observability & Logging**
    - Add distinct OpenTelemetry spans for "LLM Turn 1 (Hero)", "LLM Turn 2 (Full Store Skeleton)", "Image Processing Loop", and "YNS Sync".
    - Log database interaction timings for `generation_jobs` updates for each status.
- [ ] **Task 8: Quality Assurance**
    - Test various scenarios: successful generation through all new statuses, LLM errors, image processing failures, network interruptions.
    - Verify instruction obedience by the LLM and the effectiveness of the server-side Hero splicing.
    - Verify correct status progression (`queued` -> `hero_json_ready` -> `store_skeleton_ready` -> [`image_processing` ->] `images_resolved` -> `store_ready` or `failed`) and data storage in `generation_jobs` for all intermediate steps.

#### 8.8.7 Key Considerations & Risks

1.  **Instruction Obedience by LLM:** There's a small risk the LLM might not strictly adhere to the "task 1 only" instruction in the first turn.
    -   **Mitigation:** The backend will parse the LLM's first response. If it contains more than just the HeroSection and basic settings, it can be treated as an error, potentially triggering a retry with more constrained parameters (e.g., `temperature=0`) or logging the anomaly. The server-side splicing of the hero from turn 1 into turn 2's full JSON acts as a final consistency guarantee.

2.  **Client Handling of Dual Signals:** The client receives the final store URL via polling *and* eventually from the resolution of the original long-lived `POST` request.
    -   **Mitigation:** The client should be designed to handle this gracefully, e.g., by acting on the first signal that indicates completion (likely from polling `store_ready`) and then ignoring or aborting the other. Stopping the poll once `store_ready` or `failed` is received is crucial.

3.  **Token Costs & Caching:** Sending the full prompt for the first (hero-only) turn might seem inefficient.
    -   **Mitigation:** Major LLM providers (like OpenAI) offer prompt caching. If the initial parts of the prompt are identical between Turn 1 and Turn 2 (which they will be in the chat history), the cost for reparsing those tokens is often waived or significantly reduced for the second call, making the overall cost increase marginal.

4.  **Serverless Function Timeouts:** The entire multi-turn process, including image generation, must complete within the serverless function execution limit.
    -   **Mitigation:** Vercel's current timeout of 600 seconds for Hobby/Pro plans is well above our typical ~50-90 second total generation time. Polling makes this less of a concern for the client's perception of progress for the initial steps.

5.  **Database Load & Bloat:** Polling and storing intermediate JSON increases database interactions.
    -   **Mitigation:** The polling rate (1/sec) and the number of writes per job are low. `JSONB` is efficient for storing JSON. The cron job for cleaning up old `generation_jobs` records will prevent long-term bloat.

This approach aims for a significantly improved user experience by providing early feedback, while leveraging the existing infrastructure and minimizing new complexities.
``````

## Your task

Carefully analyze the initial outline of the project or the initial direction and let's brainstorm on the product, especially in the time constraint of 20 days. What do you think should be a set of features or good ideas that we should consider? Or do you have open questions? Or do you even think this is a good idea as a product? And also I gave you a very detailed and a real example of a PRD. Let me know if it's not too long for you. Maybe it's overwhelming and there are too many details and it's hard to analyze. So let's focus on those two things for now and we'll be going back and forth for a while.
