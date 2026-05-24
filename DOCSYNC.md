# 🤖 DocSync: Autonomous AI-Powered Technical Documentation Agent

DocSync is an autonomous AI agent engineered to streamline the technical documentation process. By integrating seamlessly with GitHub, it automatically analyzes code changes, generates comprehensive documentation, and injects it directly into developer workflows — specifically, when a Pull Request is opened or updated.

Built with a modern React frontend and a robust Node.js/Express backend, DocSync leverages Google's Gemini 2.5 Flash to provide intelligent code analysis and documentation generation, aiming to eliminate documentation bottlenecks from your development cycle.

## ✨ Features

DocSync offers a suite of features designed to make documentation effortless and integrated:

### 1. 🚀 Autonomous Pull Request Documentation
The flagship feature, DocSync acts as an automated technical writer that activates with every code change.
*   **Webhook Listener**: Monitors GitHub webhooks, triggering automatically when a Pull Request is opened or updated.
*   **Intelligent Diff Analysis**: Fetches raw code changes (diff) from the PR using the GitHub API.
*   **Gemini Processing**: Sends the diff to Google's Gemini 2.5 Flash, generating an analysis of changed files, new additions, potential concerns, and documentation impact.
*   **Automated PR Comments**: Posts a concise, bulleted Markdown summary directly as a comment on the Pull Request.

### 2. 📊 Webhook Activity Dashboard
A real-time monitoring panel built into the user interface.
*   **Live Stats Cards**: Displays total events, success rate, average processing duration, and total documents generated.
*   **Event Feed**: Provides a chronological log of every webhook event with color-coded status indicators (✅ success, ❌ failed, 🔄 processing, 👁 ignored).
*   **Auto-Refresh**: The dashboard refreshes every 10 seconds, with a toggle to pause live updates.
*   **Direct Links**: Allows users to click through to view the generated comment directly on GitHub.

### 3. 📚 Documentation History
A dedicated section to browse and review all past AI-generated documentation.
*   **Expandable Accordion**: Each entry can be expanded to reveal the full Markdown documentation inline.
*   **PR Metadata**: Displays repository, PR number, title, author, and timestamp for each historical entry.
*   **GitHub Links**: Direct links to jump to the corresponding comment on GitHub.

### 4. 📁 Project-Level Documentation Generation
Ability to generate comprehensive overviews for entire repositories.
*   **Repository Dashboard**: A modern UI to view and select your GitHub repositories.
*   **Smart Filtering**: Automatically excludes common non-code files and directories (e.g., `node_modules`, `dist`, lockfiles, images, hidden files) from analysis.
*   **README Compilation**: Generates a project-wide `DOCSYNC.md` file documenting the repository's structure, components, and suggested setup.
*   **One-Click Commit**: Provides an option to push the generated `DOCSYNC.md` file directly back to the GitHub repository.

### 5. 🧪 Code Snippet Playground
A flexible testing ground for on-the-fly documentation generation.
*   **Instant Analysis**: Paste any code snippet and receive structured Markdown documentation instantly.
*   **Contextual Formatting**: Optional fields for filename and context allow for more tailored and accurate output.
*   **One-Click Copy**: Easily copy the generated Markdown to your clipboard.

### 6. 🔒 Security & Reliability
Production-grade protections built into the webhook pipeline.
*   **HMAC-SHA256 Signature Verification**: Validates the `X-Hub-Signature-256` header to ensure that only legitimate GitHub requests can trigger your endpoint. This is activated by setting `WEBHOOK_SECRET` in your `.env` file.
*   **Rate Limiting**: Implements a rate limit of 30 requests per minute per IP address to prevent abuse and manage resource usage.
*   **Graceful Error Handling**: All failures are logged with contextual information and duration, facilitating easy debugging.

## 🏗️ Project Structure

The project is organized into a client-side React application and a Node.js/Express backend.

```
DocSync_AI-powered_Technical_Documentation_Generator/
├── .env                   # Environment variables (API keys, secrets)
├── .gitignore             # Specifies intentionally untracked files to ignore
├── index.html             # Main HTML entry point for the React application
├── LICENSE.md             # Project licensing information (MIT License)
├── metadata.json          # Project metadata for Google AI Studio
├── package.json           # Defines project dependencies and scripts
├── server.ts              # Backend: Express.js server, API endpoints, webhook system
├── tsconfig.json          # TypeScript configuration for the project
├── vite.config.ts         # Vite build configuration for the frontend
└── src/                   # Frontend source (React)
    ├── App.tsx            # Main application component, handles routing and sidebar navigation
    ├── index.css          # Tailwind CSS import for styling
    ├── main.tsx           # React application entry point
    ├── types.ts           # TypeScript type definitions (e.g., for API responses, UI state)
    └── components/        # Reusable React components for different UI sections
        ├── Dashboard.tsx        # GitHub repository analysis and documentation generation interface
        ├── Playground.tsx       # Manual code snippet documentation testing area
        ├── Settings.tsx         # Setup and integration guide for GitHub tokens
        ├── WebhookDashboard.tsx # Live webhook activity monitoring and statistics
        └── DocHistory.tsx       # Browser for previously generated documentation
```

### Backend Architecture (`server.ts`)

The `server.ts` file acts as the central hub for the backend, managing API requests, GitHub webhook events, and interactions with the AI model. It includes:

*   **Express.js Setup**: Initializes the Express application and middleware.
*   **In-Memory Stores**:
    *   `webhookActivityLog`: Stores recent webhook events for the Webhook Activity Dashboard.
    *   `docHistory`: Stores details and content of past AI-generated documentation.
*   **Security Utilities**:
    *   `rateLimitMap`: Implements a simple in-memory rate limiter to protect endpoints.
    *   `verifyWebhookSignature()`: Validates incoming GitHub webhooks using HMAC-SHA256.
*   **AI Integration**:
    *   `getGenAI()`: Provides a client for interacting with the Google Gemini API using `GEMINI_API_KEY`.
*   **API Endpoints**:

| Endpoint                   | Method | Description                                                |
| :------------------------- | :----- | :--------------------------------------------------------- |
| `/api/docs/generate`       | `POST` | Generates documentation for a given code snippet.          |
| `/api/docs/generate-repo`  | `POST` | Generates project-level documentation for a GitHub repo.   |
| `/api/github/user`         | `GET`  | Fetches authenticated GitHub user information.             |
| `/api/github/repos`        | `GET`  | Lists the authenticated user's GitHub repositories.        |
| `/api/github/commit`       | `POST` | Commits generated documentation (`DOCSYNC.md`) to a repo.  |
| `/api/github/webhook`      | `POST` | **GitHub webhook receiver** for autonomous PR analysis.    |
| `/api/github/webhook/health` | `GET`  | Provides a health check and configuration status for the webhook system. |
| `/api/webhook/activity`    | `GET`  | Retrieves the log of recent webhook event activity.        |
| `/api/webhook/history`     | `GET`  | Fetches the history of AI-generated documentation.         |
| `/api/webhook/stats`       | `GET`  | Provides aggregated statistics on webhook processing.      |

## 🚀 Setup & Usage

### Prerequisites

Before you begin, ensure you have the following installed and configured:

*   **Node.js**: Version `v18` or higher.
*   **Git**: For cloning the repository and interacting with GitHub.
*   **Google Gemini API Key**: Obtainable from [Google AI Studio](https://ai.google.dev/).
*   **GitHub Personal Access Token**: Required with `repo` scope to allow DocSync to fetch repositories, code, and post PR comments.

### Installation

1.  **Clone the repository**:
    ```bash
    git clone https://github.com/sasikumar161106/DocSync_AI-powered_Technical_Documentation_Generator.git
    cd DocSync_AI-powered_Technical_Documentation_Generator
    ```

2.  **Install dependencies**:
    ```bash
    npm install
    ```

### Configuration

Create a `.env` file in the project root directory and populate it with your API keys and secrets:

```ini
# Required for AI documentation generation
GEMINI_API_KEY="YOUR_GEMINI_API_KEY"

# Required for GitHub API interactions (fetching repos, committing docs, posting PR comments)
GITHUB_TOKEN="ghp_your_github_personal_access_token"

# Optional, but HIGHLY RECOMMENDED for webhook security
# Set this to any random string. Ensure it matches the secret configured in GitHub.
WEBHOOK_SECRET="your_webhook_secret_here"
```

*   **`GEMINI_API_KEY`**: Get your key from [Google AI Studio](https://ai.google.dev/).
*   **`GITHUB_TOKEN`**: Generate a Personal Access Token (classic) from GitHub: `Settings` → `Developer Settings` → `Personal Access Tokens` → `Tokens (classic)`. Grant it the `repo` scope.
*   **`WEBHOOK_SECRET`**: Choose any strong, random string. This will be used to secure your webhook endpoint.

### Running Locally

To start the development server:

```bash
npm run dev
```

Open your browser and navigate to `http://localhost:3000`.

### Setting Up Autonomous Webhooks

To enable DocSync's autonomous PR documentation feature, you need to expose your local server to GitHub and configure a webhook.

1.  **Expose your local server**: Use a tool like [ngrok](https://ngrok.com/) to create a public URL for your local server.
    ```bash
    ngrok http 3000
    ```
    This will provide a public URL (e.g., `https://<your-ngrok-id>.ngrok-free.app`).

2.  **Configure the webhook on your GitHub repository**:
    *   Navigate to your desired GitHub repository's `Settings` → `Webhooks` → `Add webhook`.
    *   **Payload URL**: Enter the `ngrok` URL followed by DocSync's webhook endpoint: `https://<your-ngrok-id>.ngrok-free.app/api/github/webhook`.
    *   **Content type**: Select `application/json`.
    *   **Secret**: (Optional, but recommended) Enter the same `WEBHOOK_SECRET` value you set in your `.env` file. This enables signature verification.
    *   **Events**: Choose `Let me select individual events` and select **only "Pull requests"**.
    *   Ensure the `Active` checkbox is ticked.

3.  **Test it**: Create a new branch, push some code changes, and open a Pull Request in the configured repository. DocSync should automatically post an analysis comment on the PR.

### Deploying Live (Recommended)

For continuous operation without `ngrok` or your local machine, deploying DocSync to a cloud hosting platform like **Render.com** is recommended.

1.  **Create an account** on [Render](https://render.com/) and connect your GitHub repository.
2.  Click **New +** → **Web Service**.
3.  Select your DocSync repository.
4.  Configure the build settings:
    *   **Root Directory**: `DocSync_AI-powered_Technical_Documentation_Generator` (adjust if your code is in a sub-folder).
    *   **Runtime**: `Node`.
    *   **Build Command**: `npm install && npm run build`.
    *   **Start Command**: `node dist/server.cjs`.
5.  Add your **Environment Variables**:
    *   `GEMINI_API_KEY` = your API key.
    *   `GITHUB_TOKEN` = your GitHub personal access token.
    *   `WEBHOOK_SECRET` = your custom webhook secret.
6.  Click **Create Web Service**.
7.  Once deployed, copy your new live URL (e.g., `https://docsync-agent.onrender.com`) and **update your GitHub Webhook Payload URL** in your repository settings to this new live URL.

### Using the Dashboard

The DocSync web interface provides dedicated tabs for various functionalities:

| Tab                       | Functionality                                                                  |
| :------------------------ | :----------------------------------------------------------------------------- |
| **Dashboard**             | Select a repository to analyze its structure, generate `DOCSYNC.md`, and commit it back to GitHub. |
| **Test Playground**       | Paste arbitrary code snippets to instantly generate Markdown documentation and copy to clipboard. |
| **Webhook Activity**      | Monitor all incoming GitHub webhook events in real-time with statuses and statistics. |
| **Doc History**           | Browse and review a chronological log of all past AI-generated documentation for Pull Requests. |
| **Setup & Integration**   | In-app guide providing instructions for configuring your GitHub token and webhook settings. |

## 🛠️ Technologies Used

DocSync is built upon a modern and robust technology stack:

| Layer            | Stack                                      |
| :--------------- | :----------------------------------------- |
| **Frontend**     | React, TypeScript, Tailwind CSS, Vite      |
| **Backend**      | Node.js, Express.js, TypeScript            |
| **AI Model**     | Google Gemini 2.5 Flash (`@google/genai`)  |
| **Security**     | HMAC-SHA256 signature verification, Rate Limiting |
| **Markdown**     | `react-markdown` (for rendering markdown)  |
| **Icons**        | `lucide-react`                             |
| **Animations**   | `motion` (Framer Motion)                   |

## 📄 License

This project is licensed under the [MIT License](LICENSE.md).